Življenjska pot programa:
![[Povezovalnik-Image-1.png|350]]
Povezovalnik in nalagalnik lahko združimo v en program: preprosteje, a je potrebno pred izvajanjem (nalaganjem) zmeraj znova povezati - počasno
## Povezovalnik
Vhod: en/več vhodnih objektnih modulov
Izhod:
- ==izhodni objektni modul==: združi vhodne module $\rightarrow$ razrešene vse medsebojne reference
- ==absolutno izvedljivi modul==: nalaganje na vnaprej znano lokacijo $\rightarrow$ razrešene vse prenaslovitve
- ==prenosljivi izvedljivi modul==: razreši vse zunanje reference, vse prenaslovljive sekcije združi, ustvari nove prenaslovitvene zapise
### Povezovanje
Predpostavimo: začetni nalagalni naslov = 0
Relativnim naslovom (kasneje relativni glede na končni nalagalni naslov) dodamo prilagoditvene zapise
Pri branju kontrolnih sekcij povezovalnik še ne pozna naslova zunanjih referenc $\rightarrow$ 2 prehoda:
#### 1. prehod
Določanje naslovov kontrolnih sekcij in zunanjih simbolov
- lahko obravnavamo le zapise H in D

Povezovani tabeli:
- ==tabela razdelitev pomnilnika (CSTAB)==: ime, naslov, dolžina
- ==tabela zunanjih simbolov (ESTAB)==: ime sekcije, ime simbola, vrednost - naslov znotraj sekcije

Shranimo vrednosti:
- `PROGNAME`: ime programa
- `PROGLEN`: dolžina celotnega programa
- `STARTADDR`: naslov prvega izvršljivega ukaza
#### 2. prehod
Prenaslavljanje vseh direktnih naslovov, tvorjenje tabele novih prilagoditvenih zapisov
Popravljanje direktnih naslovov upošteva:
- nalagalni naslov sekcije
- vrednosti zunanjih simbolov

Tvorba tabele NEWMODREC:
- popravi imena zunanjih simbolov
- popravi naslove - `naslov += nalagalni naslov kontrolne sekcije`
- medseboj izničujoči zapisi se ne zapišejo v novo tabelo