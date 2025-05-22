## Izjeme
Funkcijo, ki uporablja `try-catch` se označi s tipi izjem, ki jih lahko lovi
Ob `try` shranimo kontekst (registre) in PC za `throw` del
Ob `throw` po klicnem skladu odvijamo vse klicne zapise do prve funkcije, ki zna uloviti določeno izjemo
![[(Dodatne funkcionalnosti)-Image-1.png|400]]
## Avtomatsko čiščenje pomnilnika
### Štetje referenc (reference counting)
Vodimo skrite števce števila referenc za dan podatek na kopici
Vsakič ko kazalec ustvarim / uničim / spremenim: potreben dostop do kopice za popravljanje števcev
- ob odštevanju: števec ima vrednost 0 $\rightarrow$ odstrani podatek

>[!example] Primer
>![[(Dodatne funkcionalnosti)-Image-2.png|150]]
>`int *p = NULL`
>1. `p = malloc(sizeof(int))`
>2. `int *q = p`
>3. `p = NULL`

Problem: ciklični kazalci
>[!example] Primer
>![[(Dodatne funkcionalnosti)-Image-3.png|330]]
#### Metapodatki
Vsak dinamično dodeljen blok pomnilnika ima skrite metapodatke (npr. velikost bloka - koliko pomnilnika ob čiščenju sprostimo, ...)
Števec referenc dodamo v metapodatke

V razvojnem okolju dinamično dodeljevanje pomnilnika poleg metapodatkov doda še vzorec ničel in enic pred in za dejanske podatke $\rightarrow$ ob sprostitvi preveri za spremembe v vzorcu, ki pomenijo prepis pomnilnika čez meje dejanskih mej podatkov (napaka programerja)
### Označi in pometi (mark and sweep)
1. Poišči vse dosegljive kazalce (med statičnimi spremenljivkami, na skladu, v registrih, ...)
2. Rekurzivno označi vse dinamično dodeljene bloke na kopici, ki so dosegljivi preko teh kazalcev
3. Kar ni označeno lahko pobrišemo

Problema s cikličnimi kazalci tukaj ni več, ker ni več zunanjega kazalca na ciklične kazalce se ti pobrišejo
Problem: izvajanje programa se ob pometanju ustavi, kar omejuje odzivnost (interaktivnih) programov
##### Arena
Večji kos celega prostega pomnilnika, v katerem se ob določeni zasedenosti vsi porabljeni bloki prekopirajo v nasledjo areno (in se zložijo skupaj - brez vmesnega nezasedenega prostora)
To omogoča enostavnejši algoritem za `malloc` in `free`, ki se ne ukvarjata z luknjami med bloki
##### Generacije
Manjši kos celega prostega pomnilnika, ki ga po določenem časovnem obdobju stisnemo in nato nikoli več ne popravljamo
To omogoča krajša prepisovanja, saj s tem pristopom ciljamo, da podatke na kopici, ki preživijo tam določen časovni interval, ne bodo tako hitro zbrisani
#### Metapodatki
Shranjevanje korenov dostopov (kazalcev) dinamično dodeljenih blokov:
- spremenljivke, ki so kazalci - statične (na fiksnem pomn. naslovu) / avtomatske (na skladu)
- registri - aktivni v procesorju / shranjeni (na skladu)
- klicni zapis

Vsak dinamično dodeljen blok, ki predstavlja objekt, ima shranjene metapodatke:
- tabela navideznih funkcij
- refleksija - preverjanje tipa objekta v času izvajanja
- informacije o kazalcih za tip objekta (glede na strukturo objekta - opis razreda)