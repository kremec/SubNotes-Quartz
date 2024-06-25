# Zaporedja
==Zaporedje==: preslikava $\mathbb N \mapsto \mathbb R$ oz. $n \mapsto a_n$
$$
(a_n)_n=(a_1,a_2, \ ...)
$$
Podajanje zaporedij:
- ==eksplicitno==: $a_n=f(n) \ ; \ f:\mathbb N \mapsto \mathbb R$
- ==rekurivno==: $a_{n+k}=f(a_n,a_{n+1}, \ ... \ , a_{n+k})$

> [!info]- Collatzeva domneva / domneva 3n+1
> Za poljubno pozitivno celo število sta na voljo dve operaciji:
> - če je število sodo, se ga deli z 2
> - če je število liho, se ga pomnoži s 3 in prišteje 1
>
> Domneva se glasi: tako določeno zaporedje so bo končalo s številom 1, ne glede katero je izbrano prvo število
> Še do zdaj ni rešena
> Več: [YT - Veritasium](https://youtu.be/094y1Z2wpJg?si=1IwBOJ79MTEjxvUE)

==Aritmetično zaporedje==: $a_n=a_0+n*d \ ; \ a_0,d\in \mathbb R$
==Geometrijsko zaporedje==: $a_n=a_0*q^n \ ; \ a_0,d\in \mathbb R$

Zaporedje je: (podobno kot pri [[Števila, indukcija, absolutna vrednost#Števila|številskih množicah]])
- ==navzgor omejeno==: obstaja zgornja meja, najmanjša zgornja meja je ==supremum== $sup(a_n)$
- ==navzdol omejeno==: obstaja spodnja meja, največja spodnja meja je ==infimum== $inf(a_n)$
- ==omejeno==: je omejeno navzgor in navzdol
- ==(strogo) naraščajoče==: $a_{n+1} \ (\geq)\gt \ a_n$
- ==(strogo) padajoče==: $a_{n+1} \ (\leq)\lt \ a_n$
- ==monotono==: je naraščajoče ali padajoče
# Limite in konvergenca
$\lim_{n\rightarrow \infty}a_n=a$ : $a\in \mathbb R$ je ==limita zaporedja== $(a_n)_n$, če $\forall \epsilon\gt 0 \exists N\in\mathbb R: \ |a_n-a|\lt \epsilon, \ \forall n\geq N$

==Konvergentno zaporedje==: ima limito
==Divergetno zaporedje==: nima limite
Vsako konvergentno zaporedje je omejeno
Izreki o konvergenci:
1. $\forall n\in N \ : \ a_n\leq b_n\leq c_n, \lim_{n\rightarrow \infty}a_n=\lim_{n\rightarrow \infty}c_n=a \ \implies \ \lim_{n\rightarrow \infty}b_n=a$
2. naraščajoče zaporedje $a_n$ limitira v $sup(a_n)$, če je navzgor omejeno, sicer limitira v $\infty$
3. padajoče zaporedje $a_n$ limitira v $inf(a_n)$, če je navzdol omejeno, sicer limitira v $-\infty$

Primer:
$$
\lim_{n\rightarrow \infty}(1+\frac 1 n)^n=e
$$

Zaporedje:
- ==narašča preko vsake meje==: $\forall M\in \mathbb R \ \exists N\in \mathbb R \ : \ a_n\gt M, \ \forall n\in N$  oz.  $\lim_{n\rightarrow \infty}a_n=\infty$
- ==pada pod vsako mejo==: $\forall m\in \mathbb R \ \exists N\in \mathbb R \ : \ a_n\lt m, \ \forall n\in N$  oz.  $\lim_{n\rightarrow \infty}a_n=-\infty$

$$
\lim_{n\rightarrow \infty}n^a =
\left\{
	\begin{array}{ll}
		\infty &;\ a\gt 0 \ \ (divergira \ v \ \infty) \\
		1 &;\ a=0 \ \ (konvergira) \\
		0 &;\ a\lt 0 \ \ (konvergira) \\
		divergira &;\ sicer
	\end{array}
\right.
$$
- Seštevanje: $\lim_{n\rightarrow \infty}(a_n+b_n)=a+b$
- Množenje: $\lim_{n\rightarrow \infty}(a_n*b_n)=a*b$
# Vrste
==Vrsta==: simbolična vsota realnih števil $a_1+a_2+ \ ... \ = \sum_{n=1}^{\infty}a_n; \ a_n\in \mathbb R$
$m$-ta delna vsota $S_m=a_1+a_ 2+ \ ... \ +a_m=\sum_{n=1}^{m}a_n$

==Konvergentna vrsta==: zaporedje $(S_m)_n$ konvergira $\implies$ $\sum_{n=1}^\infty = \lim_{m\rightarrow \infty} a_m$
Če vrsta konvergira, potem grejo členi proti 0.
Obrat trditve n velja - ==harmonična vrsta==: $\sum_{n=1}^\infty \frac 1 n$ = ... [(dokaz divergence)](https://youtu.be/4yyLfrsSXQQ?si=JqurdL9esQaiG9LJ) ... = $\infty$

==Geometrijska vrsta==:
$$
\sum_{n=1}^\infty a_0*q^n = a_0*(q+q^2+ \ ...)=
\left\{
	\begin{array}{ll}
		\frac {a_0} {1-q} &;\ |q|\lt 1 \\
		divergira &;\ sicer
	\end{array}
\right.
$$
### Računanje konvergence
Računanje vrst: naj bosta $\sum_{n=1}^\infty a_n$ in $\sum_{n=1}^\infty b_n$ konvergentni.
Tedaj sta konvergentni:
- $\sum_{n=1}^\infty (a_n+b_n)=\sum_{n=1}^\infty a_n + \sum_{n=1}^\infty b_n$
- $\sum_{n=1}^\infty c*a_n=c* \sum_{n=1}^\infty a_n$

Dominiranje vrst: naj vrsta $\sum_{n=1}^\infty a_n$ dominira vrsto $\sum_{n=1}^\infty b_n$ :  $a_n\geq b_n \ ; \ \forall n\in \mathbb N$
Tedaj:
- $\sum_{n=1}^\infty a_n$ konvergira $\implies$ $\sum_{n=1}^\infty b_n$ konvergira  (če je omejena večja vrsta, bo tudi manjša)
- $\sum_{n=1}^\infty b_n$ divergira $\implies$ $\sum_{n=1}^\infty a_n$ divergira        (če je neomejena manjša vrsta, bo tudi večja)
#### Konvergenčni kriteriji
1. ==Kvocientni kriterij==: $L=\lim_{n\rightarrow \infty} \frac{a_{n+1}}{a_n}$
   - $L \lt 1 \implies$ vrsta $\sum_{n=1}^\infty a_n$ konvergira
   - $L \gt 1 \implies$ vrsta $\sum_{n=1}^\infty a_n$ divergira
2. ==Korenski kriterij==: $L=\lim_{n\rightarrow \infty} \sqrt[n]{a_n}$
   Tedaj:
   - $L\lt 1\implies$ vrsta $\sum_{n=1}^\infty a_n$ konvergira
   - $L\gt 1\implies$ vrsta $\sum_{n=1}^\infty a_n$ divergira
3. ==Leibnitzov kriterij==: naj $a_n$ pada proti $0$
   Tedaj $\sum_{n=1}^\infty  (-1)^n a_n$ konvergira