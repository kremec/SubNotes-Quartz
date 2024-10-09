## SIC
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
- X: način naslavljanja (1 $\rightarrow$ indeksno naslavljanje - vrednosti naslova se prišteje vrednost v X)
- NASLOV
- 