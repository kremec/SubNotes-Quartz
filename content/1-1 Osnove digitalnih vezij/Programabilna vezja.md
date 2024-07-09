Primer: Programmable Logic Array (PAL) - enostavna programabilna logična vezja
### Programabilni elementi
==Programabilni elementi== obdržijo vrednost po izklopu napajanja
Realizirani so lahko npr. kot:
- povezava, ki se jo med programiranjem prekine (podobno varovalki)
- tranzistor s "plavajočimi" vrati, ki so lahko električno nabita (EPROM, EEPROM, ...)
Programabilne elemente povezujemo v matriko - ==programabilno polje==

#### ROM vezje
Povezava 2 matrik - leva stran (IN) je stalna, desna (ALI) pa je programabilna
![[Programabilna vezja-Image-1.png|400]]
#### PAL vezje
Obratno od ROM-a - leva stran je programabilna, desna pa stalna
![[Programabilna vezja-Image-2.png|350]]
#### PAL16L8 vezje
Obsega do 16 vhodov in do 8 izhodov
Logično funkcijo predstavlja 7 disjunktivno povezanih termov 16ih spremenljivk
Realiziramo lahko vsako funkcijo, ki jo v [[Minimizacija preklopnih funkcij#Minimalne normalne oblike|MDNO]] lahko zapišemo z največ 7 termi