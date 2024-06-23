Lastna informacija: opisuje dogodek, ki se je zgodil
==Lastna verjetnost==:
$$
I_i = -log_b(p_i)
$$
$b=\{2\rightarrow bit, \ 3\rightarrow trit, \ ...\}$ ... uporabljena baza

==Entropija==: ocena količine informacije / povprečje vseh lastnih verjetnosti
$$
H(X)=\sum_{i=1}^{n}p_iI_i
$$
Lastnosti:
- zvezna
- simetrična $\rightarrow$ vrstni red parametrov ni pomemben
- nenegativna (ker je $p_i\geq 0$)
- navzgor omejena z $log(n)$
- $p_i = \frac 1 n \implies H(X) = log(n)$
- neodvisna dogodka $\implies H(X*Y) = H(X,Y) = H(X) + H(Y)$
  neodvisna dogodka $\implies H(X,Y)\leq H(X) * H(Y)$