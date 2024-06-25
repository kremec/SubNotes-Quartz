==Kompleksna števila==: $\mathbb C=\{a+bi; \ a,b\in \mathbb R\}$
- $i=\sqrt{-1}$
- $a$ - ==realni del imaginarnega števila== $Re(z)$
- $b$ - ==imaginarni del imaginarnega števila== $Im(z)$
### Operacije
- ==Konjugiranje==: $x=a+bi \ \rightarrow \ \bar x=a-bi$
- Seštevanje: $(a+bi)+(c+di)=(a+c)+(b+d)i$
- Množenje: $(a+bi)*(c+di)=(ac-bd)+(ad+bc)i$
- Deljenje: (pomnožimo števec in imenovalec s konjugirano vrednostjo imenovalca)
### Lastnosti:
- $|z|=|\bar z|$
- $\bar{\bar z}=z$
- $|z_1*z_2|=|z_1|*|z_2|$
- $\bar{z_1*z_2}=\bar z_1 * \bar z_2$
- $|z_1+z_2|\leq |z_1|+|z_2|$
- $\bar{z_1+z_2}=\bar z_1 + \bar z_2$
- $|z_2-z_1|$ ... razdalja med $z_1$ in $z_2$
### Načini zapisa
==Kartezični zapis==: $z=x+yi \ ; \ x,y\in \mathbb R$
==Polarni zapis==:
$$
\begin{aligned} z&=|z|*(cos(\varphi)+i*sin(\varphi))\\&=|z|*e^{i\varphi} \end{aligned}
$$
- $|z|=\sqrt{x^2+y^2}$ ... razdalja do $0$
- $\varphi=arctan \frac y x (+\pi)$ ... kot ($\pi$ dodamo v $3.$ in $4.$ kvadrantu)
- $e^{i\varphi}$ ... enotska krožnica

Množenje v polarnem zapisu:
$z_1=|z_1|*(cos\varphi_1+i*sin\varphi_1)$, $z_2=|z_2|*(cos\varphi_2+i*sin\varphi_2)$:
$z_1*z_2= \ ... \ = |z_1|*|z_2|*e^{i(\varphi_1+\varphi_2)}$

==Eulerjeva formula==: $e^{i\varphi}=cons\varphi+i*sin\varphi$

Za $\pm$ se splača uporabljati kartezični zapis, za množenje in korenjenje pa polarni zapis

Operacije v polarnem zapisu:
- Konjugiranje: $\bar z=\bar{r*e^{i\varphi}}=r*e^{-e\varphi}$
- Potenciranje - De Moivre: $z^n=(r*e^{i\varphi})^n=r^n*e^{in\varphi}$
- Deljenje: $\frac{z_1}{z_2}=\frac{r_1*e^i\varphi_1}{r_2*e^i\varphi_2}=\frac{r_1}{r_2} * e^{i(\varphi_1-\varphi_2)}$

Operacije v ravnini:
- Zrcaljenje preko $Re$: $z\mapsto \bar z$
- Zrcaljenje preko $0$: $z\mapsto -z$
- Razteg za faktor r: $z\mapsto z*r$
- Premik za $z_0$: $z\mapsto z+z_0$
- Vrtenje za kot $\varphi$: $z\mapsto z*e^{i\varphi}$

Korenjenje:
==Koreni enote==: rešitve $z^n=1$, rešitev je $n$ in tvorijo pravilni $n$-kotnik
$n$-ti koreni enote:
$$
\begin{aligned} z_n&=e^{i\frac{2k\pi}{n}} \\ w_i&=\sqrt[n]r*e^{i\frac{\varphi+2k\pi}{n}} \end{aligned}
$$