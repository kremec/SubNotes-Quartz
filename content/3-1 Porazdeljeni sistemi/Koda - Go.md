### Model razcepi-pridruži
```go
var wg sync.WaitGroup

func hello(s string) {
	defer wg.Done()
	for i := 0; i < 5; i++ {
		fmt.Print(s, " ")
		time.Sleep(time.Millisecond)
	}
}

func main() {
	wg.Add(1)
	go hello("hello")
	
	wg.Add(1)
	go hello("world")
	
    wg.Add(1)
	hello("!")
	
	wg.Wait()
	fmt.Println()
}
```
### Kanali - osnove
```go
var dataStream chan int
dataStream = make(chan int)

var bufferStream = make(chan int, 4)

// Pisanje
dataStream <- 314

// Branje
value, ok := <-dataStream    // 314, true
close(dataStream)
value, ok := <-dataStream    // 0, false

for msg := range stringStream {
    // ...
}
```
### Kanali - sinhronizacija
Funkcija `speaker` da gorutinam `listener` signal kdaj lahko nadaljujejo
S `struct{}` poudarimo, da kanal ni namenjen prenašanju sporočil, temveč sinhronizaciji
```go
func speaker(message string) <-chan struct{} {
	broadcastStream := make(chan struct{})
	
	go func() {
		time.Sleep(5 * time.Second)
		fmt.Println("Announcement:", message)
		close(broadcastStream)
	}()

	return broadcastStream
}

func listener(id int, broadcastStream <-chan struct{}) {
	fmt.Println("Listener", id, "is waiting for an announcement.")

	<-broadcastStream

	fmt.Println("Listener", id, "completed.")
}

func main() {
	broadcastStream := speaker("Hello world for the last time!")

	for i := 1; i < 5; i++ {
		go listener(i, broadcastStream)
	}
	listener(0, broadcastStream)

	fmt.Println("Great!")

	time.Sleep(1 * time.Second)
}
```
Gorutini `writer` neprestano pišeta vsaka v svoj kanal
Gorutina `reader` bere in obdeluje sporočila iz več kanalov
Dodamo kanal za zaustavitev gorutine reader - glavna gorutina sproži zaustavitev po 20 sekundah
```go
var wg sync.WaitGroup

func writer(id int) <-chan string {
	stream := make(chan string)
	go func() {
		defer close(stream)
		for {
			stream <- "message from " + strconv.Itoa(id)
			time.Sleep(time.Duration(id*id+1) * time.Second)
		}
	}()
	return stream
}

func reader(stream1 <-chan string, stream2 <-chan string, streamDone <-chan struct{}) {
	defer wg.Done()
	for {
		select {
		case msg1 := <-stream1:
			fmt.Println(msg1)
		case msg2 := <-stream2:
			fmt.Println(msg2)
		case <-streamDone:
			fmt.Println("Done")
			return
		case <-time.After(1 * time.Second):
			fmt.Println("timeout")
		default:
		}
	}
}

func main() {
	writer1Stream := writer(1)
	writer2Stream := writer(2)
	streamDone := make(chan struct{})

	wg.Add(1)
	go reader(writer1Stream, writer2Stream, streamDone)

	time.Sleep(20 * time.Second)
	close(streamDone)

	wg.Wait()
}
```
### Sinhronizacija - ključavnice
Uporaba ključavnice:
```go
var result int
var wg sync.WaitGroup
var lock sync.Mutex

func worker() {
	defer wg.Done()
	
	lock.Lock()
    result++
    lock.Unlock()
}

func main() {
	wg.Add(*gPtr)
	for id := 0; id < 10; id++ {
		go worker()
	}
	wg.Wait()
}
```
Uporaba `atomic` spremenljivk:
```go
var result atomic.Int64
var wg sync.WaitGroup

func worker() {
	defer wg.Done()
	
	result.Add(1)
}

func main() {
	wg.Add(*gPtr)
	for id := 0; id < 10; id++ {
		go worker()
	}
	wg.Wait()
}
```
Če gorutine veliko dostopajo do skupne spremenljivke:
- lokalna spremenljivka kot delni rezultat, kasneje uporaba le ene ključavnice
- delne rezultate se pošilja v kanal, glavna gorutina čaka na `štGorutin` prebranih vrednosti
<br>
Bralno-pisalna ključavnica:
```go
var wg sync.WaitGroup
var lockBook sync.RWMutex

func writer(id int, cycles int) {
	defer wg.Done()

	for i := 0; i < cycles; i++ {
		lockBook.Lock()

		fmt.Println("Writer", id, "start", i)
		time.Sleep(time.Duration(id) * time.Millisecond)
		fmt.Println("Writer", id, "finish", i)

		lockBook.Unlock()

		time.Sleep(time.Duration(id) * time.Millisecond)
	}
}

func reader(id int) {

	for {
		lockBook.RLock()

		fmt.Println("Reader", id, "start")
		time.Sleep(time.Duration(id) * time.Millisecond)
		fmt.Println("Reader", id, "finish")

		lockBook.RUnlock()

		time.Sleep(time.Duration(id) * time.Millisecond)
	}
}

func main() {
	// preberemo argumente
	writersPtr := flag.Int("w", 2, "# of writers")
	readersPtr := flag.Int("r", 4, "# of readers")
	cyclesPtr := flag.Int("c", 10, "# of cycles")
	flag.Parse()

	// zaženemo pisatelje
	wg.Add(*writersPtr)
	for i := 1; i <= *writersPtr; i++ {
		go writer(i, *cyclesPtr)
	}
	// zaženemo bralce
	for i := 1; i <= *readersPtr; i++ {
		go reader(i)
	}
	// počakamo, da pisatelji zaključijo
	wg.Wait()
}
```
Uporaba `sync.Map` kot slovar:
```go
func writeToMap(id int, steps int, dict *sync.Map) {
	defer wg.Done()
	dict.Store(id, 0)
	for i := 0; i < steps; i++ {
		dict.Store(id, i)
	}
}

func readFromMap(id int, steps int, dict *sync.Map) {
	defer wg.Done()
	for i := 0; i < steps; i++ {
		_, _ = dict.Load(id)
	}
}

func main() {
	gwPtr := flag.Int("gw", 1, "# of writing goroutines")
	grPtr := flag.Int("gr", 1, "# of reading goroutines")
	sPtr := flag.Int("s", 100, "# of read or write steps")
	flag.Parse()

	var dict sync.Map
	records := max(*gwPtr, *grPtr)
	for i := 0; i < records; i++ {
		dict.Store(i, 0)
	}

	timeStart := time.Now()
	for i := 0; i < *gwPtr; i++ {
		wg.Add(1)
		go writeToMap(i, *sPtr, &dict)
	}
	for i := 0; i < *grPtr; i++ {
		wg.Add(1)
		go readFromMap(i, *sPtr, &dict)
	}
	wg.Wait()

	fmt.Print("dict: map[")
	dict.Range(
		func(k, v interface{}) bool {
			fmt.Print(k, ":", v, " ")
			return true
		})
	fmt.Println("\b] time:", time.Since(timeStart))
}
```