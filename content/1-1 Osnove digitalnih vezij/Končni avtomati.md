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
## Moorov avtomat
$A_{MO}=\{X,B,Z,\delta,\lambda \}$:
- $\delta: \ B\times X \rightarrow B$
- $\delta: \ B \rightarrow Z$

![[Končni avtomati-Image-4.png|400]]
## Mealyjev avtomat
$A_{ME}=\{X,A,Z,\delta,\lambda \}$:
- $\delta: \ A\times X \rightarrow A$
- $\delta: \ A \rightarrow Z$