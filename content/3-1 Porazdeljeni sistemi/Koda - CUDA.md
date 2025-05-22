### Osnove
```go
func main() {

	// preberemo argumente iz ukazne vrstice
	bPtr := flag.Int("b", 1, "num blocks")
	tPtr := flag.Int("t", 1, "num threads")
	flag.Parse()

	// inicializiramo napravo
	dev, err := cuda.Init(0)
	if err != nil {
		panic(err)
	}
	defer dev.Close()

	// zaženemo kodo na napravi
	gridSize := cuda.Dim3{X: uint32(*bPtr), Y: 1, Z: 1}
	blockSize := cuda.Dim3{X: uint32(*tPtr), Y: 1, Z: 1}
	err := cudago.Hello(gridSize, blockSize)
	if err != nil {
		panic(err)
	}
}
```
```c
__global__ void Hello() {
	printf("Hello from thread %d.%d!\n", blockIdx.x, threadIdx.x);
}
```
### Prenašanje v pomnilnik
Rezervacija pomnilnika na gostitlju in globalnega pomnilnika na napravi:
```go
hm := make(...)
dm, err := cuda.DeviceMemAlloc(count uint64)
```
Prenašanje podatkov med pomnilnikom gostitelja in globalnim pomnilnikom naprave:
```go
err = dm.MemcpyToDevice(hmPtr *unsafe.Pointer, count uint64)
err = dm.MemcpyFromDevice(hmPtr unsafe.Pointer, count uint64)
```
### Razlika vektorjev
```go
func main() {

	// preberemo argumente iz ukazne vrstice
	numBlocksPtr := flag.Int("b", 1, "num blocks")
	numThreadsPtr := flag.Int("t", 1, "num threads")
	vectorSizePtr := flag.Int("s", 1, "vector size")
	flag.Parse()
	if *numBlocksPtr < 0 || *numThreadsPtr <= 0 || *vectorSizePtr <= 0 {
		panic("Wrong arguments")
	}

	// izračunamo potrebno število blokov
	numBlocks := *numBlocksPtr
	if numBlocks == 0 {
		numBlocks = (*vectorSizePtr-1) / *numThreadsPtr + 1
	}

	var err error

	// inicializiramo napravo
	dev, err := cuda.Init(0)
	if err != nil {
		panic(err)
	}
	defer dev.Close()

	// rezerviramo pomnilnik na gostitelju
	hc := make([]float32, *vectorSizePtr)
	ha := make([]float32, *vectorSizePtr)
	hb := make([]float32, *vectorSizePtr)

	// rezerviramo pomnilnik na napravi
	bytesFloat32 := int(unsafe.Sizeof(float32(0.0)))
	bytesVector := uint64(*vectorSizePtr * bytesFloat32)

	dc, err := cuda.DeviceMemAlloc(bytesVector)
	if err != nil {
		panic(err)
	}
	defer dc.Free()
	da, err := cuda.DeviceMemAlloc(bytesVector)
	if err != nil {
		panic(err)
	}
	defer da.Free()
	db, err := cuda.DeviceMemAlloc(bytesVector)
	if err != nil {
		panic(err)
	}
	defer db.Free()

	// nastavimo vrednosti vektorjev a in b na gostitelju
	for i := 0; i < *vectorSizePtr; i++ {
		ha[i] = rand.Float32()
		hb[i] = rand.Float32()
	}

	// prenesemo vektorja a in b iz gostitelja na napravo
	err = da.MemcpyToDevice(unsafe.Pointer(&ha[0]), bytesVector)
	if err != nil {
		panic(err)
	}
	err = db.MemcpyToDevice(unsafe.Pointer(&hb[0]), bytesVector)
	if err != nil {
		panic(err)
	}

	// zaženemo kodo na napravi
	gridSize := cuda.Dim3{X: uint32(numBlocks), Y: 1, Z: 1}
	blockSize := cuda.Dim3{X: uint32(*numThreadsPtr), Y: 1, Z: 1}
	err = cudago.VectorSubtract4(gridSize, blockSize, dc.Ptr, da.Ptr, db.Ptr, int32(*vectorSizePtr))
	if err != nil {
		panic(err)
	}

	// vektor c prekopiramo iz naprave na gostitelja
	err = dc.MemcpyFromDevice(unsafe.Pointer(&hc[0]), bytesVector)

	// počakamo, da se procesiranje zahtev na napravi zaključi
	err = cuda.CurrentContextSynchronize()
	if err != nil {
		panic(err)
	}
}
```
```c
__global__ void vectorSubtract4(float *c, const float *a, const float *b, int len) {
	// določimo globalni indeks elementov
	int gid = blockIdx.x * blockDim.x + threadIdx.x;
	// št. niti < dolžina vektorjev => morajo nekatere izračunati več razlik
	while (gid < len) {
		c[gid] = a[gid] - b[gid];
		gid += gridDim.x * blockDim.x;
	}
}
```
### Razdalja vektorjev
```go
func main() {
    // Inicializacija
    ...

	// velikosti struktur v bajtih
	bytesFloat32 := int(unsafe.Sizeof(float32(0.0)))
	bytesVector := uint64(*vectorSizePtr * bytesFloat32)
	bytesPartialSum := uint64(numBlocks * bytesFloat32)
	bytesLocalMemory := uint64(*numThreadsPtr * bytesFloat32)

	// rezerviramo pomnilnik na napravi
	...

	// nastavimo vrednosti vektorjev a in b na gostitelju
	...

	// prenesemo vektorja a in b iz gostitelja na napravo
	...

	// zaženemo kodo na napravi
	gridSize := cuda.Dim3{X: uint32(numBlocks), Y: 1, Z: 1}
	blockSize := cuda.Dim3{X: uint32(*numThreadsPtr), Y: 1, Z: 1}
	err = cudago.VectorDistanceLD4Ex(gridSize, blockSize, bytesLocalMemory, nil, dp.Ptr, da.Ptr, db.Ptr, int32(*vectorSizePtr))
	if err != nil {
		panic(err)
	}

	// počakamo, da se procesiranje zahtev na napravi zaključi
	...

	// vektor p prekopiramo iz naprave na gostitelja
	err = dp.MemcpyFromDevice(unsafe.Pointer(&hp[0]), bytesPartialSum)

	// dokončamo izračun razdalje za napravo
	distDevice := float64(0.0)
	for i := 0; i < numBlocks; i++ {
		distDevice += float64(hp[i])
	}
	distDevice = math.Sqrt(distDevice)
}
```
```c
__global__ void vectorDistanceLD4(float *p, const float *a, const float *b, int len) {
	// skupni pomnilnik niti v bloku
	extern __shared__ float part[];
	part[threadIdx.x] = 0.0;

	// kvadriranje razlike
	int gid = blockIdx.x * blockDim.x + threadIdx.x;
	float diff;
	while (gid < len) {
		diff = a[gid] - b[gid];
		part[threadIdx.x] += diff * diff;
		gid += gridDim.x * blockDim.x;
	}

	// počakamo, da vse niti zaključijo
	__syncthreads();

	// izračunamo delno vsoto za blok niti
	int idxStep;
	for(idxStep = blockDim.x >> 1; idxStep > 32 ; idxStep >>= 1) {
		if (threadIdx.x < idxStep)
			part[threadIdx.x] += part[threadIdx.x+idxStep];
		__syncthreads();
	}
	for( ; idxStep > 0 ; idxStep >>= 1 ) {
		if (threadIdx.x < idxStep)
			part[threadIdx.x] += part[threadIdx.x+idxStep];
		__syncwarp();
	}

	if (threadIdx.x == 0)
		p[blockIdx.x] = part[0];
}
```
