==Postulati - aksiomi==: nedokazljive osnovne predpostavke, iz katerih je možno izpeljati vse zakone matematičnega sistema
### Postulati Boolovih operatorjev
(Podobno kot pri [[Izjave#Izjavni vezniki|izjavnih veznikih]]):
- ==Zaprtost==: za vsak par elemntov iz množice S dobimo ob aplikaciji operatorja element, ki je prav tako iz S
$$
\begin{aligned} x,y\in X \ &\rightarrow \ x\lor y\in X \\ x,y\in X \ &\rightarrow \ xy\in X \end{aligned}
$$
- ==Nevtralni element== $e$: velja $e*x=x*e=x$
$$
\begin{aligned} x,0\in X \ &\rightarrow \ x\lor 0=x \\ x,1\in X \ &\rightarrow \ x1=x= \end{aligned}
$$
- ==Komutativnost==: velja $x*y=y*x$
$$
\begin{aligned} x,y\in X \ &\rightarrow \ x\lor y=y\lor x \\ x,y\in X \ &\rightarrow \ xy=yx \end{aligned}
$$
- ==Distributivnost==: velja $x*(y\ \cdot\  z)=(x*y) \ \cdot \ (x*z)$
$$
\begin{aligned} x,y,z\in X \ &\rightarrow \ x\lor (yz)=(x\lor y)(x\lor z) \\ x,y,z\in X \ &\rightarrow \ x(y\lor z)=xy \lor xz \end{aligned}
$$
- ==Inverzni element==: $x$ ima nevtralni element $y$, če velja $x*y=y*x=e$
$$
\begin{aligned} \forall x\in X, \exists \overline x \ &\rightarrow \ x\lor \overline x=1 \\ \forall x\in X, \exists \overline x \ &\rightarrow \ x\overline x=0 \end{aligned}
$$
- ==Število elementov==: obstajata vsaj 2 elementa $x,y\in X$, da velja $x\ne y$
### Pravila Boolove algebre
(Podobno kot pri [[Izjave#Zakoni izjavnega računa|zakoni izjavnega računa]]):
- ==Idempotenca==:
$$
\begin{aligned} x\lor x\lor \ ... \ \lor x &= x \\ xx\ ...\ x&=x \end{aligned}
$$
- ==Absorpcija==:
$$
\begin{aligned} x\lor xy &= x \\ x(x\lor y)&=x \end{aligned}
$$
- ==Asociativnost==:
$$
\begin{aligned} (x\lor y)\lor z&=x\lor (y\lor z) \\ (xy)z&=x(yz) \end{aligned}
$$
- ==DeMorganov izrek==:
$$
\begin{aligned} \overline{x\lor y\lor \ ... \ \lor z}&=\overline x \overline y \ ... \ \overline z \\ \overline{xy \ ... \ z}&=\overline x \lor \overline y \lor \ ... \lor \overline z \end{aligned}
$$