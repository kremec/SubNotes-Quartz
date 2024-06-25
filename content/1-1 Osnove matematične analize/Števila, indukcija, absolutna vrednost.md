# Števila
==Naravna števila==: $\mathbb N=\{1,2,3, \ ...\}$
==Cela števila==: $\mathbb Z=\{... \ ,-2,-1,0,1,2, \ ...\}$
==Racionalna števila==: $\mathbb Q=\{ \frac p q ; \ p,q\in \mathbb Z \land q\neq 0 \}$
==Realna števila==: $\mathbb R$ predstavljajo vse točke na številski premici
==Iracionalna števila==: $\{ \mathbb R \setminus \mathbb Q \}$ (npr. $\sqrt 2, \pi, e, \ ...$)

Naj bo $A\subset \mathbb R, \ A\neq \emptyset$:
$A$ je ==navzdol omejena==, če obstaja zgornja meja za $A$: $M\in \mathbb R \ : \ M\geq a; \ \forall a\in A$
- ==Supremum== $sup(A)$: najmanjša zgornja meja omejene množice
   ==Maksimum== $max(A)$: supremum znotraj množice $A$

$A$ je ==navzgor omejena==, če obstaja spodnja meja za $A$: $m\in \mathbb R \ : \ m\leq a; \ \forall a\in A$
- ==Infimum== $inf(A)$: največja spodnja meja omejene množice
   ==Minimum== $min(A)$: infimum znotraj množice $A$
# Indukcija
Princip indukcije: Za $A\subseteq \mathbb N$ naj velja:
1. $n_0\in A$
2. $\forall k\in \mathbb N \ : \ k\in A \implies k+1\in A$

Tedaj torej velja $A=\{n_0,n_1, \ ...\}$

Shema uporabe:
Radi bi dokazali trditev $T(n)$ za $\forall n\in \mathbb N$
1. Dokažemo ==bazo indukcije==: dokažemo $T(prvi \ člen)$ 
2. Dokažemo ==indukcijski korak==: predpostavimo $T(k)$ in izpeljemo $T(k+1)$
# Absolutna vrednost
==Absolutna vrednost== $x\in \mathbb R$: oddaljenost $x$ od $0$:
$$
|x| =
\left\{
	\begin{array}{ll}
		x &;\ x \geq 0 \\
		-x &;\ x < 0
	\end{array}
\right.
$$