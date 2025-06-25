Princip cevovoda:
- vhod: izvorna koda (npr. C/Go/Pascal/...)
- izhod: ciljna koda zbirnika za specifičen procesor (npr. Intel/AMD/RISC-V/...)

Faze zbiranja:
![[Faze prevajalnika-Image-1.png||500]]
1. ==Leksikalna analiza==: zaporedje znakov vhodne datoteke razbijemo v zaporedje ==leksikalnih simbolov==
2. ==Sintaksna analiza==: po preverjanju zaporedja/strukture leksikalnih simbolov zgradi ==drevo izpeljav==
3. ==Abstraktna sintaksa==: poenostavitev drevesa izpeljav v ==abstraktno sintaksno drevo==
4. ==Semantična analiza==: pregled pomena simbolov, povezava uporabe spremenljivk z njihovimi definicijami, preverjanje tipov izrazov, ...
5. ==Izračun klicnih zapisov==: postavitev spremenljivk, parametrov v pomnilnik - sklad ali izven sklada (odvisno od ciljne arhitekture)
6. ==Generacija vmesne kode==: vmesna koda podobna kot strojna koda, a na višjem nivoju
7. ==Osnovni bloki==: linearizacija vmesne kode, že poganjljiva v tolmaču
8. ==Generacija strojne kode==: generacija ukazov za konkreten procesor, brez konkretnih registrov (kot da imamo poljubno št. registrov)
9. ==Analiza registrov==: zbiranje informacij o aktivnosti spremenljivk - registrov
10. ==Dodeljevanje registrov==: dodeljevanje registrov spremenljivkam in drugim vrednostim
11. ==Izpis ciljne kode==: ustvarjanje datotek, za funkcije potrebne oznake za povezovalnik, ...
12. (Zbirnik in povezovalnik)

Sprednji del prevajalnika (1-6): izvorni jezik $\rightarrow$ (znaki $\rightarrow$ drevesa $\rightarrow$) vmesna koda
(Vmesni del: optimizacije vmesne kode)
Zadnji del prevajalnika(6-11): vmesna koda $\rightarrow$ ciljni jezik

Modularnost omogoča spremembo/dodajanje:
- ciljne arhitekture $\rightarrow$ popravi/dodaj fazi Izračun klicnih zapisov ter Generacija strojne kode
- izvornega jezika - popravi/dodaj vse faze do generacije vmesne kode