Topics: 
- - -
### Varnost
==Informacijska varnost==: veda o varovanju občutljivih informacij in informacijskih sistemov
==Ranljivost sistema (system vulnerability)==: sistem je izpostavljen možnosti neželene uporabe
==Varnostna pretnja (system threat)==: negativna aktivnost, ki vodi do neželenega delovanja sistema

==Varstvo (safety)==: zagotavljanje želenega delovanja sistema, varovanje pred škodo nenamernih aktivnosti
==Varnost (security)==: izogibanje neželenemu delovanju sistema, varovanje pred škodo namernih aktivnosti (kriminal) - preprečiti nepooblaščene dostope in ohranjati zaupanje v delovanje sistema

Triada Confidentiality, Integrity, Availability (CIA):
![[OS_NadzorDostopa_Triada.png|600]]

Načela načrtovanja varnih sistemov:
- ==ekonomičnost== - preprostost, uporabniku prijazno
- ==odprta zasnova== - predpostavka nepoznavanja s strani napadalca zavajujoča
- ==varne privzete nastavitve==
- ==preverjanje dovoljenj ob dejanjih==
- ==čim manjši privilegiji uporabnika==
### Nadzor dostopa do podatkov/datotek
==Pristnost (avtetičnost)==: dokaz izvora sporočila za prejemnika
==Neovrgljivost (nezatajljivost)==: dokaz dostave sporočila za pošiljatelja

Vrste dovoljenj: ==r==ead, ==w==rite, e==x==ecute, ==--== (prazno)
Sklopi uporabnikov: ==u==ser, ==g==roup, ==o==ther, ==a==ll
![[OS_NadzorDostopa_DovoljenjaDatotek.png|200]]
Datoteko lahko ==briše, kdor ima dovoljenje pisanja v imenik== z datoteko (ne le njen lastnik) - brisanje datoteke je brisanje imeniškega vnosa
==Omejeno bisanje== - oznaka ==t==: datoteko lahko odstrani le lastnik datoteke
### Zagon programov
==Nastali proces dobi dovoljenja trenutnega uporabnika in skupine== - bita `setuid` in `setgid`
Sistemski klici: `getuid()`, `getgid()`, `geteuid()` in `getegid()`