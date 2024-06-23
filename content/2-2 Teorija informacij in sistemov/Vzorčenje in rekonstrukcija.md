[[Signali in sistemi#Teorem vzorčenja|Teorem vzorčenja]]
### Rekonstrukcija signala
Funkciji $X(\nu)=\frac 1{2\nu_c}$ v frekvenčnem prostoru ustreza funkcija $x(t)=\frac{sin(2\pi\nu_ct)}{2\pi\nu_ct}$ v časovnem prostoru
Funkcijo zamaknemo, da ima center v točki vzorčenja $\rightarrow$ rekonstrukcija dejanskega signala:
$$
x(t)=\sum_{k=0}^{\infty}x_k\frac{sin(\pi\nu_c(t-k\Delta))}{\pi\nu_c(t-k\Delta)}
$$

Če ne vzorčimo dovolj pogosto, se začnejo frekvence prekrivati

Dlje časa vzorčimo, lepši frekvenčni spekter signala dobimo
Koliko časa vzorčiti, da v frekvenčnem spektru ločimo bližnje vrhove?
Osnovna frekvenca:
$$
\nu_0=min_{a\ne b} \ |\nu_b-\nu_a| \ \ \rightarrow \ \ T=\frac 1{\nu_0}
$$
Št vzorcev, ki jih potrebujemo:
$$
N=\frac T\Delta=\frac{\nu_s}{\nu_0}
$$