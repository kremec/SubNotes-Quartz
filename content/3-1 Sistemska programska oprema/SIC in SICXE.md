## Simplified Instructional Computer
### Pomnilnik
Velikost:
- $8$b pomnilnik
- ena beseda po $3$B=$24$b
- celoten pomnilnik obsega $2^{15}=32768$ B
Delovanje:
- naslavlja se posamezne bajte
- besede se naslavlja z lokacijo najnižjega bajta
- big-endian
### Registri
5 registrov, vsak velik $24$b:
- A - akumulator: aritmetične operacije
- X - indeks: indeks po tabeli
- L - linkage: povratni naslov pri skokih
- PC - programski števec
- SW - status / zastavice
A, X in L registre lahko uporabimo kot pomožne
### Formati podatkov
Cela števila: 24b predznačeno število, dvojiški komplement
Znaki: 8b ASCII
Ni aritmetike realnih števil
### Formati ukazov
![[Hipotetični Simplified Instructional Computer-Image-1.png|300]]
- OPCODE: št. strojnega ukaza
- X: način naslavljanja (1 $\rightarrow$ **indeksno naslavljanje** - vrednosti naslova se prišteje vrednost v X)
- NASLOV
### Načini naslavljanja
- UN ... uporaben naslov - vrednost (p)
- (UN) ... dereferenciran UN - vrednost na naslovu UN (\*p)
- ((UN)) ... dvojno deferenciran UN - vrednost na naslovu, ki je zapisan na naslovu UN (\*\*p)

Naslavljanja glede na **način izračuna UN**:
- **neposredno** (direct): UN = naslov
- relativno (relative):
    - **bazno-relativno**: UN = (B) + odmik $\rightarrow$ (0 ... 4095)
    - **PC-relativno**: UN = (PC) + odmik $\rightarrow$ (-2048 ... 2047)
**SIC pozna le neposredni način** naslavljanja, ki ga lahko kombiniramo z indeksnim naslavljanjem
### Nabor ukazov
#### Ukazi procesorju
Delo z registri:
- LDA, LDL: Load A $\leftarrow$ \[mem\] / L $\leftarrow$ \[mem\]
- STA, STL: Store \[mem\] $\rightarrow$ A
Aritmetične operacije: vse delujejo na registru A
- ADD, SUB, DIV, MUL (npr. SUB ONE ... A=A-(ONE))
Primerjava:
- COMP: rezultat primerjave ($<,>,=$) se shrani v **Condintional Code** v SW
Skoki:
- JLT, JGT, JEQ: pogojni skoki se izvedejo glede na stanje CC zastavice
- J: brezpogojen skok
Podprogrami:
- JSUB: vrednost PC se shrani v L
- RSUB: vrednost PC se vrne iz L
#### Zbirniška navodila - ukazi zbirniku
- RESW, RESB: rezervira prostor na oznaki labele za določeno št. besed ali bajtov
- BYTE, WORD: rezervacija pomnilnika in inicializacija
- START: označi ime in začetni naslov izvajalne kode programa (preskočimo podatkovni del)
- END: označi konec programa
### Vhod in izhod
Naprave podane z 8b kodo, prenašamo 1B med pomnilnikom in napravo
Po POSIX standardu so 0 ... stdin, 1 ... stdout in 2 ... stderr
- TD: preveri, ali je naprava pripravljena za branje/pisanje - rezultat se zapiše v CC zastavico
## SIC eXtra Equipment
Nadgradnja procesorja SIC, navzdol 100% kompatibilen s SIC
### Pomnilnik
Celoten pomnilnik obsega 1MB=$2^{20}$b $\rightarrow$ dodani načini naslavljanja, dodatni formati ukazov
### Registri
Dodatni registri:
- B - bazni register: za bazno-relativno naslavljanje
- S in T - splošnonamenska registra
- F - floating point: izjemoma velik 48b
### Formati podatkov
Realna števila - 48b:
![[Hipotetični računalnik-Image-1.png|400]]
$$
x=(s==0\ ?\ 1:-1)*m*2^{e-1024}
$$
### Formati ukazov
4 formati:
#### Format 1
Format 1B=8b: ukazi brez operanda
![[Hipotetični računalnik-Image-2.png|100]]
#### Format 2
Format 2B=16b: registrsko-registrski ukazi
![[Hipotetični računalnik-Image-3.png|300]]
Številčenje registrov:
![[Hipotetični računalnik-Image-4.png|300]]
#### Format 3
Format 3B=24b:
![[Hipotetični računalnik-Image-5.png|400]]
Pomen bitov:

| b   | p   | način naslavljanja |
| --- | --- | ------------------ |
| 0   | 0   | neposredno         |
| 0   | 1   | PC-relativno       |
| 1   | 0   | bazno-relativno    |
| 1   | 1   | NI MOŽNO           |

| n   | i   | naslavljanje     | operand |
| --- | --- | ---------------- | ------- |
| 0   | 0   | stari SIC format |         |
| 0   | 1   | takojšnje        | UN      |
| 1   | 0   | posredno         | ((UN))  |
| 1   | 1   | enostavno        | (UN)    |
e bit = 0
#### Format 4
Format 4B=32b: pomen bitov enak kot v formatu 3
![[Hipotetični računalnik-Image-6.png|400]]
e bit = 1