## Čas v preklopnih vezjih
Spreminjanje vrednosti spremenljivk lahko opazujemo v času:
![[Sekvenčna vezja-Image-1.png|500]]
### Časovni operator
Predstavlja premik vhodne spremenljivke v času za $k$ enot:
$$
D^kx=\begin{cases} x \ ; \ \ \ t=k \\ 0 \ ; \ \ \ t\ne k \end{cases}
$$
- $k=0$ ... sedanjost
- $k < 0$ ... preteklost
- $k > 0$ ... prihodnost

Lastnosti:
- $D^0x = x$
- $D^k(D^jx)=D^{k+j}x$
- $D^k(x_1*x_2)=D^kx_1*D^kx_2$ (velja za katerokoli funkcijo)
### Fronta
Sprememba nivoja spremenljivke v času:
- ==Prva fronta== $'x$: sprememba iz nizkega v visoko stanje (iz $0$ v $1$)
- ==Zadnja fronta== $x'$: sprememba iz visokega v nizko stanje (iz $1$ v $0$)

![[Sekvenčna vezja-Image-2.png|350]]
## Pomnilne celice
Pomnenje ~ ohranjanje stanja
#### Bistabil
Vezje lahko zavzame obe stabilni stanji izhoda
![[Sekvenčna vezja-Image-3.png|150]]
#### RS celica
Če razširimo bistabil dobmo Reset-Set pomnilno celico
![[Sekvenčna vezja-Image-4.png|500]]
$$
D^1q=\overline r q \lor s \ ; \ \ \ rs=0
$$
![[Sekvenčna vezja-Image-5.png|350]]
Če sta oba vhoda (set in reset) na logični enici, dobimo nestabilno (nedoločeno) stanje.
#### T pomnilna celica
Trigger pomnilna celica ima en vhod, katerega visoko stanje spremeni vrednost celice, pri nizkem stanju pa se ohranja
![[Sekvenčna vezja-Image-6.png|270]]
$$
D^1q=\overline tq  \lor t\overline q
$$
![[Sekvenčna vezja-Image-7.png|350]]
#### D pomnilna celica
Delay pomnilna celica ima en vhod; vrednost pomnilne celice je zakasnjena vrednost vhoda
![[Sekvenčna vezja-Image-8.png|280]]
$$
D^1q=d
$$
![[Sekvenčna vezja-Image-9.png|350]]
#### JK pomnilna celica
Jump-Kill pomnilna celica ima dva vhoda - $j$ brezpogojno nastavi vrednost celice, $k$ jo brezpogojno ponastavi, v primeru visoke vrednosti obeh vhodov pa se vrednost celice negira
![[Sekvenčna vezja-Image-10.png|600]]
$$
D^1q=q\overline k \lor \overline q j
$$
![[Sekvenčna vezja-Image-11.png|360]]
### Sinhrone pomnilne celice
Pri T in JK pomnilni celici je problem proženja vhodov, ki negirajo vrednost - uvedemo sinhronizacijo na urin impulz (izredno kratko trajanje visoke vrednosti)
> [!example]- Sinhroni RS in D pomnilni celici
> ![[Sekvenčna vezja-Image-12.png]]
> 
> ![[Sekvenčna vezja-Image-13.png]]
> $$
> D^1q=ud\lor \overline uq
> $$

### Pomnilne celice s predpomnenjem
Dobimo jih z zaporedno vezavo več pomnilnih celic
- Prva pomnilna celica spreminja svojo vrednost ob visokim urinem impulzu
- Druga pomnilna celica spreminja svojo vrednost ob nizkem urinem impulzu
- Do spremembe pride samo pri prehodu iz visokega v nizko stanje - zadnji urini fronti

> [!example]- D pomnilna celica s predpomnenjem
> ![[Sekvenčna vezja-Image-14.png|500]]
> $$
> \begin{aligned} D^1q_1&=ud\lor \overline uq_1 \\ D^1q_2&=uq_1\lor \overline uq_2 \end{aligned}
> $$

### Paralelno zajemanje podatkov
Ponavadi pomnilne celice vežemo skupaj - hranjenje več bitov hkrati, vezano na en urin signal
### Delilnik frekvence
Z JK celico lahko zgradimo delilnih frekvence:
![[Sekvenčna vezja-Image-15.png]]
$$
\nu_u = 2\nu_A = 4\nu_B
$$
#### Števec
Z JK celico lahko zgradimo števec - sestavljene vrednosti pomnilnih celic skozi čas predstavljajo dvojiško štetje
![[Sekvenčna vezja-Image-16.png]]
Taka izvedba ni najboljša, saj moramo zaradi zamika čakati $n$ period ure za pravilno nastavitev
#### Pomikalni register
Z D pomnilno celico zgradimo pomikalni register - začetno stanje pomnilnih celic se krožno premika
![[Sekvenčna vezja-Image-17.png]]
## Model sekvenčnega vezja
Splošen model:
![[Sekvenčna vezja-Image-18.png|300]]
- $\vec x$ ... vektor vhodnih spremenljivk
- $\vec z$ ... vektor izhodnih spremenljivk
- $\vec y$ ... vektor krmilnih spremenljivk
- $D^1\vec y$ ... vektor izhodov iz pomnilnih celic

SInhronizacija je izvedena z uro, ki vstopa v PC (pomnilne celice)