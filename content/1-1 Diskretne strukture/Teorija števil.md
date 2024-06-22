### Deljivost celih števil
==Izrek o deljenju==: Naj bosta $m,n\in \mathbb{Z}$ in $m\gt 0$. Obstajata enolično določeni celi števili $k$ in $r$, pri čemer je:
$$n=k*m+r \ \text{ in velja } \ 0\leq r\lt m$$
- k ... ==kvocient== števil n in m: $k=[\frac n m]$
- r ... ==ostanek== pri deljenju števila n z m

Število $m$ ==deli== število $n$: $m|n \iff n=x*m \in \mathbb{Z}$
Primeri: $0|0$, $\mathbb{N}|0$, $3|12$
Če števili $m,n$ nista enaki $0$, potem lahko definiramo:
==Največji skupni delitelj== števil $m,n$: $gcd(m,n)=max\{d\in \mathbb{Z}; \ d|m \ in \ d|n\}$
==Najmanjši skupni večkratnik== števil $m,n$: $lcm(m,n)=min\{v\in \mathbb{Z}; \ m|v \ in \ n|v \ in \ v\gt 0\}$

Števili $m,n$ sta si ==tuji==: $a\perp b \iff gcd(a,b)=1$
- $a|(b*c) \land a\perp b \implies a|c$
- $a,b\in \mathbb{N} \implies gcd(a,b)*lcm(a,b)=a*b$

### Razširjeni Evklidov algoritem (REA)
Iščemo $gcd(m,n)$ in koeficienta $s,t$
Izrek: $gcd(m,n)=r=s*m+t*n$

Primer postopka na roke:
1. $m,n$ naj bosta velikostno urejena ($m\gt n$)
2. Prvi dve vrstici (enačbi $I$ in $II$) sta predpisani s koeficienti $(1,0)$ in $(0,1)$
3. Nato izračunamo ostanek naslednje vrstice: $r_{i+1}=r_{i-1} \ mod \ r_i$
Primer: $gcd(765,646)=?$
![[DS_TeorijaŠtevil_REA.png]]
Rezultat predzadnje vrstice ($17$) je $gcd$, pozitivni del vsote v zadnji vrstici ($29070$) pa je $lcm$

Koda #algoritem:
```c++
int gcd(int m, int n, int & s, int & t) {
    if (m == 0) {
        s = 0;
        t = 1;
        return n;
    }
    int s1, t1;
    int d = gcd(n % m, m, s1, t1);
    s = t1 - (n / m) * s1;
    t = s1;
    return d;
}
```
### Diofantske enačbe
==Diofantska enačba==: ima celoštevilske podatke in iščemo celoštevilske rešitve

==Linearna diofantska enačba== z dvema neznankama: enačba oblike $a*x+b*y=c$
Znani so $a,b,c\in \mathbb{Z}$ ($a,b$ ... koeficienta enačbe, $c$ ... desna stran), iščemo pa celoštevilsko rešitev $x,y$
Rešljiva je ntk. $gcd(a,b)|c$, sicer LDE nima rešitev

Naj par $x_0,y_0$ reši LDE $a*x+b*y=c$ in $d=gcd(a,b)$. Potem so:
$$\begin{aligned} x_t &= x_0+t*\frac b d \\ y_t&= y_0-t*\frac a d \end{aligned}$$
Primer: LDE $21x+9y=138$
![[DS_TeorijaŠtevil_LDA.png]]
Če linearno kombinacijo, ki vsebuje gcd, pomnožimo s $\frac {138} 3$, pridelamo zvezo:
$$46*21+(−92)*9=138$$
s čimer dobimo $x_0=46$ in $y_0=-92$, kar je rešitev osnovne enačbe, s formulama za $x_t,y_t$ pa dobimo še ostale možne rešitve.
### Praštevila
==Praštevilo==: naravno število $n \gt 1$ z natanko dvema pozitivnima deliteljema
==Praštevilska dvojčka==: par oblike $(p, p+2)$

==Klasičen evklidov izrek==: Obstaja neskončno mnogo praštevil
Iz $p_1, \ ..., \ p_n$ lahko zmeraj sestavimo novo praštevilo $p=p_1* \ ... \ *p_n + 1$

Vsak $n \geq 2 \in \mathbb{N}$ je deljivo s katerim od praštevil $\implies$
==Enolični razcep==: Vsak $n \geq 2 \in \mathbb{N}$ lahko zapišemo kot produkt praštevil

==Eulerjeva funkcija==: $\varphi(x)=|\{k\in \mathbb{N}; \ 1\leq k\leq n \land k\perp n\}|$ ... število števil med $1$ in $n$, ki so tuja $n$
- $p$ je praštevilo $\implies \varphi(p)=p-1$ oz. bolj splošno $\varphi(p^n)=p^n-p^{n-1}$
- $a\perp b \implies \varphi(a*b)=\varphi(a)*\varphi(b)$
Naj bo $n\in \mathbb{N}$ in $n=p_1^{k_1}*...*p_m^{k_m}$ njegov praštevilski razcep. Tedaj:
$$\varphi(n)=(p_1^{k_1}-p_1^{k_1-1})*...*(p_m^{k_m}-p_m^{k_m-1}) = n*(1-\frac 1 {p_1})*...*(1-\frac 1 {p_m})$$
### Konguence
==a mod b==: ostanek $a$-ja pri deljenju z $m$
==Kongruenca po modulu m==: [[Relacije|relacija]] $a\equiv b\pmod{m} \ \sim \ m|(a-b) \ \sim \ a \bmod m=b \bmod m$
1. Kongruenca po modulu je ekvivalenčna relacija v $\mathbb Z$
2. Če $a\equiv b\pmod m$, potem:
$$\begin{aligned} a\pm c&\equiv b\pm c \pmod m \\ a*c&\equiv b*c \pmod m \\ a^n&\equiv b^n \pmod m \end{aligned}$$
3. Če $a\equiv b\pmod m \ \land \ c\equiv d\pmod m$, potem:
$$\begin{aligned} a\pm c&\equiv b\pm d \pmod m \\ a*c&\equiv b*d \pmod m \end{aligned}$$
4. Če $a*c\equiv b*c\pmod m \ \land \ c\perp m$, potem:
$$a\equiv b\pmod m$$
5. Če sta $p,q$ različni praštevili, potem:
$$a\equiv b\pmod p \ \land \ a\equiv b\pmod q \iff a\equiv b\pmod{pq}$$
### Eulerjev izrek
Izrek: Naj bo $a\in \mathbb Z$, $m\geq 2 \in \mathbb N$, in $a\perp m$. Tedaj je:
$$a^{\varphi(m)}\equiv 1\pmod m$$
### Mali fermatov izrek
Izrek: Če je $p$ praštevilo in $a\perp p$, potem je:
$$a^{p-1}\equiv 1\pmod p$$
in za vse $a\in \mathbb Z$ velja:
$$a^p\equiv a\pmod p$$