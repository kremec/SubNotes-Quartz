==Razvrščanje==: odločanje o razvrščanju procesov na viru (npr. procesor, pomnilnik, ...)
- ==dolgoročno razvrščanje poslov==: ==razvrščevalnik poslov== (del OS) skrbi za razvrščanje poslov, navadno nepodprto
- ==srednjeročno menjavanje procesov==: pomnilnika primanjkuje $\rightarrow$ ==menjalnik== proces začasno shrani na disk, kasneje ga naloži nazaj
- ==kratkoročno razvrščanje na procesorju==: ==razvrščevalnik== izbira izmed za izvajanje pripravljenimi procesi, ==dodeljevalnik== preklopi iz trenutnega na izbrani proces

Računsko intenzivna opravila: preferirajo daljše časovne rezine - višja izkoriščenost procesorja
V/I intenzivna opravila: preferirajo krajše časovne rezine - višja odzivnost procesa
### Mere zmogljivosti
- Paketni sistemi:
![[OS_Razvrščanje_PaketniSistemi.png|500]]
- Interaktivni sistemi - časovno dodeljevanje:
![[OS_Razvrščanje_InteraktivniSistemi.png|500]]
Ostale mere: izkoriščenost procesorja, prepustnost sistema - št. obdelanih procesov v danem časovnem obdobju, poštenost - enakomernost delitve procesorja glede na prioritete
### Razvrščevalni algoritmi
#### Osnovni algoritmi
- ==FCFS (First Come First Serve)==: proces, ki je prej pripravljen
  Pripravljen proces gre na konec vrste, za izvajanje se vzame proces iz čela (FIFO) vrste
  Enostavnost, razvrščanje brez prevzemanja
  Slab odzivni čas, dober čas obdelave
- ==SJF (Shortest Job First)==: najkrajši pripravljeni proces
  Procesi se hitreje obračajo, a potrebno vnaprejšnje poznavanje dolžine poslov
  Optimalen algoritem, razvrščanje brez prevzemanja
  Slab odzivni čas, odličen čas obdelave
- ==PSJF (Preemptive Shortest Job First)==: posel, ki se prej konča
  Potrebno vnaprejšnje poznavanje dolžine poslov
  Razvrščanje z odvzemanjem
  Slab odzivni čas, odličen čas obdelave
- ==RR (Round Robin)==: pripravljene posle razvrščamo krožno zaporedoma, vsakega nekaj časa
  Pripravljen proces gre na konec vrste, za izvajanje se vzame proces iz čela (FIFO) vrste, procesi se izvajajo v določenih časovnih rezinah
  Razvrščanje z odvzemanjem
  Odločen odzivni čas, slab čas obdelave
#### Prednostni algoritmi
Upoštevanje prioritet procesov
- ==HPF (Highest Priority First)==: pripravljeni proces z najvišjo prioriteto
  Razvrščevalnik brez ali z prevzemanjem: ![[OS_Razvrščanje_HPF.png|450]]
  Težava ==stradanja==: procesi z nižjo prioriteto ne pridejo na vrsto
  Rešitev ==staranja==: procesom, ki ne dobijo procesorja, vsake toliko povečamo prioriteto
- ==SIRO (Service In Random Order)==: razvrščanje po neki shemi naključnosti
  Razvrščevalnik brez ali z prevzemanjem
- ==LS (Lottery Scheduling)==: določanje procesa z loterijo - prepustnicami
  Procesu pri stvaritvi dodelimo nekaj prepustnic (višja prioriteta $\rightarrow$ več prepustnic)
  Pri razvrščanju se izbere naključna prepustnica, procesu zmagovalcu se dodeli procesor
- ==SS (Stride Scheduling)==: proces, ki je prehodil najmanj
  Proces pri stvaritvi dodelimo dolžino koraka (višja proriteta $\rightarrow$ krajši korak)
  Pri razvrščanju se koraki upoštevajo v skupno pot, procesu z najmanjšo potjo se dodeli procesor
#### Praktični algoritmi
- ==MLQ (Multi-Level Queue)==: večnivojska vrsta skupin oppravil - vrste padajoče po prioriteti, naraščajoče urejene po časovni rezini
  Znotraj posamezne vrste se uporablja RR
![[OS_Razvrščanje_MLQ.png|250]]
- ==MLFQ (Multi-Lvele Feedback Queue)==: MLF + prehajanje med vrstami
  Poslu ob prihodu dodelimo najvišjo prioriteto.
  Posel porabi celotno časovno rezino $\rightarrow$ dekrementiramo prioriteto
  Po določenem času vse posle prestavimo na najvišjo prioriteto - preprečevanje stradanja
- ==Razvrščevalnik Linux O(1)==: izbira in dodajanje opravila v konstantnem času
![[OS_Razvrščanje_Linux1.png|500]]
![[OS_Razvrščanje_Linux2.png|600]]
