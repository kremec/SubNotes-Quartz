### Definicija problema
Problem predstavimo s ==prostorom stanj==:
- vozlišča $\rightarrow$ stanja
- povezave $\rightarrow$ akcije
- pot $\rightarrow$ zaporedje stanj kot posledica akcij
- začetno vozlišče
- eno/več ciljnih vozlišč

Reševanje problema $\rightarrow$ iskanje poti po grafu s preiskovanjem
Rešitev problema $\rightarrow$ zaporedje akcij (pot) od začetnega stanja do ciljnega vozlišča (optimalno z najnižjo ceno poti)
## Preiskovanje
Problem: kombinatorična eksplozija možnih stanj

Razvijanje vozlišča: generiranje naslednikov
Fronta: listi drevesa, ki so kandidati z razvijanje
### Neinformirani preiskovalni algoritmi
==Neinformirano==: razpolaganjo samo z definicijo problema
#### Iskanje v širino (BFS)
Strategija: ==razvij najbolj plitvo== še nerazvito vozlišče - generiramo cel nivo preden se pomakne navzdol
- pomnenje vseh alternativnih poti
- srečevanje že obiskanih vozlišč: cikel / po drugi poti
- detekcija ciljnega vozlišča ko ga generiramo ali ko ga razvijemo (vseeno)

Implementacija: razvita vozlišča v ==FIFO vrsti== za razvijanje
![[Preiskovanje, (ne)informativni preiskovalni algoritmi-Image-1.png|300]]
Učinkovitost:
- popolnost: neuspešen z neskončno širino, sicer zagotavlja najkrajšo rešitev
- optimalnost: da (najkrajša pot brez cen povezav)
- časovna / prostorska zahtevnost: $O(b^d)$ / $O(b^d)$
#### Iskanje v globino (DFS)
Strategija: ==razvij najglobje== še nerazvito vozlišče
Implementacija: naslednike v ==LIFO sklad== za razvijanje
![[Preiskovanje, (ne)informativni preiskovalni algoritmi-Image-2.png|500]]
Učinkovitost:
- popolnost: neuspešen v prostorih z zankami / neskončno globino
- optimalnost: ne
- časovna / prostorska zahtevnost: $O(b^max)$ / $O(b*max)$
##### Iskanje s sestopanjem (backtracing search)
==Namesto vseh naslednikov generiramo samo enega po enega==
##### Iskanje z omejitvijo globine (depth-limited search)
==Vozlišča na mejni globini *m* obravnavamo, kot da nimajo naslednikov==
- premajhna / prevelika meja $\rightarrow$ ne najde rešitve / neoptimalnost
- časovna / prostoska zahtevnost: $O(b^m)$ / $O(b*m)$
#### Iterativno poglabljanje
Optimizacija DFS iskanja z omejitvijo globine: začnemo z nizko mejo, povečujemo za 1 dokler ne najdemo rešitve
![[Preiskovanje, (ne)informativni preiskovalni algoritmi-Image-3.png]]
Učinkovitost:
- popolnost: da - BFS
- optimalnost: da (najkrajša pot brez cen povezav) - BFS
- časovna / prostorska zahtevnost: $O(b^d)$ / $O(b*d)$ - DFS
#### Dvosmerno iskanje
==Vzporedni iskanji od začetnega vozlišča proti cilju in obratno== - upamo na srečanje iskanj v sredini in manjšo časovno zahtevnost $O(b^{\frac d2})$
Implementacija: BFS $\rightarrow$ optimalna rešitev
- problemski prostor redefiniramo na dva koraka v originalnem problemskem prostoru
- tako dobivamo množico novih primerov - od vsakega naslednika do vsakega naslednika cilja
- ko pridemo do iskanja poti do istega vozlišča, sta se iskalni smeri srečali
#### Cenovno-optimalno iskanje
Posplošitev BFS za neenake cene povezav
Strategija: ==razvijanje vozlišča z najmanjšo dosedanjo skupno ceno poti==
- ciljno vozlišče označimo šele, ko je na vrsti za generiranje - sicer mogoče obstaja boljša rešitev po drugi poti

