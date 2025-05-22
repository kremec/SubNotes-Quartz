Procesor razume le ==strojni jezik==, a zamudno pisanje $\rightarrow$ uporaba ==zbirnega jezika==: linearna preslikava v strojni jezik
Prevajalnik: zbirni jezik $\rightarrow$ strojni jezik, mnemoniki $\rightarrow$ operacijske kode, operandi $\rightarrow$ številske vrednosti
### Specializirane vrste zbirnikov
- ==modularni==: omogoča pisanje programa v modulih namesto eni sami datoteki
- ==mikro==: zbiranje na še nižji nivo - mikroprocesorske ukaze
- ==makro==: omogoča uporabo makrojev
  Ukazi makroja se vrinejo nepsredno v kodo namesto imena makroja (namesto klica podprograma)
- ==meta==: podamo opis računalnika, za katerega naj zbira
- ==prečni==: omogoča zbiranje za druge arhitekture, kakor na kateri teče
- =="naloži in izvedi"==: hkratno prevajanje neposredno v pomnilnik in izvajanje
### Zbirniški stavek
`[<oznaka stavka>] <ločilo> <mnemonik> {<ločilo> <operand>} [<ločilo> <komentar>]`
- ==oznaka stavka==: simbolično ime / naslov vrstice za kasnejše naslavljanje nanjo
  Lokacija: na začetku vrstice - levi naslov / desno od mnemonika (kot operand) - desni naslov
- ==mnemonik==: okrajšava strojnega ukaza
- ==ločilo==: izbrani znaki za enostavnejše delo pregledovalnika
- ==operand==: simbolično ime (oznaka stavka) / ime konstante (`EQU`) / številske vrednosti (`#1`)
### Osnovne naloge
1. ==Pregledovalnik==: pregled in razčlenitev zbirniškega stavka
2. Nadomestitev mnemonikov z operacijskimi kodami
3. Nedomestitev simboličnih imen z ustreznimi številskimi vrednostmi
4. Razširitev simboličnih operandov (`EQU`)
5. Pretvorba konstant iz izvorne oblike v notranjo strojno predstavitev
6. Prevedba in inetrpretacija "psevdo ukazov"
   ==Psevdo ukazi==: direktive, namenjene zbirniku, ki se ne prevedejo v strojno kodo (npr. `START`, `RESW`, ...)
7. Tvorba strojnih ukazov in izpis kode
8. Priprava in izpis liste prevajanj - vhodni izvorni stavek, objektna koda, številske vrednosti, ...
9. Tvorba množic tabel - simbolna tabela, tabela sekcij, ...
10. Specialne možnosti
#### Lokacijski števec
Zbirnik za vsak ukaz ugotovi, koliko pomnilnika zasede $\rightarrow$ vodi trenutno zasedenost pomnilnika
Uporaba pri razbiranju naslovov posameznih zbirniških stavkov
## Pregledovalnik
Vhodne vrstive zbirne kode razgradi na enote in jih okvalificira
Implementacija: končni avtomat in konstrukcija tabel
#### Ukazna tabela
Nespremenljiva tabela, zapečena v zbirnik, s funkcijo iskanja
Vsebuje sezname:
- ==mnemonik== - operacijska koda - tip ukaza - št. operandov
- ==register== - št. registra
- ==psevdoukaz==

Implementacija: urejena tabela (hitrejše iskanje): po abecedi / po pogostosti
Uporaba: določanje velikosti prevedenega ukaza (za lokacijski števec), pretvorba mnemonikov v strojno kodo
#### Simbolna tabela
Vsebuje: levi naslov - lokacijski števec / vrednost pri EQU
Implementacija: hashmap
Uporaba: razreševanje simboličnih imen
Možne težave:
- D naslov se pojavi pred L $\rightarrow$ dopolnimo kasneje ko poznamo lokacijo definicije
- L naslov se pojavi dvakrat $\rightarrow$ napaka (dvoumnost)
- D naslov se ne razreši $\rightarrow$ napaka (ni definicije simbola)
### Vnaprejšnje sklicevanje
Razpoznamo desni naslov (uporaba) pred levim naslovom (definicijo)
#### Enoprehodni zbirnik
Eno branje datoteke
Rešitev:
- ==omejevanje programerja==: zahteva po definiciji levega naslova pred uporabo
  Omejitev: skoki naprej niso podprti $\rightarrow$ težje programiranje
- ==turbo princip== "naloži in izvedi": beleženje manjkajočih simbolov in popravljanje za nazaj
  Predpostavka: vsa orodja in celoten program morajo biti ves čas v delovnem pomnilniku
- ==naslavljanje s simbolno tabelo==: sklicevanje na vpis v simbolni tabeli namesto na simbol
  Slabosti: programu potrebno pridružiti celo simbolno tabelo, ena stopnja naslavljanja več $\rightarrow$ počasneje
#### Dvoprehodni zbirnik
Dvakratno branje datoteke
Na začetku obeh prehodov lokacijski števec nastavimo na enako vrednost (`START ...`)
##### Prvi prehod
Razreši vse leve naslove - zapis v simbolno tabelo
==Ukaz== v zbirnem jeziku:
1. L = dolžina strojnega ukaza (iz operacijske table)
2. zapis `<oznaka>:<lokacijski števec>` v simbolno tabelo
3. LŠ = LŠ + L

