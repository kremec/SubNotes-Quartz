Motivacija: porazdeljena shramba, odjemalci vanjo pišejo in iz nje berejo (branje istih podatkov ne glede na proces) $\rightarrow$ zanesljivost storitev, razetgljivost / odzivnost sistema
Implementacija: en/več procesov, ki soglašajo o stanju shrambe (dovolj že, če soglaša večina procesov)
Izziv: zagotoviti skladnost replik kljub napakam - izpadom omrežja in procesov
Rešitev: več kopij istega procesa avtomata (DKA) $\rightarrow$ odpornost na $f$ napak:
- zaustavitev ob napaki - potrebujemo vsaj $f+1$ končnih avtomatov
- ne zaustavi ob napaki - potrebujemo vsaj $2f+1$ končnih avtomatov
## Verižna replikacija
### Podatkovna ravnina (data plane)
Procesi, ki skrbijo za replikacijo
![[Replikacija podatkov-Image-1.png|400]]
### Nadzorna ravnina (control plane)
Procesi, ki skrbijo za odpornost na napake
Odpoved glave: zamenja z naslednjim procesom, obvesti odjemalce
- Glava pred odpovedjo posodobila svojo shrambo, a ni uspela poslati sporočila $\rightarrow$ naslednji procesi niso poslali potrditve $\rightarrow$ odjemalec ne dobi potrditve $\rightarrow$ ponovno pošlje zahtevo

Odpoved repa: zamenja s predhodnim procesom, obvesti odjemalce
- Rep odpove po posodobitvi shambe in pred pošiljanjem spremembe $\rightarrow$ zapisi v vseh hrambah že shranjeni, a ni potrditev $\rightarrow$ ponovno pošlje zahtevo

Odpoved vmesnega procesa: poveže predhodnika in naslednika
- Odpoved po posodobitvi shrambe in pred pošiljanjem spremembe $\rightarrow$ predhodnik nasledniku pošlje vse od zadnje potrjene zahteve / spremembe
#### Optimizacija
Branje porazdelimo na vse procese - nepotrjene zapise označimo kot umazane:
- branje zadnjega zapisa, ki je čist $\rightarrow$ proces vrne zapis
- branje zadnjega zapisa, ki je umazan $\rightarrow$ proces prosi rep za zadnjo potrjeno verzijo

Pisanje na glavo vzporedimo - glava ne čaka na posamezno potrditev, sprejema več zahtev naenkrat
## Replikacija z voditeljem (Raft)
Model popolnoma urejenega razširjanja FIFO, predpostavlja obnovljive procese in izgube sporočil
2 končna avtomata: procesi (možna stanja: sledilec / kandidat / voditelj), shramba (vhodi: operacije nad shrambo)
Dnevnik zapisov - operacij nad bazo: če na vsaki shrambi operacije izvedemo v enakem vrstnem redu, bo končno stanje vseh shramb enako
### Delovanje - volitve
Ob zagonu vsi procesi v stanju sledilec
#### Sledilec
- od voditelja pričakuje obvestila popravkov dnevnika in srčni utrip
- sporočila v določenem času ne dobi $\rightarrow$ predvideva smrt voditelja, postane kandidat
#### Kandidat
- začne novo volilno obdobje (term) - monotono oštevilčena, ostalim procesom pošlje `voteRequest`
- večina procesov glasuje zanj $\rightarrow$ postane voditelj
- od drugega procesa (voditelja) dobi sporočilo $\rightarrow$ vrne se v stanje sledilca
- neuspešne volitve (noben kandidat ne dobi večine glasov) se ponovijo
#### Voditelj
- najprej pošlje zapis NOP
- pošiljanje zahtev za dopolnitev dnevnika `appendEntry`: oznaka voditelja, št. obdobja izvolitve, št. zapisov v dnevniku
- zahtev ni $\rightarrow$ srčni utrip
- glavni ostane do odstopa / dokler ne postane nedostopen
<br>
### Delovanje - replikacija dnevnika
Dnevnik: urejen seznam zapisov, ki vključujejo
- operacijo nad shrambo
- oznako voditelja
- št. trenutnega obdobja + št. zapisa v dnevniku
- predhodni zapis: št. obdobja + št. zapisa

Vsak proces gradi svoj dnevnik iz prejetih sporočil, soglasno usklajene zapise uporabi za posodobitev svoje shrambe.

1. Odjemalec pošlje voditelju zahtevo za operacijo nad shrambo
2. Voditelj ustvarjen dnevniški zapis pošlje sledilcem
    - nov zapis lahko pošlje v potrjevanje šele po potrditvi zadnjega zapisa
3. Sledilec zapis doda v svoj dnevnik in voditelju potrdi sprejem
4. Ko voditelj prejme večino potrditev, zapis potrdi in izvede operacijo na svoji shrambi
5. Voditelj potrditev sporoči sledilcem ob razširjanju naslednjega zapisa / srčnega utripa (povečanje številke zapisa)
6. Sledilec ob prejemu novega sporočila potrdi svoj zapis in izvede operacijo na svoji shrambi
### Spremembe sistema
Posodabljanje praznega dnevnika (nov proces) počasno $\rightarrow$ občasno naredimo snapshot shrambe in v dnevnikih vse potrjene (upoštevane) zapise izbrišemo
## Verižna replikacija vs replikacija z voditeljem

|                 | Verižna replikacija                                                           | Replikacija z voditeljem                              |
| --------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------- |
| Pisalna zahteva | po verigi do repa in nazaj                                                    | zahtevo potrdi večina procesov $\rightarrow$ hitrejše |
| Bralna zahteva  | rep usklajen z vsemi procesi in lahko odgovori takoj $\rightarrow$ odzivnejše | mora potrditi, če je še voditelj                      |
| Odpoved procesa | nadzorna ravnia mora odpoved zaznati in spremeniti verigo                     | ne vpliva na obdelavo zahteve                         |
## Modeli skladnosti
Porazdeljevanje bralnih zahtev med procese $\rightarrow$ odzivnejše, a problem neusklajenosti shramb
### Stroga skladnost
Pisanja in branja potekajo izključno preko voditelja; a počasno
### Zaporedna skladnost
Branja lahko stežejo tudi sledilci; a vsak proces lahko hrani drugačno stanje od ostalih procesov
### Končna skladnost
Odjemalcu dovolimo komunikacijo s katerimkoli procesom, po koncu vpisovanj v shrambo se končno stanje shrambe med procesi poenoti
## Teorem CAP
==Teorem CAP==: zagotovimo lahko največ 2 od 3: skladnost, dostopnost, razdelitev omrežja
- zaradi težav v omrežju izbiramo med skladnostjo ali dostopnostjo $\rightarrow$ večja, kot je zahteva za skladnost, daljši so odzivni časi

==Teorem PACELC==: network partitioning, availability, consistency; else latency, consistency
- vedno gre za tehtanje med stopnjo skladnosti (zahteva koordinacijo med procesi) in učinkovitostjo delovanja
## Replikacija brez sporov
Istočasna ne-monotona sprememba iste vrednosti s strani več replik prinese nedefinirano stanje:
![[Replikacija podatkov-Image-2.png|300]]
Monotone operacije se temu izognejo:
![[Replikacija podatkov-Image-3.png|300]]