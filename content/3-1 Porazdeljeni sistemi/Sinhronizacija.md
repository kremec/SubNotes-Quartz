Komunikacija gorutin preko skupnega pomnilnika $\rightarrow$ istočasen dostop do iste spremenljivke $\rightarrow$ nepredvidljivo delovanje
### Tvegano stanje in kritični odsek
==Tvegano stanje== (race condition): 2 ali več operaciji želimo izvesti v pravem vrstnem redu, program pa tega ne zagotavlja
==Kritični odsek==: del kode, ki ga sme izvajati le ena gorutina naenkrat - gorutina ne sme vstopiti vanj, dokler se v njem nahaja že druga gorutina
### Tipi zastojev v programu
- ==smrtni objem== (deadlock)
- ==živi objem== (livelock): gorutini neprestano ponavljata nesmiselno operacijo kot odgovor na spremembe v drugi gorutini
- ==stradanje==: gorutina ne more pridobiti virov, ker jih druge bolj intenzivno urporabljajo
### Ključavnice
==Ključavnice== (mutex ~ MUTual EXclusion): zaklepamo dostop do kritičnega odseka, da je v njem največ 1 gorutina
- implementacija: pomnilniška beseda z binarno vrednostjo
- branje, nastavljanje in zaklepanje mora biti atomarna operacija

Gorutina pred vstopom v kritični odsek preveri stanje ključavnice:
- odklenjena $\rightarrow$ zaklene in vstopi
- zaklenjena $\rightarrow$ čaka dokler se ne odklene

Ob izstopu odklene ključavnico da omogoči vstop drugim gorutinam
#### Atomarne / nedeljive operacije
==Atomarnost==: operacije ne moremo razdeliti na manjše dele ali prekiniti
Določiti moramo obseg atomarnosti, s tem da takih obsegov želimo čim manj
#### Podpora ključavnic v procesorjih
Posebni atomarni ukazi večjedrnih procesorjev:
- ==TAS (test-and-set) - preveri in nastavi==: atomarno vrne staro vrednost bita in nastavi njegovo vrednost na 1
  stara vrednost 0 $\rightarrow$ nadaljuje, stara vrednost 1 $\rightarrow$ nastavi ključavnico in ponovno poskuša
- ==CAS (compare-and-swap) - primerjaj in zamenjaj==: primerja trenutno vrednost na pomn. lokaciji in pričakovano vrednost
  vrednosti enaki $\rightarrow$ trenutno vrednost nastavi na novo vrednost
- ==FAA (fetch-and-add) - prevzemi in dodaj==: vrne staro vrednost in na pomn. naslovu vrednost atomarno poveča
  atomarna operacija $\rightarrow$ stara vrednost dodeljena niti

Implementacija: zaklepanje pomn. vodila / rešitev v pomnilniku
#### Hkratna uporaba več ključavnic in smrtni objem
Do ==smrtnega objema== (deadlock) pride, če so izpolnjeni vsi ==Coffmanovi pogoji==:
- viri (kritični odseki) imajo omejeno število lastnikov (gorutin)
- lastnik lahko pridobi en vir in čaka na naslednji vir
- lastnik ima izključno pravico do sproščanja vira
- obstaja krožna odvisnost med lastniki (1. čaka na 2., 2. na 3., ..., zadnji spet na 1.)

Preprečevanje smrtnega objema:
- ==hierarhija ključavnic - statično==: določimo oštevilčen vrstni red ključavnic, po katerem jih zmeraj zaklepamo (npr. ne zaključi ključavnice `n`, če je ključavnica `m` zaklenjena in `n<m`)
- ==pogojno zaklepanje - dinamično==: zaklenemo prvo ključavnico in poskusimo zakleniti še ostale, če katere ne uspemo zakleniti sprostimo vse in poskusimo ponovno od začetka
### Semaforji
Števna struktura z vrednostjo $\ge 0$ (ključavnica je le binarna)
Atomarne operacije:
- poskusi vstopiti: vrednost $\gt 0$ $\rightarrow$ vstop in zmanjšaj vrednost za 1
- sprosti: izstop $\rightarrow$ povečaj vrednost za 1
### Bralno-pisalne ključavnice
Zaklep za branje: možen vstop bralnih gorutin, pisalne gorutine ne morejo vstopiti
Zaklep za pisanje: možen vstop le eni pisalni gorutini, bralne gorutine ne morejo vstopiti
<br><br>
### Pogojne spremenljivke / pregrade
Uporaba: sinhrona zaustavitev in ponovni zagon gorutin glede na stanje pripadajoče ključavnice
Delovanje:
1. Gorutina zaklene ključavnico
2. `Wait()`$\rightarrow$ ključavnico sprosti in v vrsti čaka na signal za nadaljevanje
3. Signal za nadaljevanje $\rightarrow$ zbuditev in nadaljevanje
   `signal`$\rightarrow$ zbudimo eno spečo gorutino / `broadcast`$\rightarrow$ zbudimo vse speče gorutine
4. Gorutina sprosti ključavnico

(z `WaitGroup` moramo vsakič ustvariti nove gorutine)