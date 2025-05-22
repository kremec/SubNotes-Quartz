==Moorov zakon==: podvojitev št. tranzistorjev na čipih vsaki 2 leti
## Arhitektura
### Pomnilnik in registri
32b registri $\rightarrow$ do 4GB pomnilnika ("protected mode" omejitev preseže)
- osnovna naslovljiva enota: 1B
- beseda (WORD): 2B
- dvojna beseda (DWORD): 4B
- podaljšana beseda (QWORD): 8B

Razširjanje starih registrov v nove in nove
#### Načini naslavljanja
- ==Registrsko==: prenos operandov med registri (npr. `mov eax,ebx`)
- ==Takojšnje== (npr. `mov eax,20`)
- ==Neposredno==: iz pomnilnika preko podanega naslova (npr. `mov ebx,[1000]`)
- ==Neposredno z odmikom== (npr. `mov ebx,[tabela+5]`)
- ==Registrsko posredno==: dostop do pomnilnika preko naslova iz registra (npr. `mov ebx,[ebx+5]`)
### Formati ukazov
![[IA 32 oz. x86-Image-1.png|500]]
==Prefix==: način delovanja ukaza (npr. F2: REP $\rightarrow$ ukaz ponovi ECX-krat)
==Opcode==: možno več opcode-ov za isti ukaz - opcije (npr. ADD: 000000ds $\rightarrow$ d=direction (pomnilnik, register), s=size(8b, 16/32b))
==Mod R/M==:
- ==Mod==: način naslavljanja
- ==Reg==: katere registre bomo uporabili
- ==R/M==: način uporabe registrov

==SIB==: UN = odmik + scale\*index + base
==Odmik==: odmik
==Immediate==: operand
#### Najpomembnejši ukazi
- ==mov== (Move): prenos vrednosti (npr. `mov eak,naslov` $\rightarrow$ `eax=(naslov)`)
- ==lea== (Load Effective Address): prenos naslova (npr. `lea eax,naslov` $\rightarrow$ `eax=naslov`)
- ==add / sub== (Integer Addition / Subtraction) (npr. `add eax,naslov` $\rightarrow$ `eax=eax+(naslov)`)
- ==inc / dec== (Increment / Decrement)
- ==imul== (Integer Multiplication) (npr. `imul eax,naslov` $\rightarrow$ `eax=eax*(dword)(naslov)`)
- ==idiv== (Integer Division): 64b deljenec, sestavljen zgoraj 32b iz `edx` in spodaj 32b iz `eex`; kvocient se zapiše v `eax`, ostanek pa v `edx` (npr. `idiv ebx` $\rightarrow$ `edx:eex / ebx = eax:edx`)
- ==and / or / xor / not / shl / shr== (npr. `shl`-shift left hitrejše kot množenje z 2)
### Sklad
Shranjevanje 32b vrednosti lokalnih spremenljivkih in rezultatov
ESP kaže na vrh sklada - zadnje odloženi element
Ukaza:
- `PUSH <reg32/mem/const32>` $\rightarrow$ ESP -= 4, operand odloži na ESP
- `POP <reg32/mem>` $\rightarrow$ vrednost na ESP shrani v operand, ESP += 4
<br><br><br><br><br>
#### Podprogrami - calling convention
1. Stanje sklada tik pred klicem funkcije:
![[IA 32 oz. x86-Image-2.png|180]]
2. `JUMP ime_podprograma`
3. `push ebp`, `mov ebp,esp`, `sub esp,20`
![[IA 32 oz. x86-Image-3.png|180]]
4. Pridobivanje:
    - i-te lokalne spremenljivke: `mov eax,[ebp-4*(i+1)]`
    - i-tega parametra: `mov eax,[ebp+8+i*4]`
5. Rezultat podprograma shranimo v `eax`
6. `push esp,ebp`, `pop ebp` $\rightarrow$ ESP vrnemo na EBP in pop na povratni naslov
### Zastavice
Opisujejo stanje procesorja, nastavljajo se kot posledica operacij ali ročno, shranjene v registru `FLAGS=EFLAGS:RFLAGS`
#### Kontrolne zastavice
==DF== (Direction Flag): vpliva na smer "auto-increment" operacij (npr. kopiranje big ali little endian)
- `DF=0` $\rightarrow$ od spodnjega proti zgornjemu / `DF=1` $\rightarrow$ od zgornjega proti spodnjemu
#### Statusne zastavice
==ZF== (Zero Flag): zadnji rezultat = 0 $\rightarrow$ `ZF=1`
==SF== (Sign Flag): zadnji rezultat < 0 $\rightarrow$ `SF=1`
==PF== (Parity Flag): spodnjih 8b rezultsts ima sodo enic $\rightarrow$ `PF=1`
==CF== (Carry Flag) / ==OF== (Overflow Flag): napačen rezultat prejšnje nepredznačene / predznačene aritmetične operacije
### Direktive za deklaracijo in inicializacijo
==DB== (Declare Byte) / ==DW== (Declare Word) / ==DD== (Declare Double)
- `a db 64` $\rightarrow$ `char a = 64`
- `b dw ?` $\rightarrow$ `short b`
- `c dd 1,2,3` $\rightarrow$ `int c[] = {1,2,3}`
- `d dd 100 dup(0)` $\rightarrow$ `int d[100]` + inicializacija na 0
- `str db 'hello',0` $\rightarrow$ `char str[] = "Hello"` (`[H,e,l,l,o, \0]`)
### Sistemski klici
Kličemo prekinitev `int 0x80`: številka sistemskega kilca v `eax`, parametri v ostalih registrih
![[IA 32 oz. x86-Image-5.png|400]]
### Sintaksa Intel vs AT&T
- Posebni znaki pred operandi (`push 4` $\rightarrow$ `pushl $4`)
- Vrstni red operandov (`add eax,4` $\rightarrow$ `addl $4,%eax`)
- Dodatni znak na koncu ukaza pove velikost operanda (`mov al,byte ptr foo` $\rightarrow$ `movb foo,%al`)
- Dolgi skoki (`call/jmp far section:offset` $\rightarrow$ `lcall/jump $section,$offset`)