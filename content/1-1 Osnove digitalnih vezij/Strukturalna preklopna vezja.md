# Matrike in vektorji
#TODO-LINKS LA - osnove matrik in vektorjev
### Operacije nad vektorji
Vektorska redukcija po vrstici: $c=*/\vec{a_{1:n}}=a_1*...*a_n$
Vektorska redukcija po stolpcu: $c=*/\vec{a^{1:m}}=a^1*...*a^m$
Primer: $\lor/[1\ 1\ 0\ 1]=1\lor 1\lor 0\lor 1$
### Operacije nad matrikami
==1 operator==: $A*B$ - istoležne elemente matrik združiš z operatorjem $*$
> [!example]- Primer
> $$
> \begin{bmatrix} a_{11}& a_{12} \\ a_{21}& a_{22} \end{bmatrix} *
> \begin{bmatrix} b_{11}& b_{12} \\ b_{21}& b_{22} \end{bmatrix} =
> \begin{bmatrix} a_{11}*b_{11}& a_{12}*b_{12} \\ a_{21}*b_{21}& a_{22}*b_{22} \end{bmatrix}
> $$

==2 operatorja==: $A\circ*\ B$ - Kot navadno matrično množenje, pri katerem množenje zamenjamo z operatorjem $*$, seštevanje pa z operatorjem $\circ$
> [!example]- Primer
> $$
> \begin{bmatrix} a_{11}& a_{12} \\ a_{21}& a_{22} \\ a_{31}& a_{32} \end{bmatrix} \lor \ \land
> \begin{bmatrix} b_{11}& b_{12} \\ b_{21}& b_{22} \end{bmatrix} =
> \begin{bmatrix} a_{11}b_{11}\lor a_{12}b_{21} & a_{11}b_{12}\lor a_{12}b_{22} \\
> a_{21}b_{11}\lor a_{22}b_{21} & a_{21}b_{12}\lor a_{22}b_{22} \\
> a_{31}b_{11}\lor a_{32}b_{21} & a_{31}b_{12}\lor a_{32}b_{22} \\
> \end{bmatrix}
> $$
> Namesto $a_{ij}$ in $b_{ij}$ vnesi noter $0/1$ in poračunaj

==Negacija matrike== = negacija elementov

### Zapisi
==Pravilnostna tabela==:
![[Strukturalna preklopna vezja-Image-1.png|100]]
- $\vec{x}=[x_1,\ ...,\ x_n]$ ... vektor neodvisnih vhodnih spremenljivk
- $W=\begin{bmatrix} w_{0,1}& ...& w_{0,n} \\ ...& ...& ... \\ w_{2^n-1,1}& ...& w_{2^n-1,n} \end{bmatrix}$ ... matrika leve strani pravilnostne tabele
- $y=f(\vec x)$ ... funkcijska vrednost (skalar)
- $\vec f =[f_0,\ ...,\ f_{2^n-1}]^T$ ... vektor funkcionalnih vrednosti

==Vektor mintermov== $\vec m = [m_0,\ ...,\ m_{2^n-1}]=\vec{x} \ \land\equiv W^T$
==Vektor makstermov== $\vec M=[M_{2^n-1},\ ...,\ M_0]=\vec x \lor \triangledown \ W^T$
==PDNO== $f(\vec x)=\vec x \lor \land \ \vec f$
==PKNO== $f(\vec x)=\vec M \land \lor \ \vec f$
# Preklopna vezja
==Mintermski vhod/izhod==: samo eden od ($2^n$) vhodov je lahko naenkrat aktiven
### Kodirnik
Mintermski vhod se s kodirno matriko kodira v izhodno vrednost
$$
\vec y = \vec m \ \lor \equiv K
$$
![[Strukturalna preklopna vezja-Image-2.png|100]]
Primera kodirnikov: BCD kodirnik (16 vhodov v 4 izhode) in 8/3 kodirnik (8 vhodov v 3 izhode)
### Dekodirnik
Vhodna vrednost se z dekodirno matriko dekodira v mintermski izhod
$$
\vec m = \vec x \ \land \equiv D^T
$$
![[Strukturalna preklopna vezja-Image-3.png|100]]
### Multiplekser
Naslovni vektor $\vec m$ izbere vrednost vhodnega vektorja $\vec k$, ki se bo preslikal na izhod $y$
$$
y=\vec m \lor \land \ \vec{k^T}
$$
![[Strukturalna preklopna vezja-Image-4.png|150]]
Običajno pred naslovne vhode postavimo dekodirnik (zmanjšanje števila priključkov)
$$
y=(\vec x \ \land \equiv D^T) \lor \land \ \vec{k^T}
$$
![[Strukturalna preklopna vezja-Image-5.png|400]]
### Demultiplekser
Vhodna spremenljivka $y$ in naslovni mintermski vektor $\vec m$ dasta izhodni vektor $\vec k$
$$
\vec k = y\lor \land \ \vec m
$$
![[Strukturalna preklopna vezja-Image-6.png|150]]
Običajno pred naslovne vhode postavimo dekodirnik (zmanjšanje števila priključkov)
### Seštevalnik
![[Strukturalna preklopna vezja-Image-7.png|300]]
![[Strukturalna preklopna vezja-Image-8.png|140]]
## Realizacija preklopnih funkcij
Funkcijo razčlenjujemo po:
- vseh spremenljivkah $\rightarrow$ funkcijski ostanki zavzamejo vrednosti $0$ ali $1$
- $n-a$ spremenljivkah $\rightarrow$ funkcijski ostanki so izraženi iz preostalih spremenljivk
Funkcijske ostanke nato po shemi vežemo v multipleksor
> [!example]- Primer
> ![[Strukturalna preklopna vezja-Image-9.png]]