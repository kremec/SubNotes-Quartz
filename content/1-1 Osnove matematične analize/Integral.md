## Nedoločeni integral
Funkcija $F$ je ==nedoločeni integral== [[Funkcije|funkcije]] $f$, če velja: $F'(x)=f(x)$ - [[Odvod|odvod]] integrala je osnovna $f$
Nedoločeni integral je na vsakem intervalu določen do konstante natančno: $(f(x)+C)' = f'(x)$ (glej [[Odvod#Osnovni odvodi in pravila odvajanja|pravila odvajanja]]) $\rightarrow$ oba $f(x)$ in $f(x)+C$ sta nedoločena inetgrala
### Osnovni integrali in pravila nedoločenega integriranja
$$
\begin{aligned} \int a \ dx&=ax+C \\ \int x^n \ dx&=\begin{cases} \frac{x^{n+1}}{n+1} + C \ \ \ ; n \ne -1 \\ ln|x|+C \ \ \ ;n=-1 \end{cases} \\ \int a^x \ dx&=\frac{a^x}{ln\ a}+C \\ \int sin\ x \ dx&=-cos\ x + C \\ \int cos\ x \ dx&=sin\ x + C \\ \int log_ax \ dx&=xlog_ax-\frac x{ln\ a} + C \end{aligned}
$$
- Linearnost: $\int (f(x)+\alpha*g(x)) \ dx=\int f(x) \ dx + \alpha*\int g(x) \ dx$
- Vpeljava nove spremenljivke
- Integriranje po delih - ==per partes==: $\int u \ dv = uv-\int v \ du$
- Parcialni ulomki: $\frac{Ax+B}{(x-a)(x-b)}=\frac{\alpha}{(x-a)}+\frac{\beta}{(x-b)}$ ... izrazi $\alpha$ in $\beta$ kot dela originalne funkcije in novo vsoto ulomkov vnesi v originalen integral
- [[Odvod#Taylorjev polinom|Taylorjeva vrsta]]: na območju konvergence Taylorjeve vrste lahko vrsto členoma integriramo
## Določeni integral
==Riemannova vsota==: $I_n=\sum_{i=1}^n\Delta_nx \ \ ; x\in[a+(i-1)\Delta_nx, a+i\Delta_nx]$
Določen integral funkcije $f$ na intervalu $[a,b]$: $lim_{n\to \infty}I_n=\int_a^bf(x) \ dx$
Funkcija $f$ je ==integrabilna== $\iff$ obstaja določeni integral
Vsaka zvezna funkcija je integrabilna
![[OMA_Integral_DoločeniIntegral.png|400]]
### Pravila določenega integriranja
$$
\begin{aligned} \int_a^b (\alpha*f(x)+g(x)) \ dx&=\alpha*\int_a^b f(x) \ dx + \int_a^b g(x) \ dx \\ \int_a^b f(x)\ dx &= -\int_b^af(x)\ dx \\ \int_a^b|f(x)|\ dx &\ge |\int_a^bf(x)\ dx| \\ \int_a^bf(x)\ dx &= \int_a^cf(x)\ dx + \int_c^bf(x)\ dx \\ \text{f liha}\ &\implies \int_{-a}^af(x)\ dx = 0 \\ \text{f soda}\ &\implies \int_{-a}^af(x)\ dx = 2*\int_0^af(x)\ dx \\ \mu(f)&=\frac{1}{b-a}*\int_a^bf(x)\ dx \end{aligned}
$$
==Newton-Leibnitzova formula==: $F$ ... nedoločeni integral $f$
$$
\int_\alpha^\beta(x)\ dx=F(\beta)+c-(F(\alpha)+c) = F(\beta)-F(\alpha)
$$
### Prostornina vrtenine
![[OS_Integral_Vrtenina.png|400]]
Prostornina: $V=\pi*\int_a^bf^2(x)\ dx$
Površina plašča: $P=\pi*\int_a^bf(x)\sqrt{1+(f'(x))^2}\ dx$
Dolžina krivulje: $l(\gamma)=\int_a^b||\gamma'(t)||\ dt$
## Posplošeni integral
![[OMA_Itegral_PosplošeniIntegral.png|300]]
Integral do pola: $\int_a^bf(x)\ dx = \lim_{t\searrow a}\int_t^bf(x)\ dx$
Integral v neskončnosti: $\int_a^\infty f(x)\ dx = \lim_{t\nearrow \infty}\int_a^tf(x)\ dx$