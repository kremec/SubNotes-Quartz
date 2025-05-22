Vhod: zaporedje strojnih ukazov z začasnimi spremenljivkami
Izhod: zaporedje strojnih ukazov z začasnimi spremenljivkami + inferenčni graf spremenljivk

Določanje aktivnosti spremenljivk predstavlja problem podatkovnega toka (eng. dataflow problem)
### Podatkovni tokovi
Spremenljivka je aktivna, če hrani vrednost, ki jo program kasneje uporablja.

`use(n)` ... množica vseh spremenljivk, iz katerih ukaz bere
`def(n)` ... množica vseh spremenljivk, v katere ukaz piše
`succ(n)` ... množica vozlišč grafa toka, iz katerih je dosegljivo vozlišče `n`
`pred(n)` ... množica vozlišč grafa toka, ki so dosegljiva iz vozlišča `n`
### Izračun aktivnosti spremenljivk
Spremenljivka je aktivna na povezavi, če od povezave po grafu toka navzdol naletimo na `use` brez drugih `def`-ov
- spremenljivka je aktivna na vhodu vozlišča (`in[n]`), če je živa na katerikoli vhodni povezavi vozlišča
- spremenljivka je aktivna na izhodu vozlišča (`out[n]`), če je živa na katerikoli izhodni povezavi vozlišča
$$
\begin{align} in(n)&=use(n)\cup (out(n)-def(n)) \\ out(n)&=\bigcup_{s\in succ(n)}in(s) \end{align}
$$
Reševanje enačb podkatkovnih tokov poteka v vrstnem redu, obratnem kontrolnemu toku podatkov $\rightarrow$ urejanje vozlišč se naredi z globinskim iskanjem

Računanje `in` in `out` za vsa vozlišča ponavljamo, dokler se izračuni ne ustalijo
#### Statična in dinamična aktivnost
Problem izračunljivosti pri pogojnih vejitvah nam preprečuje optimalno upoštevanje rezultata in posledično skoka $\rightarrow$ vse dobljene rešitve so le konzervativni približki, obstaja več rešitev
- ==dinamična aktivnost== spremenljivke v vozlišču: obstaja izvedba programa, ki poteka preko vozlišča do uporabe spremenljivke, ne da bi pri tem šla čez novo definicijo spremenljivke
- ==statična aktivnost== spremenljivke v vozlišču: obstaja pot po povezavah toka od vozlišča do uporabe spremenljivke, ne da bi pri tem šla čez novo definicijo spremenljivke

Prevajalnik načeloma deluje na podlagi statične aktivnosti, ker splošnega algoritma za dinamično aktivnost ni
### Interferenčni grafi
Spremenljivke, ki v končnem izračunu `in` ali `out` kateregakoli vozlišča niso skupaj, gredo lahko v isti register.

==Interferenca==: pogoj, ki preprečuje dodelitev začasnih spremenljivk istemu registru (prekrivanje dosegov aktivnosti spremenljivk)

Interferenčni graf:
- vozlišča ... začasna spremenljivka
- povezava ... začasni spremenljivki sta vsaj enkrat istočasno aktivni

Možna optimizacija ukazov, ki vrednost enega registra prestavijo v drug register: če se originalna vrednost ne spremeni, potrebujemo le en register za dostopanje do obeh (enakih) vrednosti