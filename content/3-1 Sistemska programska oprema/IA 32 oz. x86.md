Intel Architecture 32b
==Moorov zakon==: podvojitev št. tranzistorjev na čipih vsaki 2 leti
## Arhitektura
### Pomnilnik in registri
32b registri $\rightarrow$ do 4GB pomnilnika ("protected mode" omejitev preseže)
- osnovna naslovljiva enota: 1B
- beseda (WORD): 2B
- dvojna beseda (DWORD): 4B
- podaljšana beseda (QWORD): 8B

Razširjanje starih registrov v nove in nove
### Formati ukazov
![[IA 32 oz. x86-Image-1.png|500]]
==Prefix==: način delovanja ukaza
(npr. F2: REP $\rightarrow$ ukaz ponovi ECX-krat)
==Opcode==: možno več opcode-ov za isti ukaz - opcije
(npr. ADD: 000000ds $\rightarrow$ d=direction (pomnilnik, register), s=size(8b, 16/32b))
==Mod R/M==:
- ==Mod==: način naslavljanja
- ==Reg==: katere registre bomo uporabili
- ==R/M==: način uporabe registrov
==SIB==: UN = odmik + scale\*index + base
==Odmik==: odmik
==Immediate==: operand
### Sklad
Shranjevanje 32b vrednosti lokalnih spremenljivkih in rezultatov
ESP kaže na vrh sklada - zadnje odloženi element
Ukaza:
- PUSH <reg32/mem/const32> $\rightarrow$ ESP -= 4, operand odloži na ESP
- POP <reg32/mem> $\rightarrow$ vrednost na ESP shrani v operand. ESP += 4
Klic podprograma s parametri:
1. Stanje sklada tik pred klicem funkcije:
![[IA 32 oz. x86-Image-2.png|200]]
2. `JUMP ime_podprograma`
3. `push ebp`, `mov ebp,esp`, `sub esp,20`
![[IA 32 oz. x86-Image-3.png|200]]
4. Pridobivanje:
    - i-te lokalne spremenljivke: `mov eax,[ebp-4*(i+1)]`
    - i-tega parametra: `mov eax,[ebp+8+i*4]`
5. Rezultat podprograma shranimo v eax
6. `push esp,ebp`, `pop ebp` $\rightarrow$ ESP vrnemo na EBP in pop na povratni naslov