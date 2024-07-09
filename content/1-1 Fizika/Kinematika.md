Vrste gibanja glede na tir:
- premo
- krivo (kroženje, nihanje, valovanje)

Vrste gibanja glede na hitrost:
- ==enakomerno gibanje== (hitrost se s časom ne spreminja)
![[Kinematika-Image-1.png|400]]
- neenakomerno gibanje - če se hitrost s časom spreminja linearno: ==enakomerno pospešeno/pojemajoče gibanje==
![[Kinematika-Image-2.png|400]]
### Enakomerno in enakomerno pospešeno gibanje
Določimo koordinatni sistem, da imamo 1D problem
$$
\begin{aligned} x&=x(t) \\ v&=\frac{dx}{dt} \\ a&=\frac{dv}{dt}=\frac{d^2x}{dt^2} \end{aligned}
$$
$$
\begin{aligned} v(t)&=v_0+\int_{t_0}^{t}a(t)\ dt=v_0+a_0t \\ x(t)&=x_0+\int_{t_0}^t v(t)\ dt=x_0+v_0t+\frac{at^2}{2} \end{aligned}
$$
$$
\begin{aligned} s&=vt \\ v_k^2&=v_z^2+2a(x-x_0) \end{aligned}
$$
### Prosti pad in navpični met
![[Kinematika-Image-3.png|100]]
Prosti pad:
$$
\begin{aligned} v&=v_0+gt=\sqrt{2gh} \\ h&=\frac{gt^2}{2}=h_0+v_0t \end{aligned}
$$
Navpični met:
$$
\begin{aligned} v^2&=v_0^2-2gh \\ t&=\sqrt{\frac{2h}{g}} \\ h_{max}&=\frac{v_0^2}{2g} \end{aligned}
$$
### Vodoravni in poševni met
Razdelimo na $x$ in $y$ komponento (2D problem)
- v $x$ smeri je gibanje enakomerno ($x$ komponenta začetne hitrosti)
- v $y$ smeri je gibanje enakomerno pospešeno (konstanten negativen gravitacijski pospešek $g$)
Vodoravni met:
![[Kinematika-Image-4.png|200]]
$$
\begin{aligned} x(t)&=v_xt \\ y(t)&=y_0-\frac{gt^2}{2} \end{aligned}
$$
Poševni met:
![[Kinematika-Image-5.png|300]]
$$
\begin{aligned} a_x&=0 \\ v_x&=v_{0x}=v_0\cos(\varphi) \\ x(t)&=v_0\cos(\varphi)t \\ \\ a_y&=-g \\ v_y&=v_0\sin(\varphi)-gt \\ y(t)&=v_0\sin(\varphi)t-\frac{gt^2}{2}=x\tan\varphi-\frac{gx^2}{2v_0^2\cos^2\varphi} \end{aligned}
$$
$$
\begin{aligned} x_{max}&=\frac{v_0^2\sin2\varphi}{g} \\ y_{max}&=\frac{v_0^2\sin^2\varphi}{2g} \end{aligned}
$$
### Kroženje
Beleženje lege s:
- kartezičnimi ($x,y$) koordinatami $\rightarrow$ $\vec r=(x(t),y(t))$
- [[Kompleksna števila#Načini zapisa|polarnimi]] ($r,\varphi$) koordinatami $\rightarrow$ $\vec r=(r(t),\varphi(t))=(R\cos\varphi,R\sin\varphi)$
  $w$ ... ==kotna hitrost==, $\alpha$ ... ==kotni pospešek==
![[Kinematika-Image-6.png|150]]
Veljajo vse splošne formule premega gibanja, pri čemer zamenjamo: $x\to \varphi$, $v\to w$, $a\to \alpha$
$$
\begin{aligned} a_t&=\alpha R \\ v&=wR \\ \vec v&=\vec w \times \vec r \\ \vec v&=(-Rw\sin\varphi, Rw\cos\varphi) \\ \vec a &=(-Rw^2\cos\varphi-R\alpha\sin\varphi, -Rw^2\sin\varphi+R\alpha\cos\varphi) \end{aligned}
$$

Smer vektorja hitrosti je vedno tangancialna na tir kroženja - se nenehno spreminja
> [!example]- Dokaz
> $$
> \vec v\cdot\vec r=v_xx+v_yy+v_zz=R^2w(-\sin\varphi\cos\varphi)+R^2w(\sin\varphi\cos\varphi)+0=0
> $$

Spreminjanje hitrosti opišemo z ==radialnim pospeškom==, ki je vedno usmerjen proti središču kroženja
$$
a_r=Rw^2=\frac{v^2}{R}=wv_0
$$
$$
\begin{aligned} l&=\varphi R \\ N&=\frac{\varphi}{2\pi} \end{aligned}
$$

Pri enakomernem kroženju vpeljemo še ==frekvenco== $\nu=\frac{w}{2\pi}$ in ==nihajni čas== $t_0=\frac{1}{\nu}$