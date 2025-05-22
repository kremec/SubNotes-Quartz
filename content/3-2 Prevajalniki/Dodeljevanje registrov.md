Vhod: zaporedje strojnih ukazov z začasnimi spremenljivkami + interferenčni graf spemenljivk
Izhod: zaporedje strojnih ukazov z registri

Barvanje interferenčnega grafa za $k$ registrov:
1. Vozlišča z manj kot $k$ sosedi umaknemo z grafa na sklad (graf čim bolj zmanjšujemo)
2. Vozlišče (npr. z največ povezavami) umaknemo z grafa na sklad in ga označimo za "morebitni preliv" (skupaj z vozliščem umaknemo tudi njegove povezave $\rightarrow$ drugim vozliščem znižamo stopnje $\rightarrow$ morda ima spet kako vozlišče manj kot $k$ povezav)
   (Ponavljamo fazi 1 in 2 dokler ne prestavimo vseh vozlišč na sklad)
3. S sklada prestavimo vozlišče v graf (neoznačena vozlišča se bodo zagotovo dala pobarvati, neoznačena pa le mogoče)
	- Če se vozlišče da pobarvati, ga pobarvamo
	- Če se vozlišča ne da pobarvati, ga pobarvamo (naključno/transparentno) in damo med "dejanske prelive"
4. Če obstajajo "dejanski prelivi", popravim strojno kodo (spremenljivko shranjujem v klicnem zapisu namesto v registru, označimo da ne bomo več mogli obravnavati kot preliv) in ponovim fazi analize aktivnosti registrov in dodeljevanja registrov

Registre iz MOVE ukazov (vrednost le premaknejo iz enega v drug register) poskusimo med barvanjem spraviti v isti register $\rightarrow$ odstranimo te (nepotrebne ukaze)
Nasploh (razen v tem primeru) takih združevanj nočemo:
- pregled parov vozlišč vzame svoj čas
- graf postane gostejši $\rightarrow$ manj svobode pri dodeljevanju registrov
### Algoritmi združevanja MOVE ukazov
#### Osnova
Ne upoštevamo MOVE ukazov
#### Briggs
Vozlišči $A$ in $B$ (povezani v MOVE ukazu) lahko združimo v $AB$, če velja:
- stopnja $AB$ < $k$

Po združitvi se bo še zmeraj zagotovo dalo pobarvati
#### George
Vozlišči $A$ in $B$ (povezani v MOVE ukazu) lahko združimo v $AB$, če za vsakega soseda $T$ od $A$ velja bodisi:
- stopnja $T$ < $k$ (ali)
- $T$ je tudi sosed $B$

>[!example] Primer
>![[Dodeljevanje registrov-Image-1.png]]
### Faze
![[Dodeljevanje registrov-Image-2.png]]

>[!example] Primer
>![[Dodeljevanje registrov-Image-3.png]]

### Možni problemi
#### Neortogonalni registri
Za določene spremenljivke lahko zahtevamo, da se morajo obravnavati le v določenih registrih (npr. določen register za množenje)
Rešitev: uvedba "umentnih" vozlišč inferenčnega grafa, ki predstavljamo registre, potrebne spremenljivke povežemo z vsemi ostalimi vozlišči registrov (zaradi česar ne morejo iti v tiste registre)