Implementacija: fronta v ==prioritetni vrsti== po skupnih dosedanjih cenah
Učinkovitost:
- popolnost: da (pozitivne cene povezav)
- optimalnost: da
- časovna / prostorska zahtevnost: 
### Informirani preiskovalni algoritmi
==Informirano==: razpolagajo tudi z dodatno informacijo/domenskim znanjem

==Hevristično preiskovanje==: uporabimo oceno obetavnosti vozlišč za doseganje cilja
==Hevristika/hevristična ocena/ocena h/h(n)==: funkcija obetavnosti vozlišča
- nizek $h$ $\rightarrow$ bolj obetavno / visok $h$ $\rightarrow$ manj obetavno

Implementacija: vozlišča v prioritetni vrsti (po oceni $h$)

Merjenje kakovosti:
- št. generiranih vozlišč
- efektivni faktor vejanja = št. generiranih vozlišč po globinah za odkritje rešitve
#### Požrešno iskanje
Strategija: ravij ==najbolj obetavno== vozlišče (glede na $h$ oceno)
- cenilna funkcija (za vsako vozlišče): $f(n)=h(n)$

Popolnost: ne (možnost ciklov)
Optimalnost: ne
Časovna/prostorska zahtevnost: $O(b^{max})$
#### A*
Strategija: ==izboljšava funkcije vrednotenja== - $f(n)=g(n)+h(n)$
- $g(n)$ ... znana cena poti do n
- ponovno generiramo vozlišča, če je manjši $g(n)$ - smo našli hitrejšo pot do tistega vozlišča

Implementacija: fronta v prioritetni vrsti

Popolnost in optimalnost: da, če ustreza ==pogoju dopustnosti==: idealno je $h(n)$ čim bližje dejanski ceni optimalne poti, a ==je ne sme presegati== - zmeraj je manjša od dejanske poti do cilja
Časovna zahtevnost: odvisna od kakovosti hevristike - $O(b^{f(\epsilon)*d})$ ;  $\epsilon$ ... relativna napaka hevristike
Prostorska zahtevnost: vsa vozlišča hranimo v spominu $\rightarrow$ problem
#### IDA* (Iterative-Deepening A*)
Strategija: ==[[Preiskovanje#Iterativno poglabljanje|iterativno poglabljanje]] z mejo $f(n)$ namesto globine==
- na vsaki iteraciji razvijemo vsa vozlišča z $f(n)\lt$ mejna vrednost $\rightarrow$ $meja=min f(n)$ še nerazvitih vozlišč

Razvijanje mora potekati v prioritetnem vrstnem redu - razviti mora najmanjše potrebno št. vozlišč:
- $h(n)$ mora biti ==monotona/konsistentna==: $h(n)\lt c(n,n')+h(n')$, $h(g)=0$ za vsako končno vozlišče
  Poenostavitev: cenilna funkcija $f(n)\lt f(n')$ oz. dopustna + pada glede na dejanske cene povezav

Učinkovitost: redundanca - ponovno generiranje veliko vozlišč, neučinkovit če imajo vozlišča veliko različnih $f(n)$ - veliko iteracij skozi vse meje
Prostorska zahtevnost: v pomnilniku mora hraniti le trenutno pot, ne vseh vozlišč
### Kakovost hevrističnih funkcij
Kakovost $h$ lahko ocenimo:
- št. generiranih vozlišč
- efektivni faktor vejanja = št. generiranih vozlišč po globinah za odkritje rešitve

Oboje želimo minimizirati

==Relaksacija modela==: ignorira nekatera pravila igre za lažjo oceno stanja ($h$)
## Lokalni preiskovalni algoritmi
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
## Preiskovanje brez informacije o stanju
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
## Igranje iger
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