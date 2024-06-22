Topics: 
- - -
Problem: dostop do datotek iz več pomnilnih naprav - vsaka s svojo ==imeniško strukturo==
==Več ločenih imeniških struktur== - Windows:
- črkovne oznake naprav - disketni enoti `A:` in `B:`, diskovne enote `C:`, `D:`, ...  $\rightarrow$  dostop - oznaka naprave + pot dod datoteke

==Ena enotna imeniška struktura== - Linux, Unix, macOS:
- naprave kot pod-strukture ==pripnemo (mount)== v ciljni imenik (==točka pripenjanja==)  $\rightarrow$  ukaza `mount` in `unmount`
### Navidezni datotečni sistem (VFS)
Nudi enoten vmesnik do različnih fizičnih datotečnih sistemov z abstrakcijo datoteke.
Abstrakcija je objektno orientirana:

Struktura ==superblock==: predstavitev priklopljenega datotečnega sistema
- tip in lokacija (naprava) datotečnega sistema, ter nizkonivojske operacije nad njim
- kazalec inode na ==korenski imenik==;  velikost bloka, zastavice read-only, dirty, ...

Struktura ==inode== (index node): datoteka poljubnega tipa, predstavlja vse razen imena datoteke
- št. inode, št. trdih povezav, velikost datoteke ter kazalci na bloke z vsebino
- lastnik, skupina - dovoljenja, čas dostopa in spremembe
- operacije `create()`, `link()`, `mkdir()`, `rmdir()`, `read()`, `open()`, ...

Struktura ==dentry== (directory entry): imeniški vnos v imeniku, preslikava ime $\rightarrow$ inode
- ime datoteke, kazalec inode na datoteko ter kazalec na starševski imenik

Primer:
![[OS_VFS_PrimerStruktur.png|inlL|400]]
### Datotečni deskriptorji
Struktura ==file==: predstavlja odprto datoteko = datotečni deskriptor
- kazalec na ustrezen dentry; uid in gid procesa, ki je datoteko odprl; pozicija v datoteki

Vsak datotečni deskriptor ima št. deskriptorja, ki ji ustreza tak objekt: 0 $\rightarrow$ `stdin`, 1 $\rightarrow$ `strdout`, 2 $\rightarrow$ `stderr`, ...

Podvajanje št. deskriptorja - sistemska klica:
- `new = dup(orig)` ... vrne št. deskriptorja `new`, ki predstavlja isti dekriptor (isti objekt file) kot `orig`, uporabi se prva prosta št. deskriptorja
![[OS_VFS_dup.png|370]]
- `dup2(orig, new)` ... preusmeritev deskriptorja `orig` v `new`
![[OS_VFS_dup2.png|370]]