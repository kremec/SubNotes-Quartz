==Funkcija==: predpis ([[Relacije|relacije]]), ki vsakemu elementu $x$ iz ==definicijskega območja== $D_f\subset \mathbb R$ priredi natanko določeno število $f(x)\in \mathbb R$

==Graf funkcije== $f$ : krivulja v ravnini $G(x)=\{(x,f(x)); \ x\in D_f\}\subset \mathbb R \times \mathbb R$
Graf funkcije seka poljubno navpično premico v največ eni točki.
Projekcija grafa na os $x$ je $D_f$, projekcija grafa na os $y$ pa $Z_f$

Podajanje predpisa funkcij:
- ==eksplicitno==: $y=f(x)$                      (npr. $y=\sqrt{1-x^2}$)
- ==implicitno==: $F(x,y)=0$                   (npr. $x^2+y^2-1=0$)
- ==parametrično==: $x=x(t), \ y=y(t)$   (npr. $x=cos(t)$)
#### Operacije
- $x\mapsto f(x)+g(x)$  ... vsota $f+g$
- $x\mapsto f(x)-g(x)$  ... razlika $f-g$
- $x\mapsto f(x)*g(x)$   ... produkt $fg$
- $x\mapsto \frac{f(x)}{g(x)}$             ... kvocient $\frac f g$
- $(g\circ f)(x)=g(f(x)) \ ; \ Z_f\subseteq D_g$  ... kompozitum $f\circ g$
#### Transformacije
- $g(x)=f(x-a)$ ... vodoravni premik za $|c|$
- $g(x)=f(x)+c$ ... navpični premik za $|c|$
- $g(x)=f(\frac x a)$      ... vodoravni razteg/skrček za faktor $c$
- $g(x)=c*f(x)$  ... navpični razteg/skrček za faktor $c$
- $g(x)=-f(x)$    ... zrcaljenje preko $x$ osi
- $g(x)=f(-x)$    ... zrcaljenje preko $y$ osi

#### Lastnosti
(Podobno kot pri [[Relacije#Preslikave|preslikavah]]):
- ==soda==: $f(-x)=f(x) \ ; \ \forall x\in D_f$
- ==liha==: $f(-x)=-f(x) \ ; \ \forall x\in D_f$
- ==injektivna==: različni točki $x_1\neq x_2 \in D_f$ preslika v različni vrednosti $f(x_1)\neq f(x_2) \in Z_f$
- ==surjektivna==: $Z_f=\mathbb R$
- ==bijektivna==: injektivna in surjektivna

==Inverzna funkcija==: $f^{-1}(x)=y \iff f(y)=x$, $f$ mora biti injektivna
Izračun: zamenjamo vse $x$-e in $y$-e (dobimo $x=f(y)$) in izrazimo $y$ kot funkcijo $x$
Graf: prezrcalimo graf funkcije $f$ prekosimetrale lihih kvadrantov
### Limite funkcij
[[Zaporedja, vrste, limite#Limite|Limita]] funkcije: $\lim_{x\rightarrow a}f(x)=b \ \iff \ \forall\epsilon\gt 0 \ \exists \delta\gt 0 \ : \ \forall x\in (a-\delta,a+\delta)$ velja $f(x)\in(b-\epsilon,b+\epsilon)$
Naraščanje preko vseh meja: $\lim_{x\rightarrow a}f(x)=\infty$
Padanje pod vsako mejo: $\lim_{x\rightarrow a}f(x)=-\infty$
### Zveznost funkcij
Funkcija $f$ je zvezna v $a\in D_f$, če $f(a)=\lim_{x\rightarrow a}f(x)$
Primer nezvezne funkcije:
$$
sgn(x)=
\left\{
	\begin{array}{ll}
		1 &;\ x\gt 0 \\
		0 &;\ x=0 \\
		-1 &;\ x\lt 0
	\end{array}
\right.
$$

Lastnosti zveznosti:
- Vse elementarne funkcije (polinomi, eksponentne, trigonometrične, ...) so zvezne
- Če sta $f$ in $g$ zvezni v $a\in D_f$:
  - je graf $f$ nepretrgana krivulja
  - sta zvezni $f+g$ in $f*g$
  - lahko zamenjamo vrstni red računanja limite v $a$ in vrednosti funkcije
## Numerično reševanje enačb - iskanje ničel
==Bisekcija== - ideja: $f(a)*f(b)\lt 0\implies f$ ima ničlo na $[a,b]$
1. Izberemo začetna približka $a$ in $b$, in naj velja $f(a)*f(b)\lt 0$ (različno predznačena)
2. Induktivno izračunamo naslednje približke: $x_{n+1}=\frac{a_n+b_n}{2}$ (vmesna točka med levo in desno mejo iskanja)
3. $f(x_{n+1})=0 \ \rightarrow$  našli ničlo
   Sicer izberemo stran, pri kateri sta predznaka različna:
   $f(x_{n+1}*f(a_n)\lt 0 \ \rightarrow$  vzamemo $[a_n,x_{n+1}]$, saj je ničla nekje vmes
   $f(x_{n+1})*f(b_n)\lt 0 \ \rightarrow$  vzamemo $[x_{n+1},b_n]$, saj je ničla nekje vmes

==Regula falsi== - podobno bisekciji, drugačno (bolj optimalno) računanje približkov
1. Izberemo začetna približka $a$ in $b$, in naj velja $f(a)*f(b)\lt 0$ (različno predznačena)
2. Induktivno izračunamo naslednje približke: $x_{n+1}=\frac{a_n*f(b_n)-b_n*f(a_n)}{f(b_n)-f(a_n)}$ (presečišče premice čez izbrani točki približkov in x osjo)
3. $f(x_{n+1})=0 \ \rightarrow$  našli ničlo
   Sicer izberemo stran, pri kateri sta predznaka različna:
   $f(x_{n+1}*f(a_n)\lt 0 \ \rightarrow$  vzamemo $[a_n,x_{n+1}]$, saj je ničla nekje vmes
   $f(x_{n+1})*f(b_n)\lt 0 \ \rightarrow$  vzamemo $[x_{n+1},b_n]$, saj je ničla nekje vmes

Ta algoritem naj bi (ponavadi) našel ničlo hitreje kot pri bisekciji

==Sekantna metoda== - Regula falsi brez $f(a)*f(b)\lt 0$
1. Izberemo naključna začetna približka $x_1$ in $x_2$
2. Induktivno izračunamo naslednje približke: $x_{n+1}=\frac{x_{n-1}*f(x_1)-x_n*f(x_{n-1})}{f(x_1)-f(x_{n-1})}$ (v bistvu delamo [[Odvod#Taylorjev polinom|Taylorjevo aproksimacijo]] stopnje 1)
3. Upamo, da slednje konvergira k ničli

==Navadna iteracija==:
1. Določimo funkcijo $g$, katere negibna točka je ničla $f$
2. Upamo, da limita $g$ ničla $f$