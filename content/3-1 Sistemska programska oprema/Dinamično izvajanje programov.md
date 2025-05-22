### Vmesna koda
==Vmesno kodo== izvajamo na poljubnem sistemu znotraj ==navideznega izvajalnega okolja== s tolmačem (interpreterjem)
Prednosti: varnost, majhno št. prevajalnikov, prenosljivost
Slabost: počasnejše delovanje
# Java arhitektura
## Java tolmač
Implementacije:
- ==tolmačenje vsakič znova==: preprosto, a počasno
- ==sprotno prevajanje== (Just-In-Time): hitro izvajanje, a velika poraba pomnilnika
  Ob prvem klicu metode se koda prevede, optimizira in shrani za nadaljnje klice
- ==prilagodljivo optimiranje==: Naložena koda se sproti tolmači, le največkrat klicane metode se prevede v strojni jezik in optimizira
#### Življenjski cikel
1. Prevajanje v ==zložno kodo (bytecode)==
2. Nalaganje razredov na poljubno lokacijo - vsa sklicevanja potekajo preko simboličnih imen (prenaslavljanje ni potrebno)
3. Povezovanje ~ razreševanje simboličnih imen v absolutne naslove
    - ==zgodnje razreševanje==: vnaprejšnje razreševanje vseh konstant
    - ==pozno razreševanje==: vsako sklicevanje se razreši v trenutku uporabe
    - ==vmesno razreševanje==: delno razreševanje ob nalaganju, delno ob izvajanju
## Razredne zbirke
==Razredna zbirka==: standardiziran zapis prevedene kode, primerne za nalaganje / povezovanje / izvajanje v JVM
- Hrani podatke v binarni obliki v standardu, ki ga razume vsak JVM
- Namenjena prenosu po omrežju $\rightarrow$ potrebno učinkovito (kompaktno kodiranje)
Osnovni podatek je big-endian 8b zlog
Zbirke imajo vnaprej znane dolžine, zato mora biti podana
### Nabor konstant
==Nabor konstant==: tabela različnih struktur (potrebujemo shranjeno št. konstant pred začetkom zapisov)
- znakovne konstante
- imena razredov, vmesnikov, atributov
Tip konstante podan s prvim zlogom Tag:
![[Dinamično izvajanje programov-Image-1.png|300]]
![[Dinamično izvajanje programov-Image-2.png|300]]
![[Dinamično izvajanje programov-Image-3.png|300]]
## JVM 32
Beseda, registri: 32b
Naslovni prostor: 32b $\rightarrow$ 4GB naslovljivega pomnilnika
### Registri
Za izvajanje operacij JVM uporablja izključno sklad $\rightarrow$ zadoščajo 4 registri:
- PC ... naslov trenutno izvajanjega ukaza
- vars ... kazalec na začetek tabele lokalnih spremenljivk
- optop ... kazalec na vrh operandskega sklada
- frame ... kazalec na trenutni okvir
### Sklad
Hrani parametre, naslove in vmesne rezultate
Vsaka nit dobi svoj sklad, register PC in sklad za native metode
==Okvir== (frame): del sklada, ki se dodeli metodi ob klicu; trenutna metoda uporablja najvišji del (okvir) sklada
- ==Izvajalno okolje==: hrani vrednosti registrov za metodo tega okvirja
  pframe ... kazalec na nad-metodo (povratni naslov)
- ==Operandski sklad==: parametri in rezultati bytecode operacij
  optop kaže na vrh sklada za to nit
- ==Tabela lokalnih spremenljivk==: formalni parameter in lokalne spremenljivke
#### Klic metode
Metoda A kliče metodo B:
1. Ustvari se okvir za metodo B
2. V tabelo lokalnih spremenljivk okvirja B se odložijo parametri
3. Trenutne vrednosti registrov PC, optop in vars shrani v izvajalno okolje okvirja A
4. Trenutno vrednost registra frame shrani v izvajalno okolje okvirja B (pframe)
5. Nastavimo nove vrednosti registrov:
    - optop, vars = B.optop, B.vars
    - PC = naslov prvega ukaza metode B
#### Vrnitev iz metode
Vrnitev iz metode B:
1. Rezultat zapišemo v 0-to lokalno spremenljivko
2. Nastavimo vrednosti registrov:
    - frame = B.frame
    - vars, PC = frame.vars, frame.PC
    - optop = frame.optop++
### Kopica
Ukaz `new` rezervira del kopice in vrne referenco nanj
Sproščanje neuporabljenega rezerviranega pomnilnika opravlja JVM čistilec (garbage collector)
### Področje za metode
Koda (bytecode) vseh razredov in objektov
Vsaka metoda se pojavi samo enkrat (četudi 100 objektov implementira metodo, se dela le na eni verziji te metode preko `this`)
## Izvajanje zložne kode
Javanski program: zaporedje enozložnih operacijskih kod
Ukazi dostopajo do podatkov:
- takojšnje vrednosti v zložni kodi
- lokalne spremenljivke
- vpisi na operacijskem skladu
### Ukazi
3 skupine ukazov:
- 200 splošnonamenskih ukazov
- 3 rezervirani ukazi: `breakpoint` - razhroščevanje, `impdep1` in `impdep2` - ustvarjanje sistemskih klicev in prestreznikov
- 25 hitrih ukazov: nadomestijo "počasne" ukaze po povezovanju