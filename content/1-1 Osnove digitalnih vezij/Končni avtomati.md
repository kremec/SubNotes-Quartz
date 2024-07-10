## Splošni končni avtomati
==Končni avtomat== $A=\{X,Y,Z,\delta,\lambda \}$:
- $X$ ... neprazna končna množica vhodnih črk - ==vhodna abeceda==
- $Y$ ... neprazna končna množica notranjih črk - ==notranja abeceda==
- $Z$ ... končna množica izhodnih črk - ==izhodna abeceda==
- $\delta$ ... ==funkcija podajanja stanj==, ki na osnovi vhodne in notranje črke poda novo notranjo črko
  $D^1y=\delta (y, x) \ ; \ \ \ x\in X, \ y\in Y$
- $\lambda$ ... ==izhodna funkcija==, ki na osnovi vhodne in notranje črke poda izhodno črko
  $z=\lambda (y,x) \ ; \ \ \ x\in X, \ y\in Y$

![[Končni avtomati-Image-1.png|300]]
==Vhodna beseda==: časovno zaporedje vhodnih črk
==Notranja beseda==: časovno zaporedje notranjih črk kot posledica prehajanja stanj avtomata
==Zunanja beseda==: časovno zaporedje izhodnih črk kot posledica prehajanja stanj avtomata in vhodnih črk
### Diagram prehajanja stanj - grafična predstavitev
![[Končni avtomati-Image-2.png|500]]
### Tabelarična predstavitev
![[Končni avtomati-Image-3.png|350]]
## Moorovi in Mealyjevi končni avtomati
### Moorov avtomat
$A_{MO}=\{X,B,Z,\delta,\lambda \}$:
- $\delta: \ B\times X \rightarrow B$
  $D^1b=\delta(b,x)$
- $\lambda: \ B \rightarrow Z$
  $z=\lambda(b)$

![[Končni avtomati-Image-4.png|400]]
### Mealyjev avtomat
$A_{ME}=\{X,A,Z,\delta,\lambda \}$:
- $\delta: \ A\times X \rightarrow A$
  $D^1a=\delta(a,x)$
- $\lambda: \ A \rightarrow Z$
  $z=\lambda(a,x)$
![[Končni avtomati-Image-5.png|400]]
### Pretvorba Moorovega v Mealyjev avtomat
Začetno stanje Moorovega stanje je definirano, pri Mealyjevem avtomatu pa se pojavi šele pri prvi vhodni črki.
$\delta_{ME}(a,x)=\delta_{MO}(b,x)$
$\lambda_{ME}(a,x)=\lambda_{MO}(\delta_{MO}(b,x))$
### Pretvorba Mealyjevega v Moorov avtomat
Množico notranjih stanj Moorovega avtomata tvorijo pari notranjega stanja in izhodne črke Mealyjevega avtomata: $[a,z]\in B$
$\delta_{MO}([a,z],\ x)=[\delta_{ME}(a,x),\ \delta(a,x)]$
$\lambda_{MO}([a,z])=z$
## Ekvivalenca končnih avtomatov
Končna avtomata sta ekvivalentna, če imata pri istem vhodnem zaporedju črk enako izhodno zaporedje črk
Pri primerjavi Moorovega in Mealyjevega avtomata je potrebno paziti, da Mealyjev avtomat generira izhodno črko šele, ko se na vhodu pojavi prva vhodna črka - izhod je zakansnjen za 1 znak
## Vezava avtomatov
Zaporedno ali vzporedno vežemo vhode in izhode avtomatov
Novo stanje skupka avtomatov $[Y_1,Y_2]$
### Zaporedna vezava avtomatov
$X=X_1$ ,  $Y=Y_1\times Y_2$ ,  $Z=Z_2$
$\delta([Y_1,Y_2], x)=[\delta_1(Y_1,x), \delta_2(Y_2,\lambda_1(Y_1,x))]$
$\lambda([Y_1,Y_2],x)=\lambda_2(Y_2, \lambda_1(Y_1, x))$
### Vzporedna vezava avtomatov
$X_1\subseteq X$ ,  $X_2\subseteq X$ ,  $Y=Y_1\times Y_2$
$\delta([Y_1,Y_2], [x_1,x_2])=[\delta_1(Y_1,x_1), \delta_2(Y_2,x_2)]$
$\lambda([Y_1,Y_2],[x_1,x_2])=[\lambda_1(Y_1,x_1),\lambda_2(Y_2,x_2)]$
## Dekompozicija in minimizacija avtomatov
### Particije
$n$-bločna particija : $\pi =\{B_1, \ ..., \ B_n\}$
- Particija enote $\pi_e$ : vsi elementi so v enem bloku
- Particija niča $\pi_0$ : vsak element predstavlja svoj blok

Operacije:
- $\pi_i\cdot\pi_j=\{B_{i_1}\cap B_{j_1}, \ B_{i_1}\cap B_{j_2}, \ ..., \ B_{i_2}\cap B_{j_1}, \ ..., \ B_{i_n}\cap B_{j_m}\}$
- $\pi_i+\pi_j$  ...  če je v nekem bloku element, združiš vse bloke s tem elementom v en blok
### Minimizacija
