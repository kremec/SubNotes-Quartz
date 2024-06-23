#TODO-LINKS
==Več/Multiprogramiranje==: sočasno izvajanje več procesov na enem procesorju
==Več/Multiprocesiranje==: vzporedno izvajanje več procesov na več procesorjih

Souporaba virov med več entitetami:
- ==časovno deljenje==: časovne rezine (npr. procesorja, omrežne povezave, ...)
- ==prostorsko deljenje==: rezine vira samega (npr. pomnilnika, diskovnega prostora, ...)
### Večopravilnost
==Večopravilnost==: večprogramiranje preko časovnega deljenja
- ==sodelovalna==: proces prepusti procesor znotraj sistemskih klicev / kliče yield
  Računsko intenzivni procesi lahko procesor "ugrabijo"
- ==prevzemna==: časovne rezine upravlja OS s prekinitveno uro
  Po preteku se procesor dodeli naslednjemu procesu, trenuten se vrne v vrsto
### Neposredno izvajanje
==Neomejeno neposredno izvajanje==: "samo poženi program"
Hitro izvajanje v celoti na procesorju, a med čakanjem na V/I operacije procesor ni izkoriščen
OS je proces, ki ne teče vedno $\rightarrow$ prožimo ga s prekinitvami:
- **prekinitve in izjeme** (npr. sistemska ura, V/I dogodek, zgrešitve strani, deljenje z 0, ...)
- sistemski klici (npr. ustvarjanje procesa, branje datoteke, ...)
![[OS_Večopravilnost_Neomejeno.png|400]]

==Omejeno neposredno izvajanje==: "inicializiraj PSP in rokovalnik sistemskih klicev, poženi program in čakaj na vrnitev nadzora OS"
![[OS_Večopravilnost_Omejeno.png|400]]
### Preklop procesa
Na koncu rokovalnika, tik preden se vrnemo v uporabniški način:
- razvrščevalnik izbere naslednji proces v čakalni vrsti
- spremembe stanj procesov (odhajajoči proces na čakanje v vrsto, prihajajoči proces se aktivira)
- preklop konteksta in menjava naslovnega prostora - PC, sklad, statusni in ostali registri

Učinkovitost tega procesa je odvisna od:
- strojne opreme - hitrost pomnilnika, arhitekture sistema, procesorja, ...
- OS - razvrščevalni algoritem, čiščenje procesov, ...