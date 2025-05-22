Vhod: zaporedje kanoničnih dreves posamezne funkcije (za vse funkcije)
Izhod: zaporedje strojnih ukazov z začasnimi spremenljivkami posamezne funkcije (za vse funkcije)

Poddrevesa vmesne kode predstavljajo eno ali več osnovnih operacij, ki jih lahko procesor izvede v enem ali večih ukazih
==Tlakovci==: drevesni vzorci, ki se skladajo s strojnimi ukazi izbrane arhitekture, s katerimi "pokrijemo" poddrevesa
- ukazi, ki rezultat shranijo v register (npr. `ADD`, `SUBI`, `LOAD`)
- ukazi, ki izvajajo stranske učinke na pomnilniku (npr. `STORE`)

Vzorec pravila tlakovca: preslikava poddrevo $\rightarrow$ ukaz + rezultat (vrednost ali naslov)

==Tlakovanje==: "pokrivanje" delov drevesa s tlakovci, ki se ne prekrivajo
Učinkovitost najdene rešitve "pokritja" ocenjujemo: najmanjše število ukazov / najmanjša skupna zahtevnost ukazov / ...
- optimalno pokritje: nobena sosednja ukaza se ne moreta združiti v ukaz z manjšo ceno
- optimum: globalno optimalna razdelitev (ki jo vseeno gradimo na približkih ocen, ki ne morejo upoštevati vseh zapletenih vrst medsebojne interakcije ukazov)
### Algoritem za izbiranje ukazov
Algoritmi za iskanje optimalnih razdelitev so lažji kot algoritmi za iskanje optimumov
- CISC: ukaz izvrši veliko operacij $\rightarrow$ tile-i so veliki $\rightarrow$ razlika med optimalnim pokritjem in optimumom se lahko bolj pozna
- RISC: ukaz izvrši malo operacij $\rightarrow$ tile-i so majhni (primerljiva cena) $\rightarrow$ enostavnejši algoritmi
#### Maximal munch
Algoritem za optimalen tiling, ki generira strojne ukaze v obratnem vrstnem redu (od korena drevesa navzdol)
Od korena drevesa po vseh poddrevesih izbereš največji prilegajoč se tlakovec, nato ponovi za vsa nepokrita poddrevesa

Če za vsako posamezno vozlišče obstaja single-node tile, se tak algoritem ne more "zaplezati" (priti do tega, da noben tile ne bi mogel pokriti poddrevesa)
#### Dinamično programiranje
Dinamično programiranje: tehnika, ki optimum išče na podlagi optimumov vseh podproblemov #TODO-LINKS 

Algoritem za iskanje optimuma, ki generira strojne ukaze v pravilnem vrstnem redu (od listov drevesa navzgor)
Vsakemu vozlišču priredi ceno - cena tile-a na vozlišču + vsota cen zaporedja ukazov, po katerih smo priplezali do danega vozlišča
#### Drevesne gramatike
Generalizacija algoritma dinamičnega programiranja za kompleksnejše arhitekture z veliko ukazi, tipi registrov in načini naslavljanj
Algoritem tako hrani optimume za vse variante in uporabi le potrebne, variante pa najlažje raziskujemo s kontekstno neodvisno gramatiko
### CISC računalniki

|                           | RISC                                                              | CISC                                                            |
| ------------------------- | ----------------------------------------------------------------- | --------------------------------------------------------------- |
| **Število registrov**     | $\geq32$                                                          | $\lt16$                                                         |
| **Tipi registrov**        | Uniform tip registrov                                             | Več tipov registrov, vsak uporabljen za druge naloge            |
| **Aritmetične operacije** | Samo med registri                                                 | Dostop do registrov in/ali pomnilnika preko načinov naslavljanj |
| **Oblika ukazov**         | $r_1\leftarrow r_2\ op\ r_3$                                      | $r_1\leftarrow r_1\ op\ r_2$                                    |
| **Dostop do pomnilnika**  | Preko `load` in `store` ukazov s predpisano obliko $M[reg+const]$ | Različni načini naslavljanja                                    |
| **Dolžina ukazov**        | Vsi ukazi iste dolžine                                            | Različne dolžine ukzaov (opcode, naslov, ...)                   |
| **Učinek**                | En rezultat ali efekt na ukaz                                     | Ukazi imajo stranske učinke                                     |
Slabosti CISCa (npr. določeni tipi registrov, oblika ukazov z dvema registroma, ...) zaobidemo z dodatnimi prenosi vrednostmi med registri (alokator registrov bo moral bolj delati)