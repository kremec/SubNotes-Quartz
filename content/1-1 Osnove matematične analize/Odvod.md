# Odvod funkcije ene spremenljivke
==Diferenčni kvocient==:
$$
dk=\frac{f(x_0+h)-f(x_0)}{h}
$$
==Odvod== [[Funkcije|funkcije]] $f$ v $x_0$: $f'(x_0)=\lim_{h\to\infty}dk$
==N-ti odvod== funkcije $f$: $f^{(N)})(x_0)=(f^{(n-1)})'(x_0)$
Če je $f$ odvedljiva, je tudi [[Funkcije#Limite funkcij in zveznost|zvezna]].
#### Osnovni odvodi in pravila odvajanja
$$
\begin{aligned} (a)'&=0 \\ (x^n)'&=n*x^{n-1} \\ (a^x)'&=a^x*ln\ a \\ (sin\ x)'&=cos\ x \\ (cos\ x)'&=-sin\ x \\ (log_ax)'&=\frac1{x*ln\ a} \end{aligned}
$$
$$
\begin{aligned} (\alpha*f+g)'&=\alpha*f'+g' \\ (f*g)'&=f'*g+f*g' \\ (f(g(x)))'&=f'(g(x))*g'(x) \\ (\frac fg)'&=\frac{f'*g+f*g'}{g^2} \end{aligned}
$$
### L'Hospitalovo pravilo
$$
\lim_{x\to c}f(x)=\lim_{x\to c}g(x)={0 \ ali \ \pm\infty} \ \ \implies \ \ \lim_{x\to c}\frac{f(x)}{g(x)} = \lim_{x\to c}\frac{f'(x)}{g'(x)}
$$
### Taylorjev polinom
Aproksimacija ($n+1$-krat odvedljivih) funkcij s Taylorjevim polinomom stopje $n$
$$
T_n(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2}(x-x_0)^2+ \ ... \ +\frac{f^{(n)}(x_0)}{n!}
$$
$T_n(x)$ je dobra aproksimacija, z največjo možno napako:
$$
R_n(x)=\frac{f^{(n+1)}(c)}{(x+1)!}(x-x_0)^{n+1}
$$
==Taylorjeva vrsta==: stopnjo aproksimacije $n$ pošljemo "v neskončnost":
$$
T(x)=\sum_{n=0}^\infty \frac{f^{(n)}(x_0)}{n!}(x-x_0)^n
$$
> [!example]- Taylorjeve vrste
> $$
> \begin{aligned} e^x&=\sum_{n=0}^\infty \frac{x^n}{n!} \\ cosx&=\sum_{n=0}^\infty (-1)^n \frac{x^{2n}}{(2n)!} \\ sinx&=\sum_{n=0}^\infty (-1)^n \frac{x^{2n+1}}{(2n+1)!} \end{aligned}
> $$
> $$
> e^{ix} = \sum_{n=0}^\infty \frac{(ix)^n}{n!} = \ ... \ = cosx + i*sinx
> $$
### Geometrijski pomen
1. Geometrijski pomen prvega odvoda:
	- $f'(x)>0$ $\rightarrow$ $f$ je v $x$ naraščajoča
	- $f'(x)<0$ $\rightarrow$ $f$ je v $x$ padajoča
	- $f'(x)=0$ $\rightarrow$ $x$ je ==stacionarna točka==:
		- $f''(x)>0$ $\rightarrow$ lokalni minimum
		- $f''(x)<0$ $\rightarrow$ lokalni maksimum
		- $f''(x)=0$ $\rightarrow$ lokalni minimum / lokalni maksimum / sedlo
2. Geometrijski pomen drugega odvoda:
	- $f''(x)>0$ $\rightarrow$ $f$ je v $x$ konkavna
	- $f''(x)<0$ $\rightarrow$ $f$ je v $x$ konveksna
	- $f''(x)=0$ in se predznak $f''$ v $x$ spremeni $\rightarrow$ $x$ je prevoj
# Odvod funkcij več spremenljivk
### Parcialni in smerni odvod
==Parcialni odvod== $f$ po $x$:
- naklonski koeficient (naklon) prereza grafa $f$ v smeri $x$ osi
- naklon najboljše linearne aproksimacije v smeri $x$
![[OMA_Odvod_ParcialniOdvod.png|500]]
$$
\begin{aligned} f_x(a,b)&=\frac{\partial f}{\partial x}(a,b)=lim_{h\to 0}\frac{f(a+h,b)-f(a,b)}{h} \\ f_y(a,b)&=\frac{\partial f}{\partial y}(a,b)=lim_{h\to 0}\frac{f(a,b+h)-f(a,b)}{h} \end{aligned}
$$

==Smerni odvod== je relativna sprememba funkcijske vrednosti $f(x_0,y_0)$ ob majhnem premiku iz točke v smeri vektorja $\vec e$, npr. $f_x=f_{(1,0)}$, $f_y=f_{(0,1)}$
$$
f_{\vec e}(a, b)=f_x(a,b)e_1+f_y(a,b)e_2
$$
### Diferenciabilnost
Funkcija $f$ je ==diferenciabilna== v $(a,b)\in D$, če:
$$
f(a+h_1,b+h_2)=f(a,b)+f_x(a,b)*h_1+f_y(a,b)*h_2+o(h_1,h_2)
$$
Diferenciabilnost določi (obstoj):
- tangentne ravnine na graf v točki $(a,b)$
- linearne aproksimacije
### Gradient
==Gradient== je vektor (smer in velikost=naklon) največje rasti funkcije $f$:
$$
\nabla f = grad\ f=(f_x,f_y)
$$
![[OMA_Odvod_Gradient.png|400]]
Gradient je v vseh točkah pravokoten na nivojnice: $\nabla f\cdot (x',y')=0$
> [!info]- Gradientni spust
> Iščemo globalni minimum funkcije, z začetnim približkom $x_1$
> $$
> x_{k+1}=x_k-\gamma*\nabla f(x_k)
> $$
> $\gamma$ ... hitrost učenja (learning rate)
> Uporaba pri učenju nevronskih mrež: [YT - 3Blue1Brown](https://youtu.be/IHZwWFHWa-w?si=FpnFvHJoTVg9CPXm)
### Stacionarne točke
Ekvivalentni pogoji, da je $A$ stacionarna točka: $f_x(A)=f_y(A)=0 \iff f_v(A)=0 \iff \nabla f(A)=0$
Vsak lokalni ekstrem je stacionarna točka (če ni na robu $D_f$)
==Hassova matrika==: uporabimo druge parcialne odvode (npr. $f_{xy}$ ... $f_x$ odvajamo po $y$):
$$
Hs=\begin{bmatrix} f_{xx} & f_{xy} \\ f_{yx} & f_{yy} \end{bmatrix}
$$
Izračunamo determinanto: $D(x_0,y_0)=f_{xx}*f_{xy} \ - \ f_{xy}*f_{yx}$
- $D(x_0,y_0)>0$ $\rightarrow$ $(x_0,y_0)$ je lokalni ekstrem:
	- $f_{xx}(x_0,y_0)>0$ $\rightarrow$ lokalni minimum
	- $f_{xx}(x_0,y_0)<0$ $\rightarrow$ lokalni maksimum
- $D(x_0,y_0)<0$ $\rightarrow$ $(x_0,y_0)$ je sedlo
### Vezani ektremi
==Vezani ekstrem== $f$ pri pogoju $g=0$ je ekstrem funkcije $f \ | \ g=0$ - ekstrem preseka funkcij
![[OMA_Odvod_VezaniEkstremi.png|400]]
Potreben pogoj za lokalni ekstrem: $\nabla f * (\text{tang na} \ g=0)=0 \ \iff \ \nabla f \ || \ \nabla g$
Standardna formulacija: ==Lagrangeva funkcija==:
$$
L(x,y,\lambda)=f(x,y)-\lambda * g(x,y)
$$
Stacionarne točke $L$ so kandidati za vezane ekstreme:
- $L_x=f_x-\lambda g_x = 0$
- $L_y=f_y-\lambda g_y = 0$
- $L_\lambda = g = 0$ (predpostavljen pogoj)
> [!info]- Lagrange
> Več na to temo: [YT - Khan Academy](https://youtu.be/yuqB-d5MjZA?si=Z0kOHDR_YIns2OUP)