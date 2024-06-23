### Ključavnica
Osnovni mehanizem za zagotavljanje **vzajemnega izključevanja**

Poskus 1: lock kot spremenljivka, katere vrednost lahko v zanki preverjaš dokler se ne odpre
Težave: sočasnost preverjanja stanja ključavnice

==Atomarna operacija==:
- ==zaporedje enega ali več ukazov== se izvede kot celota, ali pa se sploh ne izvede
- ==izolacija od drugih sočasnih procesov== - noben drug proces ne more prekiniti operacije in imeti vpogleda v vmesno stanje
- ==vzajemno izključevanje== - izvede se le ena naenkrat
- ==obvoz medpomnilnika==

Težava: strojni ukazi navadno niso atomično - kako jo zagotoviti?
### Strojna izvedba
==Onemogočanje prekinitev==: vstop v KO - onemogočimo prekinitve, ob izstopu jih nazaj omogočimo
Težave: onemogoči večopravilnost (ko se zacikla KO se zacikla cel sistem), ne deluje na večprocesorski arhitekturi (na ostalih procesorjih so prekinitve vseeno mogoče)

Namenski strojni ukazi:
- `test & set`:  če je zaklenjeno vrne true, sicer zaklene in vrne false
- `compare & swap`: če je trenutna rednost enaka testni vrednosti zamenj z novo vrednostjo, sicer vrne staro vrednost
- `exchange`: zamenjava dveh vrednosti
- `fetch & add`: poveča vrednost in vrne staro vrednost

Prednosti: delujej na večprocesorskih sistemih, enostavnost, podpirajo več KO
Težave: vrteče čakanje zapravlja procesorski čas, možna stradanje in smrtni objem
### Programska izvedba
==Dekkerjev algoritem==: dva procesa si predajata prednost, vrteče čakanje
![[OS_VzajemnoIzključevanje_Dekker.png|300]]
==Petersonov algoritem==:
![[OS_VzajemnoIzključevanje_Peterson.png|220]]
==Lamportov pekarski algoritem==: za N procesov, princip ožtevilčenih listkov
![[OS_VzajemnoIzključevanje_Lamport.png|550]]
### Učinkovitost ključavnic
==Zakasnitveni čas (latency)==: čas za pridobitev proste ključavnice
==Čakalni čas (delay)==: čas za pridobitev ravnokar sproščene ključavnice
==Tekmovanje (competition)==: promet na vodilu zaradi atomične operacije in zagotavljanja koherentnosti pomnilnika

==Vrteča ključavnica (spinlock)==: porablja procesorski čas za iskanje
Namesto vrtečega čakanja nit blokiramo, in jo zbudimo ob pravem trrenutku