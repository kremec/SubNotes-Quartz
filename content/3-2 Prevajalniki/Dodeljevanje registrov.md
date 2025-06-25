Vhod: zaporedje strojnih ukazov z začasnimi spremenljivkami + interferenčni graf spemenljivk
Izhod: zaporedje strojnih ukazov z registri

Dodeljevanje registrov ~ barvanje interferenčnega grafa
Faze dodeljevanja registrov (za $k$ registrov):
1. ==Build==: Gradnja interferenčnega grafa
   ==Neortogonalni registri==: "umetna" vozlišča registrov, spremenljivke povežemo s prepovedanimi (da ne morejo biti dodeljena vanje)
2. ==Simplify==: Umik ne-MOVE vozlišč z < $k$ sosedi na sklad (graf čim bolj zmanjšujemo)
3. ==Coalesce==: Združitev MOVE vozlišča v en register na sklad (če obstaja / če možno) $\rightarrow$ ==simplify==
4. ==Freeze==: Izbris izbrane MOVE povezave (če obstaja) $\rightarrow$ ==simplify==
5. ==Potential spill==: Umik vozlišča (npr. z največ povezavami) na sklad z označbo za "morebitni preliv" (skupaj z vozliščem izginejo tudi njegove povezave $\rightarrow$ drugim vozliščem se stopnje znižajo $\rightarrow$ kaka vozlišča imajo lahko spet < $k$ sosedov) $\rightarrow$ ==simplify==
6. ==Dodeljevanje registrov==: Premik vozlišč s sklada na graf, neoznačena vozlišča se zagotovo da pobarvati, označena le mogoče:
	- Vozlišče se da pobarvati $\rightarrow$ barvanje
	- Vozlišča se ne da pobarvati $\rightarrow$ barvanje z naključno/transparentno barvo in umestitev med "dejanske prelive"
	
	Če obstajajo "dejanski prelivi":
	- popravek strojne kode: shranitev spremenljivke v klicnem zapisu namesto v registru
	- ponovitev vseh faz analize aktivnosti registrov in dodeljevanja registrov
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

>[!example] Dokaz s primerom
>Cel graf $G$, $G'$ ... sosedi vozlišča $a$ s stopnjo < $k$:
>![[Dodeljevanje registrov-Image-4.png|330]]
>$G'$ takoj odstranimo (stopnje < $k$) $\rightarrow$ ostane graf $G-G'$
>- Če $a$ in $b$ ne združimo: $G-G'$ se lahko pobarva s $k$ barvami
>  ![[Dodeljevanje registrov-Image-5.png|240]]
>- Če $a$ in $b$ združimo: $G-G'-\{a\}$ se tudi lahko pobarva s $k$ barvami
>  ![[Dodeljevanje registrov-Image-6.png|200]]