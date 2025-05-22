## Modeli porazdeljenih sistemov
#### Povezave v omrežju
- ==povezava s sprejemljivimi izgubami== (UDP): sporočila se lahko izgubijo in podvajajo $\rightarrow$ najprimernejši
- ==zanesljiva povezava== (TCP): sporočila dostavljena točno enkrat
- ==overovljena zanesljiva povezava== (TLS): nadgradnja z mehanizmi overovitve pošiljatelja
#### Obnašanje procesov
- ==binazntinski model / model z napako==: predpostavlja nepričakovano obnašanje (hrošči, napake, zlonamerni posegi, ...)
- ==neobnovljivi proces==: predpostavlja pravilno obnašanje, a se ob sesutju ne vzpostavi nazaj
- ==obnovljivi proces==: predpostavlja pravilno obnašanje, a se ob sesutju ponovno zažene (vseeno izgubimo vsebino pomnilnika) $\rightarrow$ najprimernejši
#### Modeliranje časa
- ==sinhroni model==: posredvanje sporočila se vedno zaključi v danem časovnem okvirju $\rightarrow$ nerealistično
- ==asinhroni model==: posredovanje sporočila lahko traja neomejen čas $\rightarrow$ robustnost, a ni zmeraj možen
- ==delno sinhronski model==: predpostavlja večinoma sinhrono delovanje z možnostjo zakasnitev $\rightarrow$ najprimernejši
### Zaznavanje napak
Posredovanje sporočila $\rightarrow$ sporočilo ne prispe do prejemnika / prejemnik ga ne obdela / potrditev ne pride do pošiljatelja
Pošiljatelj po določenem času predpostavi nedostopnost prejemnika $\rightarrow$ zaključi z napako / ponovi posredovanje sporočila
## Čas v porazdeljenih sistemih
### Fizične ure
Merijo realni / procesorski čas
Večina OS pozna ==monotono uro==: relativni čas od dogodka (npr. zagona), a neuporabna pri primerjavi dogodkov
#### Kvarčni kristal
Zaniha $2^{15}$-krat na sekundo $[PPM]$=mikrosekunde na sekundo
Problem: kristali niso iste oblike $\rightarrow$ zamiki $\rightarrow$ potrebna sinhronizacija
#### Atomska ura
Cezij zaniha ~$9*10^9$-krat na sekundo $\rightarrow$ natančnost na 1s v 3M letih
==TAI== (Time Atomic International): povprečje >300 atomskih ur
#### Astronomska ura
Gibanje zemlje $\rightarrow$ manj natančno $\rightarrow$ potrebno usklajenvanje s prestopnimi sekundami
==UTC==: Linux - sekunde od `1.1.1970` / Windows - sekunde od `1.1.1601`
#### Sinhronizacija ur po protokolu NTP (Network Time Protocol)
Strežniki (atomska ura / sprejemnik GPS) sporoča usklajen čas
Odjemalci morajo upoštevati zamike ob zahtevi: čas potovanja zahteve, procesiranja in potovanja odgovora
![[Modeli porazdeljenih sistemov-Image-1.png|250]]
Izračun zamika ure:
$$
\Omega=t_s-t_4=\frac{(t_2-t_1+t_3-t_4)}{2}
$$
Izboljšana natančnost: povprečimo večkratne odgovore enega/več strežnikov
Popravljanje ure:
- $\Omega<125ms$ $\rightarrow$ odjemalec uro počasi sprotno popravlja
- $125ms\leq \Omega < 1000s$ $\rightarrow$ odjemalec uro takoj nastavi na novo vrednost
- $\Omega\geq 1000s$ $\rightarrow$ odjemalec zazna napako in ne naredi ničesar
### Logične ure
Merjenje časa v dogodkih: ob dogodku algoritem določi logični ==časovni žig==
Dogodek $X$ se je zgodil pred dogodkom $Y$:
- $X$ in $Y$ tečeta na istem procesu in $X$ se je zgodil pred $Y$
- $X$ je pošiljanje sporočila in $Y$ je prejemanje sporočila
- obstaja dogodek $Z$, ki se je zgodil po $X$ in pred $Y$
#### Lamportova ura
==Sinhronizacijska točka==: pošiljanje sporočila - dogodki pred sinh. točko so se zgodili pred dogodki za sinh. točko

Vsak proces ima svoj števec dogodkov, ob vsakem dogodku `števec++`
- pošiljanje sporočila: `števec++`, števec pripnemo sporočilu
- prejem sporočila: `števec=max(števec, števec_iz_sporočila)`, `števec++`
Dva nepovezana dogodka imata lahko isti časovni žig $\rightarrow$ ne moremo določiti vzročne povezanosti vseh dogodkov ali zaznati sočasnosti dogodkov
#### Vektorska ura
Vsak proces ima svojo tabelo števcev, ob vsakem dogodku `števci[moj]++`
- pošiljanje sporočila: `števci[moj]++`, tabelo števcev pripnemo poročilu
- prejem sporočila: za vse števce `števci[i]=max(števci[i], števci_iz_sporočila[i])`, `števec[moj]++`

$X$ se je zgodil pred $Y$, če:
- vsi števci tabele $X$ $\leq$ istoležni števci tabele $Y$
- vsaj en števcev tabele $X$ < istoležni števec tabele $Y$
## Protokoli za razširanje sporočil
#### Dostava po najboljših močeh
Sporočilo na nivoju omrežne opreme (IP multicast) pošljemo vsem vozliščem
Zagotavlja, da sporočila dobijo vsa delujoča vozlišča
#### Zanesljiva dostava sporočil
Sporočilo pošljemo vsakemu procesu posebej, ob napaki ga pošljemo ponovno
##### Nestrpno razširjanje
Proces prvič prejme sporočilo $\rightarrow$ ==prepošlje ga vsem ostalim procesom==
Neučinkovito: vsak izmed $n$ procesov prejme $n-1$ enakih sporočil - $O(n^2)$
##### Razširanje z govoricami
Proces prvič prejme sporočilo $\rightarrow$ ==prepošlje podanemu številu naključnim procesom==
Verjetnost za zgrešitev zelo majhna, a $O(n)$
#### Vrstni red dostave
##### Razširjanje FIFO
Sporočila posameznega procesa morajo biti dostavljena v enakem vrstnem redu, kot so bila poslana (vrstni red sporočil različnih procesov je poljuben)
##### Popolnoma urejeno razširjanje
Sporočila so vsem procesom dostavljen v enakem vrstnem redu, ki pa je lahko poljuben
##### Popolnoma urejeno FIFO razširjanje
Zlitje popolnoma urejenega in FIFO razširjanja
##### Vzročno razširjanje
Sporočila različnih procesov morajo biti dostavljena v enakem vrstnem redu, kot so bila poslana (vrstni red sporočil v primeru istočasnega pošiljanja je poljuben)