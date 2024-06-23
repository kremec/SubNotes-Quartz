Kanal lahko povzroči napake v podatkih (npr. šum) $\rightarrow$ sporočila opremimo z dodatnimi podatki za preverjanje in/ali popravljanje napak
### Diskretni kanal brez spomina
==Prehodna / pogojna verjetnost== - če smo imeli na vhodu $x_i$, da je iz kanala prišel $y_j$
$$
p(y_j)=\sum_{i=1}^{r}p(x_i)*p(y_j/x_i)
$$
$$
\sum_{j=1}^{s}p(y_j/x_i)=1
$$
==Vezana verjetnost==:
$$
\sum_{i=1}^{r}\sum_{j=1}^{s}p(x_i,y_j)=1
$$
### Obrat kanala
==Bayesovo pravilo== - če smo dobili iz kanala $y_j$, kako verjetno je bil poslan $x_i$
$$
p(x_i/y_j)=\frac{p(x_i)*p(y_j/x_i)}{p(y_j)}
$$
### Pogojna entropija
Verjetnost za nek $y$ pr nekem $x_i$:
$$
H(Y/X=x_i)=-\sum_{j=1}^{s}p(y_j/x_i)*log_r(y_j/x_i)
$$
Verjetnost za nek $y$ pri kateremkoli $x$:
$$
H(Y/X)=-\sum_{i=1}^{r} p(x_i)*H(y/X=x_i) = -\sum_{i=1}^{r}\sum_{j=1}^{s}p(x_i, y_j)*log_r(p(y_j/x_i))
$$

$$
0\leq H(Y/X)\leq H(Y)
$$
### Vezana entropija
$$
H(X,Y)=-\sum_{i=1}^{r}\sum_{j=1}^{s}p(x_i,y_j)*log(p(x_i,y_j))
$$
### Medsebojna informacija
![[TIS_Kanal_Venn.png|300]]
![[TIS_Kanal_Kanal.png|350]]
<div style="page-break-after: always;"></div><br><br>

### Kapaciteta kanala
$$
C=max \ I(X;Y)
$$
Kapaciteto kanala maksimiziramo preko verjetnosti vhdonih znakov

==Binarni Simetrični Kanal==: $C = 1-H(p, 1-p)$
![[TIS_Kanal_BSK.png|200]]
==Binarni Kanal z Brisanjem (BEC)==: $C=1-p$
![[TSI_Kanal_BEC.png|200]]
### II. Shannnov teorem
Združevanje znakov v bloke $\rightarrow$ bolj verjeten zanesljiv prenos
Več kontroolnih bitov $\rightarrow$ večja zanesljivost, a počasneje

==Histrost koda==:
$k$ podatkovnih bitov, $m$ kontrolnih bitov, $n$ vseh poslanih bitov v bloku; $M$ št. različnih kodnih zamenjav
$$
R= \frac{max \ H(X^n)}{n}=\frac{log(M)}{n}
$$
==Za== $R\leq C$ ==obstaja kod, ki zagotavlja tako prevajanje informacije, da je verjetnost napake pri dekodiranju poljubno majhna==
Za $R\gt C$ tak kod ne obstaja