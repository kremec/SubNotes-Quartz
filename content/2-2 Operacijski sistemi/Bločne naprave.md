==Naloga OS: preslikava fizične organizacije podatkov v logično== (medij hrani informacijo $\rightarrow$ uporabnik hrani datoteke)

Vrste (fizičnih) datotečnih sistemov:
- ==diskovni==: ext2, ext3, ... (Linux); vfat, ntfs, ... (Windows), ...
- ==mrežni==: nfs, smbfs, ...
- ==posebni==: proc (/proc/), sysf (/sys/), udev (/dev/), ...

==Gonilnik bločne naprave==: napravo predstavi kot zaporedje blokov fiksne velikosti
==Gonilnik datotečnega sistema==: organizira bloke med seboj in jim doda pomen

Narava je predstavljena kot zaporedje blokov - ==Logical Block Addressing==:
![[OS_BločneNaprave_LBA.png|450]]
Dodeljenvanje blokov:
![[OS_BločneNaprave_DodeljevanjeBlokov.png|450]]
### Fragmentacija
==Fragmentacija==: neučinkovita raba pomnilniškega prostora $\rightarrow$ zmanjšanje kapacitete, hitrosti dostopa, ...
==Defragmentacija==: preazporeditev dodeljenega pomnilnika $\rightarrow$ zmanjšanje fragmentacije

Vrste fragmentacij:
- ==notranja fragmentacija==: fiksna dolžina bloka $\rightarrow$ zadnji blok datoteke je le delno izkoriščen
![[OS_BločneNaprave_NotranjaFragmentacija.png|490]]
- ==zunanja fragmentacija==: neuporabljena območja, ki so vsako zase premajhna za nadaljnje dodelitve
![[OS_BločneNaprave_ZunanjaFragmentacija.png|490]]
- ==podatkovna fragmentacija==: bloki posamezne datoteke niso hranjeni blizu skupaj
![[OS_BločneNaprave_PodatkovnaFragmentacija.png|490]]
<br /><br />
### Razdelitev diska (disk partitioning)
Razdelitev fizičnega diska na več razdelkov - ==particij==, ki se obnašajo kot ločeni logični diski, vsaka ima ==Volume Boot Record== - metapodatke

Načini razdeljevanja diskov - tabele particij:
==MBR (glavni zagonski zapis)==: 1. sektor (= 512 B) vsebuje MRB zapis, do 4 particije, vsaka do 2 TiB
![[OS_BločneNaprave_MBR.png|500]]

==GPT (GUID tabela particij)==: del UEFI sistema, do 128 particij, vsaka do več ZiB
![[OS_BločneNaprave_GPT.png|500]]

==EBR (razširjeni zagonski zapis)==, ==Apple partition map==, ==BSD disklabel==, ...
### Particija FAT
Zgradba: ==grozd (cluster)== - več zaporednih sektorjev
![[OS_BločneNaprave_ZgradbaFAT.png|550]]

==Tabela FAT (File Allocation Table)==: zaporedje grozdov v enojno povezan seznam, ki tvori datoteko
![[OS_BločneNaprave_TabelaFAT.png|500]]

Vrste FAT:
- FAT12 in FAT16: 12/16b naslavljanje, fiksni prostor za krenski imenik
- FAT32: dodatni prostor za metapodatke particije, korenski imenik je lahko shranjen kjerkoli
- VFAT in exFAT: podpora za dolga imena datotek preko dodatnih imeniških vnosov / naravna podpora za dolga imena datotek (256 znakov)