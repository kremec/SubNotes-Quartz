==Sočasnost (concurrency)==: prekrivanje obstoja (in občutek hkratnega izvajanja) več procesov
==Vzporednost (parallelism)==: dejansko hkratno izvajanje več procesov (na več procesorjih)
==Porazdeljenost (distribution)==: izvajanje več procesov v več vozliščih omrežja

- ==Sočasnost brez vzporednosti==: večopravilnost - prepletanje izvajanja ukazov
- ==Sočasnost z vzporednostjo==: prekrivanje izvajanja ukazov (večprocesorski sistem)
- ==Vzporednost brez sočasnosti==: vzporednost na nivoju ukazov

Težave: deljenje globalnih virov, smrtni objem, ...

Odnosi med procesi:
- ==tekmovalnost==: procesi ne vedo drug za drugega $\rightarrow$ tekmovanje za vire
- ==sodelovanje==: medprocesna komunikacija ali deljeni viri
### Sočasno izvajanje ukazov
==Prepletanje izvajanja - multiprogramiranje==: en procesor za več procesov
Izvedba ukazov različnih procesov se poljubno prepleta - razvrščevalnik določi vrstni red izvajanja niti
==Prekrivanje izvajanja - multiprocesiranje==: več procesorjev za več pocesov
Izvedba ukazov različnih procesov se poljubno prekriva
### Souporaba vira
Sočasna uporaba vira s strani več procesov $\rightarrow$ lahko pride do nepričakovanih vrednosti vira (odvisna od konkretne arhitekture procesorja, prevajalnika, ...)

==Tvegano stanje (race condition)==: rezultat souporabeskupnega vira je odvisen od prepletanja izvajajočih se ukazov

==Krtični odsek (critical section)==: del programske kode, kjer se sočasno uporablja skupni vir (lahko vodi v tvegano stanje)

==Vzajemno izključevanje (mutual exclusion)==: zagotovilo, da se znotraj KO sočasno nahaja največ 1 proces - vstop v KO je možen le, če ni noben drug proces v njem
### Izzivi kritičnih odsekov
==Stradanje (starvation)==: proces, ki želi vstopiti v KO, ne pride na vrsto (zaradi prioritet)
==Staranje==: procesom, ki ne dobijo vira, vsake toliko časa povečamo prioriteto

==Smrtni objem (deadlock)==: procesi ne morejo nadaljevati izvajanja, ker ciklično čakajo drug na drugega
- Zaznavanje: ignoriranje (npr. Unix, Windows)
- Reševanje: ukinjanje nekega procesa v ciklu / obnavljanje stanja (rollback) / ...