==Navodila== zbirniku:
- ==rezervacije in inicializacije== (RESW, BYTE)
    1. zapis `<oznaka>:<lokacijski števec>` v simbolno tabelo
    2. LŠ = LŠ + <dolžina rezervacije>
- ==konstanta== (EQU)
    1. zapis `<oznaka>:<vrednost>` v simbolno tabelo
- ==izhodišče== (ORG)
    1. LŠ = `<vrednost operanda>`
- ==konec== (END)
##### Drugi prehod
Zamenjaj desne naslove z vrednostmi iz simbolne tabele
==Ukaz== v zbirnem jeziku:
1. iz operacijske tabele preberi opcode, tip in dolžino ukaza
2. iz simbolne tabele preberi vrednost operanda (desnega naslova)
3. generiraj in izpiši strojno kodo
4. LŠ = LŠ + L

==Navodila== zbirniku:
- ==rezervacije== (RESW)
    1. LŠ = LŠ + <dolžina rezervacije>
- ==rezervacija + inicializacija== (BYTE)
    1. generiraj objektno kodo - vrednost konstante
    2. LŠ = LŠ + <dolžina rezervacije>
- ==konstanta== (EQU)
- ==izhodišče== (ORG)
    1. LŠ = `<vrednost operanda>`
- ==konec== (END)
##### Komunikacija med obema prehodoma
- samo simbolna tabela
- pri prehod ustvari vmesno datoteko z vso dotedanjo analizo $\rightarrow$ drugi prehod bere le to
<br><br><br><br><br><br><br>
### Tvorba operacijske kode in operandov
==Operacijska koda== poleg mnemonika lahko odvisna tudi od:
- načina naslavljanja (npr. `RET` odvisen od bližine naslova)
- tipa operandov (npr. ADD odvisen od velikosti operanda; kateri operand je register in kateri pomnilniški naslov)
- velikost konstante (npr. EQU velikost operanda $\rightarrow$ direktno/razširjeno naslavljanje)

==Operand==:
- ==rezervirane besede== (npr. oznake registrov), pogosto shranjujemo v operacijski tabeli
- ==številska konstanta== v ukazu
- ==simbolično ime== (desni naslov) v simbolni tabeli
- ==sestavljen operand== iz simboličnih imen, konstant / računskih operatorjev / logičnih operatorjev
### Objektna koda
Program $\rightarrow$ ==objektna koda== $\rightarrow$ ==objektna datoteka== v ==objektnem formatu== (standardu)
Uporaba: samostojen program / modul v večjem programu
#### SIC objektna datoteka
Tekstovni format s 3 vrstami zapisov:
1. ==Zaglavje (Header - H)==: (1) H, (2-7) ime programa, (8-13) začetni naslov, (14-19) dolžina programa (LŠ + dolžina ukaza END)
2. ==Programski zapis (Text - T)==: (1) T, (2-7) začetni naslov T zapisa, (8-9) dolžina T zapisa $\rightarrow$ max 30 = 0x1E bajtov, (10-69) objektne kode 3B ukazov $\rightarrow$ max 10 ukazov 
3. ==Zapis za konec (End - E)==: (1) E, (2-7) naslov prvega izvršljivega ukaza
#### Posebnosti pri SIC/XE
Več formatov ukazov: 1/2/3/4-B koda
Več načinov naslavljanja: takojšnje - `#<operand>` in posredno - `@<operand>`
Registrsko-registrski ukazi: več ukazov
Relativno naslavljanje: privzeto PC, sicer bazno (če direktiva BASE), ne pozabi na n in i bite
- PC-relativno: `odmik = UN - (LŠ) - L`
- bazno-relativno: `odmik = UN - (B)`
Uporaba 4-zlogovnega razširjenega formata: `+<ukaz>`
### Prenaslavljanje
==Absolutni programi==: fiksen nalagalni prostor - redko uporabno v praksi zaradi nalaganja programov na naključno mesto v pomnilniku
- na nalagalni naslov so občutljivi le neposredni (ne-relativni) naslovi
- prenaslavljanje ni potrebno pri ukazih: PC/bazno reativno naslavljanje / formata ukazov 1 in 2

Zbirnik označi neposredne naslove, da jim nalagalnik prišteje vrednost nalagalnega naslova:
==Prilagoditveni zapis (M-Modification)==: (1) M, (2-7) relativna lokacija ukaza, (8-9) dolžina naslovnega polja (ponavadi `05`/`06` - katere pol-byte popraviti)
Smiselno za malo ukazov potrebnih popravkov, sicer raje uporabimo
==Bitna maska v T zapisu==: (1) T, (2-7) naslov, (8-9) dolžina, (10-12) prilagoditveni biti $\rightarrow$ vsak bit pove, če je potrebna sprememba ukaza, (13-72) objektna koda
### Programski bloki
Programsko kodo želimo razdeliti v bloke (koda, krajše in daljše spremenljivke)
- poenostavljeno naslavljanje in lažje programiranje

