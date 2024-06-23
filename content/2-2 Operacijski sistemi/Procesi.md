Topics: #TODO-LINKS 
- - -
==Proces== kot ==pasivna== entiteta (shranjena koda / podatki) in ==aktivna== entiteta (program v izvajanju)
Glavni nalogi: ==lastništvo virov== (procesi) in ==izvajanje kode== (niti)
Storitve OS: upravljanje življenj procesov in medprocesna komunikacija

Sestava procesa:
- programska koda: strojna koda, ki se izvaja na procesorju
- **sklad in kopica**: podatki, pomembni za izvajanje (naslovni prostor, ki ga proces uporablja)
- podatki: ostali podatki
- ==deskriptor procesa==: nadzorni podatki OS za upravljanje procesa
### Življenje procesa
Hierarhija procesov: ==starš== poda poda zahtevo po stvaritvi novega procesa - ==otroka==

Stvaritev procesa:
- evidenca procesov: ==PID== (identifikator procesa) in ==PPID== (identifikator starša procesa)
- inicializacija PID, PPID, stanja procesa, podajanje argumentov, priprava pomnilnika, ...
- nalaganje izvršne datoteke: ==eager== - nalaganje celote pred izvajanjem, ==lazy== - po potrebi

Končanje procesa:
- sprostitev zasedenih virov
- sprostitev deskriptorja procesa

Stanje procesa:
![[OS_Procesi_StanjeProcesa.png|500]]
==Nov==: tekom stvaritve in inicializacije

Aktiven:
- ==pripravljen==: pripravljen na izvajanje - čakanje na dodelite procesorja
- ==izvajan==: dejansko izvajanje na procesorju

Nekativen:
- ==čakajoč/blokiran==: čakanje na nek dogodek, potreben za nadaljevanje procesa
==Končan==: tekom ukinjanja in sprostitve virov
### Podatkovne strukture
Seznami pripravljenih, čakajočih, ... procesov vsebujejo ==deskriptorje procesov==: jedrna podatkovna strukturam ki hrani ==nadzorne podatke== procesa in omogoča ==preklapljanje procesov==
- Identiteta: PID in PPID, čas stvarjenja procesa
- Okolje: argumenti in okoljske spremenljivke
- Razvrščevalni podatki: stanje, prioriteta, dogodki na katere proces čaka, ...
- Poverjenja: UID in GID, dotopne pravice
- Izvajalni kontekst: uporabniški in kontrolni registri
- Kontekst datotečnega sistema: trenutni delovni imenik, seznam odprtih datotek, ...