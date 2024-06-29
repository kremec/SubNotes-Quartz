==Preklopne spremenljivke==: neodvisne spremenljivke $x_1$, ..., $x_n$ $\in \{0,1\}$
==Preklopna funkcija==: odvisna spremenljivka nad preklopnimi spremenljivkami $f(x_1,\ ...,\ x_n)\in \{0,1\}$

==Vhodni vektorji==: $\vec w_i$ predstavlja število $i$ v binarnem zapisu, pri čemer so $0$ in $1$ razporejene po preklopnih spremenljivkah
Primer: $\vec w_3 = (0, \ ..., \ 0,1,1)$ pomeni, da sta v tabeli najbolj desni spremenljivki v tem primeru nastavljeni na $1$, ostale pa na $0$
Vseh vhodnih vektorjev je $2^n$ - vse kombinacije nastavitev vrednosti $n$ spremenljivk
==Pravilnostna tabela==:
![[Preklopne funkcije in vezja-Image-1.png|250]]

==Logične funkcije==: za $n$ spremenljivk obstaja $2^{2^n}$ logičnih funkcij
==Logični simboli / operatorji==: (podobni/isti kot [[Izjave#Izjavni vezniki|izjavni vezniki]])
![[Preklopne funkcije in vezja-Image-3.png|400]]
![[Preklopne funkcije in vezja-Image-4.png|350]]![[Preklopne funkcije in vezja-Image-5.png|350]]
### Mintermi, makstermi, PDNO in PKNO
$$
x^w=\begin{cases} x \ \ \ ;w=1 \\ \overline x \ \ \ ;w=0 \end{cases}
$$
==Minterm==: Spremenljivke povezujemo s konjunkcijami in uporabljamo negacije
$$
m_i=x_1^{w_{1i}} \ ... \ x_n^{w_{ni}}
$$
==Maksterm==: Spremenljivke povezujemo z disjunkcijami in uporabljamo negacije
$$
M_{2^n-1-i}=x_1^{\overline {w_{1i}}} \ \lor \ x_n^{\overline {w_{ni}}}
$$
Primer: 3 spremenljivke
![[Preklopne funkcije in vezja-Image-2.png|450]]
Relacije med mintermi in makstermi:
$$
\begin{aligned}
\overline{m_i}&=M_{2^n-1-i} \\
\overline{M_i}&=m_{2^n-1-i}
\end{aligned}
$$

### Popolne normalne oblike
==Popolna disjunktivna normalna oblika (PDNO)==: disjunkcija osnovnih konjunkcij vseh (vhodnih) spremenljivk
$$
f(x_1, \ ..., \ x_n)=\bigvee_{i=0}^{2^n-1}m_if_i
$$
Primer zapisa: $f(x_1,x_2,x_3)m_1 \lor m_2 \lor m_4 \lor m_7 = \lor (1,2,4,7)$
==Popolna konjunktivna normalna oblika (PKNO)==: konjunkcija osnovnih disjunkcij vseh (vhodnih) spremenljivk
$$
f(x_1, \ ..., \ x_n)=\bigwedge_{i=0}^{2^n-1}(M_{2^n-1-i}\lor f_i)
$$
Primer zapisa: $f(x_1,x_2,x_3)M_7M_4M_2M_1 = \land (1,2,4,7)$
Pretvorba med PDNO in PKNO: dvojna negacija funkcije

==Popolna Shefferjeva normalna oblika (PSNO)==: Shefferjevi mintermi ($s_i=x_1^{w_{1i}}\uparrow ... \uparrow x_n^{w_{ni}}$), povezani s Shefferjevim operatorjem
$$
f(x_1, \ ..., \ x_n)=\uparrow_{i=0}^{2^n-1}(f_i\uparrow s_i)
$$
==Popolna Pierceva normalna oblika==: Piercevi makstermi ($P_{2^n-1-i}=x_1^\overline{w_{1i}}\downarrow ... \downarrow x_n^\overline{w_{ni}}$), povezani s Piercevim operatorjem
$$
f(x_1, \ ..., \ x_n)=\downarrow_{i=0}^{2^n-1}(f_i\downarrow P_{2^n-1-i})
$$

### Veitchev diagram
Obsega $2^n$ polj, vsako polje določa minterm, presečišče polj pa določa funkcijo
Uporablja se za zapis in [[Minimizacija preklopnih funkcij|minimizacijo funkcij]]
![[Preklopne funkcije in vezja-Image-6.png|250]]

Primer uporabe za minimizacijo:
![[Preklopne funkcije in vezja-Image-7.png|350]]
### Ločenje oz. Shannonov teorem
$$
\begin{aligned}
f(x_1, \ ..., \ x_n)&=f(0,x2, \ ..., \ x_n)\overline{x_1} \ \lor \ f(1,x2, \ ..., \ x_n)x_1 \\
f(x_1, \ ..., \ x_n)&=(f(0,x2, \ ..., \ x_n)\lor x_1)(f(1,x2, \ ..., \ x_n)\lor \overline{x_1})
\end{aligned}
$$
Če funkcijo po tem postopku ločimo po vseh spremenljivkah, pridemo do PDNO oblike funkcije
### Dekompozicija preklopne funkcije
Funkcijo razdlimo na dva dela, zaradi česar jo lahko (če je možno) realiziramo z manj elementi.
$$
f(x_1, \ ..., \ x_n)=g(h(x_1, \ ..., \ x_s),x_{s+1}, \ ..., \ x_n)
$$
Primer: $f(x_1,x_2,x_3,x_4,x_5)=x_1x_2x_3 \lor x_1x_2x_4 \lor x_1x_2x_5=x_1x_2(x_3 \lor x_4 \lor x_5)$
### Odvisnost funkcije od spremenljivke
$$
\frac{df\ (x_1,x_2,x_3)}{d\ x_i} = f(x_1, \ ...,0, \ ..., \ x_n) \ \triangledown \ f(x_1, \ ...,1, \ ..., \ x_n)=\begin{cases} 0 \ \ \ ;\text{funkcija ni odvisna od }x_i \\ 1 \ \ \ ;\text{funkcija je odvisna od }x_i \\ 0 \ \ \ ;\text{funkcija je odvisna od }x_i \text{ pod pogojem g}  \end{cases}
$$

### Variantnost preklopne funkcije
Funkcija je ==invariantna== za zamenjavo dveh spremenljivk, če se pri zamenjavi neodvisnih spremenljivk med seboj funkcijska vrednost ne spremeni:
$$
f(x_1,\ ...,\ x_i,\ ...,\ x_j,\ ...,\ x_n)=f(x_1,\ ...,\ x_j,\ ...,\ x_i,\ ...,\ x_n) \ \ \ ;\ i\ne j
$$
## Simetrične funkcije
Funkcija je:
- ==popolnoma simetrična==, če je invariantna za vse zamenjave
- ==delno simetrična==, če je invariantna samo pri nekaterih zamenjavah
- ==popolnoma nesimetrična==, če je neinvariantna za vse zamenjave
#### Simetrijska števila
Simetrijsko število $m$ $\iff$ $m$ enic v vektorju vhodnih spremenljivk
Popolnoma simetrična funkcija mora imeti enako vrednost pri vseh simetrijskih številih (če ne bi pomenilo, da obstaja transpozicija enic po vhodnih vrednostih, ki se ne bi skladala z ostalimi)
$f_{\{\vec{m}\}}(x_1, \ ...,\ x_n)$ - funkcija, simetrična pri simetričnih številih $\vec{m}$
> [!example]- Simetrična števila
> ![[Preklopne funkcije in vezja-Image-8.png|500]]
#### Lastnosti simetričnih funkcijah
Simetrične funkcije so tudi:
- Negacija simetrične funkcije
- Negacija vhodnih spremenljivk
- Dualna funkcija

Konjunkcija in disjunkcija ohranjata simetričnost
Ločenje ohranja simetričnost
### Testiranje simetričnosti
1. Testiranje vseh $2^n$ vhodnih naborov $(n-1)$ transpozicij
2. S pomočjo ==razširjenega Veitchevega diagrama== - številke v poljih predstavljajo število enic v vhodnem vektorju:
	1. Kot masko premikaš osnovni Veitchev diagram po razširjenem Veitchevem diagramu
	2. Če pokriva vsa enaka števila, je na ta števila simetrična, pri vhodu, kot razberemo iz pozicije zadnega minterma
	   Primer modre: pokrite so vse $1$ in $4$, minterm $m_{15}$ predstavlja $\overline{x_1}x_2\overline{x_3}x_4$ - zato je funkcija pri tem vhodu simetrična funkcija za simetrijska števila $1$ in $4$
![[Preklopne funkcije in vezja-Image-9.png|550]]