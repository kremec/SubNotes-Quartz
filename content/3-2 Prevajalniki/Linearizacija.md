Vhod: vmesna koda posamezne funkcije (vseh funkcij)
Izhod: linearizirana vmesna koda posamezne funkcije (vseh funkcij)

==Linearizacija==: priprava vmesne kode za prevod v zbirni jezik in optimizacije
Faze linearizacije: drevo vmesne kode $\rightarrow$ kanonična drevesa $\rightarrow$ osnovni bloki $\rightarrow$ sledovi
### Kanonična drevesa
Vsak stavek vmesne kode posamezne kode lahko obravnavamo posamično
Cilj: standardizacija vozlišč `CALL` in splošna poenostavitev drevesa za naslednje faze
##### Gnezdeni klici funkcij
Starš vsakega vozlišča vmesne kode `CALL` mora biti bodisi:
- `ESTMT`
- `MOVE`, katerega cilj je začasna spremenljivka

>[!example] Primer
>```
>f(g(51), T5+1)
>```
>![[Linearizacija-Image-1.png|300]]
>###### 1. Način
>```
>T751 = g(51)
>T752=f(T751, T5+1)
>return T752
>```
>![[Linearizacija-Image-3.png|600]]
>Končni rezultat:
>![[Linearizacija-Image-4.png|400]]
>Tiha a nevarna predpostavka: `g` ne spreminja `T3` (sicer povozi naslov zapisa rezultata)
>###### 2. način
>Končni rezultat:
>![[Linearizacija-Image-5.png|800]]
>Več vozlišč `MOVE` in začasnih spremenljivk, a varneje (ničesar ne moremo prepisati) in lažje za implementacijo
##### Zaporedja stavkov
Linearizacija vozlišča vmesne kode tipa "seznam stavkov" premika proti vrhu drevesa, da nam na koncu ostane linearen seznam stavkov
##### Stavki s stranskim učinkom
Prav tako vozliščem tipa "stavek s stranskim učinkom" izloči stranske učinke, saj je sicer pri analizi potrebno natančno obravnavati vrstni red izvajanja takih učinkov
### Osnovni bloki in sledovi
==Osnovni blok==: zaporedje stavkov, ki se začne z začetno labelo in konča s (pogojnim) skokom, vmes ne vsebuje label ali (pogojnih) skokov
Razporeditev osnovnih blokov zaradi modularnosti ne vpliva na izvajanje programa

==Sled==: zaporedje stavkov, ki se med izvajanjem programa izvajajo zaporedno
Število različnih sledi in število skokov med njimi želimo minimizirati
Prav tako želimo zaporedja pogosto izvajanih ukazov ohraniti znotraj ene sledi $\rightarrow$ izognemo se nepotrebnim nepogojnim skokom
##### Pogojne vejitve
Vendar večina procesorskih arhitektur podpira le pogojne skoke, ki v primeru negativne vrednosti (`false`) pogoja preprosto nadaljujejo z izvajanjem naslednjega ukaza ("padec skozi") $\rightarrow$ namesto 2 label zahtevamo, da vsakemu pogojnu skoku sledi del kode za negativno vrednost pogoja, s čimer se znebimo enega skočnega ukaza

Problem: 2 bloka v primeru negativnega pogoja zahtevata skok na isti osnovni blok
Rešitev: obrnitev pogoja / pri drugem bloku kot "negativni blok" vstavimo labelo in skok
```
...
CJUMP C, L1, L2'

LABEL L2'
JUMP L2

...
```
##### Nepogojni skoki
Za blok, ki se konča z nepogojnim skokom, postavimo ciljni blok, in se s tem znebimo skočnega ukaza
>[!example] Primer
>```
>CJUMP (T1 == 5), L1, L2
>```
>pretvorimo v
>```
>     JEQ0 T1, L1
>     JUMP L2
>L2: ...
>```
>kjer se ukaza `JUMP L2` lahko znebimo