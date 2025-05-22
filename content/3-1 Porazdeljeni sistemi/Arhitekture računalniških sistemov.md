==Moorov zakon==: št. tranzistorjev se vsaki 2 leti podvoji
Dennardovo pravilo: zmanjšanje velikosti tranzistorja omogoči več tranzistorjev
### Enojedrna zasnova / von Neumann
![[Arhitekture računalniških sistemov-Image-1.png|300]]
Zaporedno izvajanje: prevzem ukaza - dekodiranje - prevzem operandov - izvajanje - shranjevanje
#### Pomnilniška hierarhija
1. Registri
2. ==Predpomnilnik==:
    - večnivojski (L1 = ukazi + podatki, L2 in L3 = podatki)
    - organiziran v bloke (enota prenosov)
    - direktni / asociativni / set-asociativni
    - pisanje skozi / pisanje nazaj
3. Glavni pomnilnik: 100x počasnejši dostop kot registri
4. Navidezni pomnilnik: razširitev na disku, organiziran v strani

Kopica: dinamično dodeljevanje pomnilnika
Sklad: LIFO, shranjujemo kontekst ob klicih funkcij - povratni naslov, lokalne spremenljivke, ...
#### Vzporedenje v strojni opremi
- Cevovod - stopnje z enako kompleksnostjo
- Vektorski ukazi - hkratno izvajanje ukaza na več operandih
- Špekulativno izvajanje - med preverjanjem pogoja izvajamo ukaze, ki mu najverjetneje sledijo
- Superskalarnost - vzporedno izvajanje neodvisnih ukazov
- Strojne niti - hkratno izvajanje različnih programskih tokov
#### Omejitve
- ==pregrevanje čipa== - 130W na jedro
- prepustnost pomnilnika - procesor čaka na podatke
- ostale optimizacije strojnega vzporejanja že implementiranje
### Večjedrne arhitekture
Omogočajo:
- ohranjanje Moorovega zakona
- ==energetsko učinkovitost== - opravimo več z manj moči

Marsikdaj avtomatiski paralelizem (optimizacije procesorja) ni učinkovit $\rightarrow$ programi morajo biti zasnovani z vzporednostjo v mislih
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
### Sistemi s skupnim pomnilnikom
Procesorji si delijo skupni pomnilnik (enovit naslovni prostor) in L2 ter L3 predpomnilnika $\rightarrow$ ==spremembe v pomnilniku vidijo vsi procesorji==
Problem skladnosti: podatki v L1 predpomnilnikih se lahko razlikujejo
#### Unified Memory Architecture (UMA)
![[Arhitekture računalniških sistemov-Image-2.png|250]]
Enak dostopni čas do pomnilnika za vsa jedra
Zagotavljanje skladnosti:
- vohljanje: preverjanje in popravljanje ostalih predpomnilnikov + pisanje skozi
- direktorijski protokoli (npr. MESI)
#### Non-Unified Memory Architecture
![[Arhitekture računalniških sistemov-Image-3.png|400]]
Dostopni čas procesorja do neposredno povezanih pomnilniških modulov krajši, do ostalih 2-3x daljši $\rightarrow$ čim več dela s pomnilnikom svoje domene
Zagotavljanje skladnosti: direktoriji za vodenje stanj blokov predpomnilnikov
- U(ncached) - pomnilniški blok ni uporabljen na nobenem predpomnilniku
- S(hared) - zapis uporabljen v večih predpomnilnikih, možno le branje
- E(xclusive) - zapis v enem predpomnilniku, ki ima pravo vrednost
### Sistemi s porazdeljenim pomnilnikom
![[Arhitekture računalniških sistemov-Image-4.png|200]]
Vsak procesor lahko neposredno dostopa le do enovitega pomnilnika na svojem vozlišču
Vrste:
- gruče: na vsakem vozlišču svoj OS
- masivno vzporedni procesorji: en OS za vsa vozlišča
- ozvezdja: št. procesorskih jeder enega vozlišča > št. vozlišč
