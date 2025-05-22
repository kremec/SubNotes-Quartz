### x86
- ==mov== (Move): prenos vrednosti
  `mov eak,naslov` $\rightarrow$ `eax=(naslov)`
- ==lea== (Load Effective Address): prenos naslova
  `lea eax,naslov` $\rightarrow$ `eax=naslov`
- ==add / sub== (Integer Addition / Subtraction)
  `add eax,naslov` $\rightarrow$ `eax=eax+(naslov)`
- ==inc / dec== (Increment / Decrement)
- ==imul== (Integer Multiplication)
  `imul eax,naslov` $\rightarrow$ `eax=eax*(dword)(naslov)`
- ==idiv== (Integer Division): 64b deljenec, sestavljen zgoraj 32b iz `edx` in spodaj 32b iz `eex`; kvocient se zapiše v `eax`, ostanek pa v `edx`
  `idiv ebx` $\rightarrow$ `edx:eex / ebx = eax:edx`
- ==and / or / xor / not / shl / shr== (npr. `shl`-shift left hitrejše kot množenje z 2)
- ==db / dw / dd== (Declare Byte / Word / Double): deklaracija in/ali inicializacija
  `a db ?` $\rightarrow$ `char a` / `b dw 64` $\rightarrow$ `short b = 64` / `c dd 1,2,3` $\rightarrow$ `int c[] = {1,2,3}` /  `d dw 10 dup(?)` $\rightarrow$ `int d[10]`
### JVM bytecode
Prva črka nakazuje tip podatkov, po mnemoniku zapisan indeks spremenljivke:
![[Koda-Image-1.png|300]]
Konstante:
- Najpogosteje uporabljene konstante: `iconst_0`, `fconst_2`, ...
- Ostalo: `ldc <št_konstante_v_naboru_konstant>`

Prenos med lokalnimi spremenljivkami in skladom:
- `iload_0` ... 1. lokalno spremenljivko integer prenesi na sklad
- `fstore_2`
- `iload <lokalna_spremenljivka>` / `astore <lokalna_spremenljivka>`

Delo s skladom:
- `pop`/`pop2` ... izbriši 1/2 besedi z vrha sklada
- `dup`/`dup2` ... podvoji 1/2 besedi na vrhu sklada
- `swap` ... zamenja zgornji 2 besedi na skladu

Pretvorba tipov: `i2l`, `i2f`, ..., `l2d`, ..., `d2f`

Aritmetične in logične operacije:
- `iadd`, `ladd`, `isub`, `lmul`, `lrem`
- `fadd`, ...
- `iand`, `ior`, `ishl`, ...

Primerjava vrha sklada:
- z 0: `ifeq`, `ifne`, ...
- z 2. elementom sklada: `if_cmpeq`, `if_cmplt`, ...

Preusmerjanje izvajanja: parameter `<odmik>` pri primerjavah / `goto <odmik>`