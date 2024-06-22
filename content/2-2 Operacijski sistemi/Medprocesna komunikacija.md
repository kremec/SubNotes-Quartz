==Medprocesna komunikacija==: nadzorovan mehanizem OS za prenos podatkov med naslovnimi prostori (navadno sočasnih) procesov brez kršenja zaščite
- ==prenašanje sporočil==: vtičnice, cevi, sporočilne vrste, ...
- ==deljeni pomnilnik==: direkten dostop do podatkov
### Prenašanje sporočil
Hitra vzpostavitev - počasna komunikacija (kopiranje podatkov)

Pošiljanje sporočila v kanal, prejem sporočila iz kanala, odgovor na sporočilo (če je potreben)
Operacije so lahko:
- ==sinhrone - blokirajoče==: zmenek - pošiljanje in prejem sta sinhroni
- ==asinhrone - neblokirajoče==: potrebujemo medpomnenje (npr. vrsto) sporočil

Naslavljanje procesov:
- ==neposredna komunikacija== preko PID-jev
- ==posredna komunikacija== preko vmesnikov (npr. vrat)
  Bodisi v naslovnem prostoru procesa ali sistemskem prostoru

4 prehodi med uporabniškim in jedrnim načinom $\rightarrow$ leno kopiranje naslova sporočila
![[OS_MedprocesnaKomunikacija_Kanal.png|400]]
### Deljeni pomnilnik
Počasna vzpostavitev (vzpostavitev preslikave, sinhronizacija) - hitra komunikacija 
Odgovornost za komunikacijski protokol

Primerjava hitrosti:
![[OS_MedprocesnaKomunikacija_Primerjava.png|500]]