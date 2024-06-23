### Enostavni kodi
#### Ponavljajoči kodi
$L(n, 1)$: namesto enega pošljemo $n$ enakih znakov
![[TIS_VarnoKodiranje_PonavljajočiKodi.png|350]]
Kod je zelo počasen $\rightarrow$ naj se $n$ in $k$ povečueta hitreje kot $m=n-k$
#### Kontrolne vsote
Podatkovnim bitom dodamo nekaj ==paritetnih bitov== za preverjanje parnosti
Nastavljeni so, da je vsota bitov po modulu 2 fiksna vrednost ($0$ ali $1$)
#### Pravokotni in trikotni kod
==Pravokotni kod==: sodost po vrsticah in stolpcih
- Zaznavanje in popravljanje 1 napake

==Trikotni kod==: vsota elementov v stolpcu in vrstici s paritetnim bitom mora biti soda
- Zaznavanje in popravljanje 1 napake, a z manj kontrolnimi biti - boljša hitrost
![[TIS_VarnoKodiranje_PravokotniTrikotniKod.png|300]]
### Hammingova razdalja koda
==Hammingova razdalja med kodnima zamenjavama==: št. znakov, po katerih se razlikujeta (primerjaš 1., 2. itd. zaporedni znak in šteješ razlike)

==Hammingova razdalja koda==:
$$
d_H=min \ d(\vec{x_a}, \vec{x_b})
$$
Pove nam, koliko napak lahko:
- odkrijemo
$$
e_{MAX}=d_H-1
$$
- popravimo
$$
f_{MAX}=\lfloor \frac{d_H-1}{2} \rfloor
$$
### Hammingov pogoj
Da bi pravilno dekodirali vse kodne zamenjave, kjer je prišlo do $e$ ali manj napak, mora veljati:
$$
M \leq \frac{2^n}{\sum_{i=0}^{f} \binom n i}
$$
oz.
$$
št.\ različnih\ sporočil \leq \frac{vse\ možnosti}{velikost\ otoka}
$$
<br><br><br>
### Linearni bločni kodi
==Linearni bločni kodi== $L(n,k)$:
- vsota kodnih besed je kodna beseda
- produkt kodne besede s konstanto je kodna beseda (zato moramo imeti zmeraj kodno zamenjavo samih ničel)

==Hammingova razdalja linearnega koda== = št. enic v kodni zamenjavi z najmanj enicami
==Generatorska matrika==: $G$ dimenzij $k * n$
$$
\vec x = \vec z * G
$$
==Paritetna matrika==: $H$ dimenzij $m*n$ (dobimo jo iz enačb)
![[TIS_VarnoKodiranje_LinearniBločniKodi.png|450]]
$$
\vec x * H^T = 0 \iff H*\vec{x^t}=0
$$
$$
G*H^T=0
$$

==Sistematični kodi==: podatkovni in varnostni biti v $G$ so ločeni: $G=(I_k \ | \ A) \ \ oz. \ \ G=(A \ | \ I_k)$
#### Sindrom
Ko se v kanalu zgodijo napake, prejemnik zaradi njih ne more takoj preveriti podatkov
Izračunamo ==sindrom== in preverimo, kje se je zgodila napaka: $\vec s = \vec 0$ - ni napake, v primeru $\gt 1$ napak pa lahko poslabšamo
$$
\vec s = \vec y * H^T = \vec e * H^T
$$
Ker je verjetnost dveh (ali več) napak veliko manjša od verjetnosti ene napake, popravljamo samo enojne
### Hammingov kod
$H(2^m-1, 2^m-1-m)$ zna popraviti 1 napako
### Ciklični kodi
$C(n,k)$ je LBK, v katerem vsak krožni premik kodne zamenjave da drugo kodno zamenjavo, in nobena kodna zamenjava ne manjka
#### Zapis s polinomi
$$
x(p)=x_{n-1}p^{n-1}+ \ ... \ + x_1p + x_0
$$
Krožni premik polinoma za $i$ mest:
$$
x^i(p) = p^i*x(p) \ \ mod \ \ (p^n+1)
$$
#### Generatorski in paritetni polinom
$$
g(p)=1p^m+g_{m-1}p^{m-1}+ \ ... \ +g_1p+1
$$
Krožni premiki: $[g(p), p*g(p), p^2g(p), ...]$
$$
g(p)*h(p)=0 \ \ mod \ \ (p^n-1)
$$
$$
x(p)*h(p)=0
$$