### Monolitna zasnova backenda
==Vse funkcije poslovne logike združene v celoto==
![[Mikrostoritve-Image-1.png|400]]
Nekatere storitve se uporabljajo več kot druge (primer spletne trgovine: katalog > košarica)
Problem: ko horizontalno skaliramo celo arhitekturo, se po ==nepotrebnem skalirajo tudi manj nujne storitve== - cena clouda
### Mikrostoritve
==Poslovno logiko razbijemo na zaključene funkcionalne celote==
![[Mikrostoritve-Image-2.png|400]]
+ ==modularnost==
+ ==ponovna uporaba==: sprememba pristopa iz gradnje na sestavljanje aplikacij
+ (horizontalna) ==skalabilnost==: zagotovljen uptime, sistem za (de)skaliranje glede na porabo (Kubernetes)