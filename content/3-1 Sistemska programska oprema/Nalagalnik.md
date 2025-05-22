Nalagalnik: naloži program v pomnilnik (objektna datoteka), poskrbi za začetek izvajanja
#### Absolutni nalagalnik
Nalaganje ==absolutnih programov== na ==vnaprej - v času pisanja programa - določen nalagalni naslov==
1. Objektno kodo naloži na predvidene lokacije
2. Začne izvajati program
#### Nalagalnik s prenaslavljanjem
Nalaganje ==prenosljivih modulov== na ==naslov, ki ga pridobi od OS== + ==popravljanje neposrednih naslovov==
1. Od OS pridobi nalagalni naslov
2. Popravi dele objektne kode v skladu s prilagoditvenimi zapisi
3. Objektno kodo naloži na naslov = originalni naslov + nalagalni naslov
4. Izvajanje preusmeri na naslov = naslov iz E zapisa + nalagalni naslov
#### Dinamični nalagalnik
==Program daljši od razpoložljivega pomnilnika==:
- navidezni pomnilnik $\rightarrow$ potrebujemo podporo OS
- dinamično nalaganje $\rightarrow$ hkrati so v pomnilniku le medseboj odvisni deli programa, neodvisni lahko zasedajo isto pomn. lokacijo

Prevajalnik: detektira neodvisne dele kode, namesto klicev prekrivajočih delov vključi klic dinamičnega nalagalnika
Povezovalnik: če dinamični nalagalnik ni del OS, kodo dinamičnega nalaganja vključi v kodo prevedenega programa
Dinamični nalagalnik:
1. Naloži del kode na predvideno mesto
2. Popravi morebitne neposredne naslove
3. Kliče dinamično naloženo kodo
### Začetni nalagalnik
Preprost nalagalnik za prvo nalaganje ob zagonu sistema
Večfazno nalaganje zmeraj bolj kompleksnih nalagalnikov v pomnilnik
Nalaganje začetnega nalagalnika:
1. Shranjen v ROM, ob zagonu prepis v RAM
   Slabost: ne moremo ga spreminjati
2. Sestavni del interne procesorjeve logike kot poseben ukaz / kratek program v ROM
#### Intel
==Sistemsko inicializacijsko področje (SIP)==: zgornjih 64k naslovnega prostora
- zagonske in diagnostične funkcije (POST)
- BIOS
Ob zagonu: `PC=najvišji naslov - 16`: na tem naslovu skok SIP $\rightarrow$ izvajanje POST + prekinitev `0x19` - osnovno začetno nalaganje
### Glavni nalagalni sektor
Začetnega nalagalnika BIOS ne more prebrati iz datoteke (abstrakcije, saj dela le s fizičnimi deli sistema)
==Glavni nalagalni sektor (Master Boot Record - MBR)==: vnaprej določen (ponavadi prvi) sektor posamezne nalagalne enote
- BIOS blok parametrov: podatki o lastnostih nalagalne naprave
- informacije o particijah naprave
- dopolnitveni program za izbiro OS

Nalaganje z MBR:
1. Uporabnik v BIOS nastavi vrstni red nalagalnih enot
2. Po izvedbi POST se v BIOSu kliče prekinitev `0x19` $\rightarrow$ branje prvega sektorja iz prve prisotne nalagalne enote
3. Vsebina sektorja se prenese na naslov `0x0000:7C00`
4. Če na nalagalni enoti ni OS sporoči napako, sicer izvedi rutino za izbor OS (npr. GRUB)
5. Z izbiro OS se določi particija, iz katere se prebere BR (Boot Record) $\rightarrow$ MBR ga naloži in izvajanje preseli nanj $\rightarrow$ za nalaganje OS poskrbi BR