Zbirnik namesto programerja označene odseke zbirne kode združi v bloke objektne kode
Ukaz: `USE <ime_bloka>`
- dogovor: privzet neimenovan blok se razteza od začetka programa/ukaza USE brez podanega imena do prvega imenovanega bloka
#### 1. prehod
Generacija 2 tabel: ==simbolni tabeli dodamo stolpec "blok"==, ==tabela blokov== - ime, naslov, dolžina
Ko zbirnik zazna ukaz USE:
- LŠ prejšnjega bloka zapiše v stolpec "dolžina" v tabelo blokov v pravilno vrstico
- v tabeli blokov poišče pravi novi blok:
    - ne obstaja: ustvari nov blok
    - obstaja: LŠ=dolžina + povečaj  naslove vseh blokov za njim za podaljšano dolžino tega bloka
#### 2. prehod
Izračun vrednosti vseh simboličnih imen z uporabo obeh tabel
Objektno kodo izpisujemo po vresti kot ve v izvorni kodi, saj smo za vsak blok shranili LŠ - končno relativno nalagalno lokacijo
<br>
### Kontrolne/nadzorne sekcije
Ločene programske enote v eni/več datotekah, ki sestavljajo program - omogočajo prevajanje le dela programa
- `EXTDEF`: izvoz simbola iz sekcije $\rightarrow$ zbirnik jih bo označil, povezovalnik popravi naslove
- `EXTREF`: uvoz simbola iz druge sekcije

Novi/prilagojeni zapisi:
1. ==Definicijski zapisi (D - Definition)==: (1) D, (2-7) ime zunanjega simbola, (8-13) relativni naslov zunanjega, (14-73) informacije o ostalih simbolih - ponavljanje 2-13
2. ==Referenčni zapis (R - Reference)==: (1) R, (2-7) ime zunanjega simbola, (8-73) informacije o ostalih simbolih - ponavljanje (2-7)
3. ==prilagoditveni zapis (M - Modification)==: (1) M, (2-7) začetni naslov polja v kodi, (8-9) dolžina polja, (10) smer popravka - + ali -, (11-16) ime zunanjega simbola, katerega vrednost je treba prišteti/odšteti
### Literali
==Literal==: konstanta brez imena, uporabljena neposredno v zbirniškem ukazu
Zbirnik:
- za literal rezervira prostor: na koncu programa / tik po skočnem ukazu / po ukazu LTORG
- se nanj sklicuje preko ==enostavnega naslavljanja== (ne takojšnje)
- prepozna dvojne literale: zanje rezervira en prostor in se sklicuje le nanj

Za razreševanje zbirnik uporabi ==tabelo literalov== s stolpci: literal, dolžina, tip, naslov (npr. EOF, 3, C, ...)
#### 1. prehod
Za vsak najdeni literal preveri tabelo, če ne obstaja: določi dolžino in tip, naslov pusti prazen
Ko pride do mesta za rezervacijo prostora določi vrednosti naslovov:
- `naslov(0) = LŠ`
- `naslov(i) = naslov(i-1) + dolžina(i-1)`
#### 2. prehod
Vsak najdeni literal zamenja z naslovom iz tabele
Ko pride do mesta za rezervacijo prostora vse literale prepiše v objektno kodo
### Simbolične konstante (EQU)
Simboličnemu imenu lahko priredimo:
- konstantno vrednost / vrednost oznake (npr. `ALFA EQU 5`)
- enačimo vrednosti simbolnih imen (npr. `BETA EQU ALFA`)
- vrednost aritmetičnega ukaza (npr. `GAMA EQU ALFA-BETA+3`)
- vrednost LŠ - naslov naslednje pomnilniške lokacije (npr. `BUFEND EQU *`)

Izrazi so lahko:
- ==relativni==: vrednost odvisna od LŠ $\rightarrow$ pozitiven predznak, brez množenja/deljenja
- ==absolutni==: vrednost neodvisna od LŠ $\rightarrow$ same absolutne konstante / relativne komponente nastopajo v obratno predznačenih parih

Vnaprejšnje sklicevanje - pred 2. prehodom morajo biti vse vrednosti simboličnih imen znane:
- prepovemo vnaprejšnje sklicevanje
- ==tabela vnaprejšnjih referenc (dodani stolpci simbolni tabeli)==: simbolično ime, odvisnost, referenca/vrednost, odvisniki
  Cilj: v stolpcu odvisnost imeti same ničle, sicer ==nerazrešen simbol / ciklične reference==
#### Delovanje zbirnika
`SIM EQU REF`
Nova simbolična konstanta - ustvari novo vrstico:
- `referenca = REF`
- `odvisnost = št. odvisnosti v REF`
- vsem simbolom iz `REF` dodaj `SIM` med odvisnike, če simbol iz `REF` še ne obstaja ustvari novo vrstico

Razreševanje simbolov: ko je `odvisnost = 0` pomeni, da ni več neznank v `REF`
- izračunamo `referenca`
- vsem ostalim simbolom, ki so v `odvisniki`:  `odvisnost -= 1`