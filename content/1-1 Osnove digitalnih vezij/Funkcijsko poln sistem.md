[[Izjave#Polnost nabora izjavnih veznikov|Funkcijsko poln sistem]]: množica funkcij (operatorjev), s katerimi lahko realiziramo katerokoli preklopno funkcijo
Osnovni funkcijsko polni sistem: $(\land \ , \lor \ , \ \overline{ })$
Izpeljani funkcijsko polni sistemi: $(\lor \ , \ \overline{ }), \ (\land \ , \ \overline{ }), \ (\downarrow), \ (\uparrow), \ (\implies , 0) \ (\iff, \lor \ ,0)$ 

Množica $M$ je ==zaprt razred==, če s funkcijo $f\in M$ ne moremo realizirati nobene druge funkcije, ki ne bi bila vsebovana v množici $M$
Osnovni zaprti razredi:
- $T_0$ - ==razred ohranja ničle==: $f(0,...,0)=0$
  Vstaviš same $0$ v funkcijo
- $T_1$ - ==razred ohranja ničle==: $f(1,...,1)=1$
  Vstaviš same $1$ v funkcijo
- $S$ - ==razred sebidualnih funkcij==: $\overline{f(\overline{x_1}, \ ..., \ \overline{x_n})} = f(x_1, \ ..., \ x_n)$
  Analitično: Funkcijo v PDNO razpišeš z $x$-i, nato negiraš vsakega posebaj in celoten izraz
  Tabelarično: Spišeš resničnostno tabelo funkcije, preverjaš $f(\vec{w_i})\ne f(\vec{w_{2^n-1-i}})$
- $L$ - ==razred linearnih funkcij==: $f(x_1, \ ..., \ x_n)=a_0\triangledown a_1x_1 \triangledown ... \triangledown a_nx_n$
  Izračunaš vse $a_i$ in preveriš vse enačbe
- $M$ - ==razred popolnoma monotonih funkcij==: $\vec{w_i}\lt \vec{w_j} \implies f(\vec{w_i})\lt f(\vec{w_j})$
  Izbrani vektor $\vec{w_i}$ mora biti bitno manjši od $\vec{w_j}$

Funkcijski nabor je funkcijsko poln, če funkcije odpirajo vse zaprte sisteme - vsaj ena funkcija iz funkcijskega nabora ne sme pripadati vsakemu od zaprtih sistemov