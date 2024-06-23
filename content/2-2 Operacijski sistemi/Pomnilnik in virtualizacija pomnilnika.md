#TODO-LINKS 
## Pomnilnik
==Fizični pomnilnik== (PA): s procesorjem fizično povezan pomnilnik
==**Naslovni prostor**== (VA): OS abstrakcija fizičnega pomnilnika, kot ga procesi vidijo
Proces vidi le svoj kos fizičnega pomnilnika

Zgodnji preprosti sistemi: velja VA = PA
Večprogramiranje: deljenje pomnilnika - preslikava VA $\rightarrow$ PA

==Sklad==: avtomatska (de)alokacija preko prevajalnika - lokalne spremenljivke, argumenti funkcij, ...
==Kopica==: eksplicitna alokacija, dealokacija lahko eksplicitno ali preko GC (Garbage Collection)

Določanje naslovov:
- čas prevajanja: zbirnik/prevajalnik določi naslove spremenljivk
- čas povezovanja: zlaganje prevedenih modulov skupaj
- čas nalaganja: nalaganje prenosljive kode na poljubno mesto v fizičnem pomnilniku
- čas izvajanja: premikanje in zamenjava procesor
### Pomnilniške storitve OS
`exit()` sprosti naslovni prostor procesa

Nastavljanje velikosti podatkovnega segmenta (kopice): sistemski klic `brk`
Alokacija pomnilnika: `malloc`, `calloc`, `realloc`, ...
Dealokacija pomnilnika: `free`

==ASLR (Address Space Layout Randomization)==: randomizacija naslovnega prostora
Napad: skok v okvarjeno kodo na nek znan fiksen naslov
Rešitev: naključna razporeditev ključnih delov naslovnega prostora
## Virtualizacija pomnilnika
Cilji:
- proces vidi ==sklenjen del pomnilnika==
- ==izolacija procesov== - ne vplivajo drug na drugega ali na OS
- ==transparentnost== - proces se ne zaveda virtualizacije
- ==učinkovitost== - hitra preslikava naslovov (OS, MMU in TLB)

Izvedbe preslikovanja:
- ==celotna presolikovalna tabela== - nemogoče zaradi preveč naslovov
- ==premeščanje== - celoten naslovni prostor premestimo na poljubni PA
- ==segmentacija== - razdelitev na bloke različnih velikosti
- ==ostranjevanje== - razdelitev pomnilnika na bloke enakih velikosti
- ==segmentacija + ostranjevanje== - segmenti so razdeljeni na strani
#### Statično premeščanje
Program se prevede na VA 0, naloži na izbrani PA; uporaba le, ko ni strojne podpore za virtualizacijo
#### Dinamično premeščanje
Bazni register - nalagalni naslov, mejni register - velikost naslovnega prostora
Strojna podpora preslikovanja in preverjanja zaščite, manipulacija regstrov v priviligiranem načinu
#### Segmentacija in ostranjevanje
![[OS_VirtualizacijaPomnilnika_SegmentacijaOstranjevanje.png|350]]
==Segmentacija==:
- bloki - segmenti različnih velikosti, imajo pomen (koda, podatki, ...)
- težavno upravljanje pomnilnika, zunanja fragmentacija

==Ostranjevanje==:
- bloki - strani enake velikosti, brez pomena
- lažje upravljanje pomnilnika, notranja fragmentacija
### Ostranjevanje
![[OS_VirtualizacijaPomnilnika_Ostranjevanje.png|400]]
Velika tabela pri velikih naslovih $\rightarrow$ večnivojska tabela strani
Veliko dostopov do pomnilnika za iskanje naslova $\rightarrow$ TLB (predpomnilnik preslikovanja)
### Uporaba zunanjega pomnilnika
Na voljo je malo notranjega poomnilnika (RAM), naslovni prostor pa je lahko zelo velik
Zato uporabimo zunanji pomnilnik (diski) kot ==odlagalni prostor (swap space)==:
- swap out - shranjevanje strani iz pomnilnika na disk
- swap in - nalaganje strani iz diska v pomnilnik
![[OS_VirtualizacijaPomnilnika_Swapping.png|500]]
- ==Zadetek v TLB==: če VPN obstaja v TLB ...
- ==Zadetek v TLB, iskanje v tgabeli strani==: če VPN obstaja v preslikovalni tabeli strani ...


- ==Zgrešitev strani==: naloži stran iz zunanjega pomnilnika, osveži vnos v preslikovalni tabeli strani, ...

Če je za stran premalo prostorav pomnilniku, naredi zamenjavo strani:
- ==FIF (Furthest in future)==: izločitev strani, ki bo dostopana najdlje v prihodnosti (nemogoče vedeti vnaprej)
- ==FIFO (First In First Out)==: izločitev strani, ki je najdlje v pomnilnmiku (lahko spet takoj rabimo)
- ==LFU (Least-Frequently Used)==: izločitev najmanj uporabljane strani (evidenca uporabe)
- ==LRU (Least-Recently Used)==: izločitev najdalje neuporabljene strani (evidenca časov)