# Lokalni preiskovalni algoritmi
Namesto sistematičnega preiskovanja izvajajo ==iterativno ocenjevanje==:
- izberi začetno množico stanj
- poišči sosednja stanja od trenutnega, pri tem ne ohranjaj poti
- ponavljaj do ustavitvenega pogoja

==Zanima nas le kakovost rešitve, brez poti do nje==
- manjša poraba prostora
- dobimo dober približek v prostorih, prevelikih za sistematično preiskovanje

==Kriterijska funkcija==: ocena kakovosti rešitve
Iščemo globalni maksimum glede na kriterijsko funkcijo, težave:
- lokalni maksimumi: obtičimo v lokalnem optimumu, vsi sosedi slabši kot trenutno stanje
- planote: obtičimo v konstantni vrednosti kriterijske funkcije
- grebeni: za plezanje navzgor bi bil potreben sestop
### Plezanje na hrib (hill-climbing / greedy-local search)
Strategija: Premikaj se po prostoru stanj ==v smeri najboljše izboljšave kriterijske funkcije==
##### Reševanje iz lokalnih maksimumov
- ==Koraki vstran==: v primeru iste vrednosti kriterijske funkcije dovolimo premik v to stanje, smiselno omejiti št. korakov vstran (npr. v primeru planote)
- ==Stohastičnost==: naslednje stanje izberemo verjetnostno
- ==Naključni ponovni zagon==: večkratni zagon iz naključnih začetnih stanj
### Simulirano ohlajanje
Strategija optimizacijskega algoritma: generiramo naključne sosede trenutnega vozlišča
- najdemo boljše stanje $\rightarrow$ vedno izberemo
- ==najdemo slabše stanje $\rightarrow$ izberemo z določeno verjetnostjo, ki s časom pada==
### Lokalno iskanje v snopu
Strategija: hranimo $k$ stanj $\rightarrow$ izbiramo $k$ optimalnih sosedov (ni enako kot $k$ vzporednih iskanj - ocenjujemo kakovost cele generacije hkrati)
Problem: celoten snop iskanj lahko obtiči v lokalnih maksimumih
Rešitev: stohastično iskanje v snopu - naslednike izberemo naključno z verjetnostjo sorazmerno njihovi kakovosti
# Preiskovanje brez informacije o stanju
Okolje:
- ==transparentno==: agent zazna popolno informacijo $\rightarrow$ preiskovanje ==prostora dejanskih stanj==
- ==netransparentno==: agent nima informacije o stanju $\rightarrow$ preiskovanje ==prostora verjetnih stanj==
Definicija:
- ==verjetna stanja==: prostor, sestavljen iz ==potenčne množice vseh možnih dejanskih stanj== (npr. stanje $s=\{s_1,s_2\}$ je verjetno stanje sestavljeno iz 2 dejanskih stanj)
- začetno stanje: največkrat ==množica vseh možnih dejanskih stanj==
- ==akcije== verjetnih stanj:
    - $akcije(s)= \bigcup_{s_i\in s}akcije(s_i)$: preprosto, vendar lahko pripelje do neveljavnih stanj (če je akcija možna le za 1 od 2 stanj)
    - $akcije(s)= \bigcap_{s_i\in s}akcije(s_i)$: bolj varno - razvito stanje vsebuje le stanja, ki so možen rezultat vseh akcij
- prehodna funkcija: $rezultat(s,a)=\{s_j; \ s_j=rezultat(s_i,a), \ s_i\in s\}$
- ciljno stanje: verjetno stanje, v katerem vsa dejanska stanja izpolnjujejo ciljni predikat
# Igranje iger
Preiskovanje prostora med 2 nasprotnikoma - ==več-agentno== tekmovalno okolje, kjer mora agent ==upoštevati vpliv akcij drugega agenta== na svojo uspešnost
Cilj: strategija predvidevanja akcije za vsako možno potezo nasprotnika
### Algoritem MINIMAX
Predstavitev poteka igre: ==igralno drevo potez== igralcev MAX in MIN vsebuje podmožico vseh možnih stanj igralnega drevesa, ki razkriva dovolj informacije za izvedbo poteze (problem velikega prostora stanj)
![[Lokalno preiskovanje, iskanje brez informacije o stanju, igranje iger-Image-1.png|400]]
Stanja vrednostimo s kriterijsko funkcijo - pozitivne vrednosti ugodne za MAX, negativne za MIN
- ==konstantna vsota== kriterijske funkcije (zero-sum): vsota vrednosti kriterijskih funkcij za oba igralca je zmeraj enaka
- ==spremenljiva vsota== kriterijske funkcije
MAX kriterijsko funkcijo zvišuje, MIN jo znižuje:
$$
MINIMAX(v)=\left\{
	\begin{array}{ll}
		kriterijska\ funkcija &;\ v\ je\ končno\ stanje \\
		max_{a\in akcija(v)} MINIMAX(rezultat(v,a)) &;\ igralec\ MAX \\
		min_{a\in akcija(v)} MINIMAX(rezultat(v,a)) &;\ igralec\ MIN
	\end{array}
\right.
$$

Popolnost: da, če je prostor stanj končen
==Optimalnost: da, če nasprotnik igra optimalno==
Časovna zahtevnost: $O(b^m)$
Prostorska zahtevnost: $O(bm)$ / $O(m)$ - iskanje v globino
### Rezanje alfa-beta
==Ne upoštevamo vej, ki ne vplivajo na končno vrednost== $\rightarrow$ ni nam potrebno upoštevati celotnega prostora stanj (pridobimo pomnilnik za nadaljnje preiskovanje obetavnih poddreves v globino)
- $\alpha$: najboljša do sedaj najdena rešitev vozlišča MAX (najvišji že najdeni maksimum)
- $\beta$: najboljša do sedaj najdena rešitev vozlišča MIN (najnižji že najdeni minimum)
Algoritem:
- začetno vozlišče: $[\alpha,\beta]=[-\infty,\infty]$
- na vsakem koraku prenašamo $[\alpha,\beta]$ v globino
- ob vračanju posodabljamo $[\alpha,\beta]$ glede na najdene vrednosti - MAX posodablja le $\alpha$, MIN le $\beta$
- v nekem vozlišču $\alpha\geq\beta$ $\rightarrow$ prekinemo preiskovanje ostalih poddreves
Časovno zahtevnost znižamo na $O(b^\frac m2)$ (možna globina preiskovanja se podvoji)