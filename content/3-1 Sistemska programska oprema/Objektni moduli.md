Program običajno sestavljen iz več ločenih delov, vsak del lahko pisan v svojem programskem jeziku
- zbirnik dele predstavi v standardni obliki - objektna datoteka
- povezovalnik vse dele poveže v celoto
#### Sestavni deli
==Objektna koda==
==Predviden nalagalni naslov / prenaslovitvena tabela==:
- absolutni naslov $\rightarrow$ absolutni nalagalni naslov
- relativni naslov $\rightarrow$ prenaslovitvena tabela
==Globalni simboli== zapisani v 2 tabelah:
- ==tabela vstopnih simbolov== (EXTREF): ime, vrednost
- ==tabela izstopnih simbolov== (EXTDEF): ime, mesta pojavitve simbola
#### Standardi
- ==COFF== - `4C 01`: predhodnik ELF temelji na formatu a.out, Unix system V in Windows
- ==DOS MZ== - `4D 5A`: izvršljive datoteke v Windowsih
- ==ELF== - ``7F 45 4C 46``: vsi Linux sistemi
- ==Mach-O== - `CAFEBABE` / `FEEDFACE`: MacOS
## ELF
#### ELF zaglavje
Identifikacija formata:
- magična številka
- format: 32b / 64b
- kodiranje podatkov: little / big endian, dvojiški komplement, ...
- verzija
Tip modula: objektni / izvršljiv
Podatki o sekcijah:
- offset do opisov sekcij
- velikost posameznega opisa sekcije
- število opisov sekcij
- indeks sekcije, ki vsebuje podatke ostalih sekcij
#### Opis sekcije
- ime: 4B $\rightarrow$ en od tipov opisa sekcije hrani vsa imena, tukaj hranjen le indeks imena
- tip sekcije - biti / stringi
- offset, len: kje v datoteki se sekcija nahaja, in koliko je dolga
#### Simbolna tabela
- ime
- vrednost
- velikost