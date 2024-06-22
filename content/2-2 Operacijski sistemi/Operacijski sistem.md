Topics: #TODO-LINKS 
- - -
Uporabniški vidik: vmesnik med uporabnikom in računalnikom
IT vidik: vpogled in upravljanje sistema - programske in strojne opreme, ponudnik sistemskih storitev

Koncepti OS:
==Abstrakcija==: posplošitev/skrivanje podrobnosti ter združevanje podobnih enot (npr. abstrakcija **datoteke**, ki je lahko fizično shranjena na veliko možnih načinov)
==Virtualizacija==: ustvarjanje navidezne opreme, ki se slika v realno/fizično (npr. emulacija procesorja, pomnilnika, ...)
==Varnost==: mehanizmi zaščite sistema (npr. izolacija procesov, zaščita pomnilnika in V/I naprav, ...)
==Sočasnost==: obstoj večih procesov z občutkom istočasnega izvajanja, sinhronizacija
==Persistenca==: obstoj podatkov v učinkoviti hrambi

Zgradba OS: [[Operacijski sistem#Jedro OS|jedro]], **gonilniki naprav**, [[Lupina|lupina]], [[Računalniški sistem#Programska oprema (software)|sistemska orodja]], pogosto kakšna [[Računalniški sistem#Programska oprema (software)|sistemska programska oprema]]
### Jedro OS
==Jedro==: programska koda najpomembnejših storitev OS - upravljanje s procesi, pomnilnikom, ...

Procesorski nivoji zaščite:
- ==zaščiteni način==: omejena uporaba procesorja (programska oprema)
- ==priviligirani način==: neomejeno obvladovanje sistema - pomnilnik, naprave, sistemski ukazi, ...

Komunikacija med jedrom in strojno opremo: ==naprava== (omogoča opravilo) $\leftarrow$ ==kontrolnik naprav== $\leftarrow$ ==vmesnik strojne opreme== $\leftarrow$ ==gonilniki naprav== (upravljajo z napravo preko vmesnikov) $\leftarrow$ programi
### Arhitektura jedra
==Arhitektura jedra==: struktura in način povezovanja med posameznimi deli jedra

==Monolitno jedro==: velik kos strojne kodi, ki vsebuje celoten OS
Hitrost - posamezni deli OS komunicirajo preko navadnih klicev funkcij
Napaka v enem delu lahko povzroči sesutje celotnega OS, težja obladljivost kode
Primeri: System V, DOS, Windows 9x, FreeDOS, ...

==Monolitno modularno jedro==: zasnova modulov gonilnikov
Dinamičnost - module lahko naložimo/odstranimo tekom izvajanja
Primeri: BSD, Linux, OS-9, ...

==Mikro jedro==: vsebuje le osnovne funkcionalnosti, ostalo se izvaja preko procesov
Prilagodljivost, porazdeljenost, varnost, enostavna implementacija
Počasna medprocesna komunikacija
Primeri: Mach, L4, PikeOS, ...

==Hibridno jedro==: mikro-jedrna zasnova (ločeni servisi) v monolitski izvedbi (skupen naslovni prostor)
Primeri: Windows NT, iOS, macOS, ...

![[OS_OS_PrimerjavaJeder.png]]

==Nano/piko jedro==: manjše mikro jedro / hipervisor / **HAL** (Hardware Abstraction Layer)
==Exokernel==: manjše mikro jedro le z zaščito in samouporabo virov
==Unikernel==: namesno jedro za izbrano aplikacijo - navadno v virtualnem okolju