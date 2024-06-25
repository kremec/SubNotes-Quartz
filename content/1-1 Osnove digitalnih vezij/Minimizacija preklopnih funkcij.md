==Minimizacija preklopnih funkcij==: iskanje funkcije, ki uporablja čim manj veznih elementov (pri realizaciji tako porabimo manj čipov)

==Glavni vsebovalnik==: konjunktivni izraz, ki je disjunktivno vsebovan v opazovani funkciji tako, da ne obstaja noben krajši konjunktivni izra
==Sosednji konjunkciji== imata isti nabor spremenljivk, razlikujeta pa se samo po 1 negaciji
Primer: $x_1x_2\overline{x_3}$ in $\overline{x_1}x_2\overline{x_3}$
Sosednje konjunkcije lahko zaradi sosednosti opustimo
Primer: $x_1x_2\overline{x_3}\lor \overline{x_1}x_2\overline{x_3}=(x_1\lor \overline{x_1})x_2\overline{x_3} = x_2\overline{x_3}$
## Minimizacija
==Quinova metoda minimizacije==:
1. $f$ zapišemo z mintermi
2. Poiščemo sosednje konjunkcije, postopek iskanja sosednjih konjunkcij ponavljamo, dokler obstajajo
3. Poiščemo potrebne glavne vsebovalnike (konjunkcije ki ostanejo), iz potrebnih glavnih vsebovalnikov sestavimo minimalno obliko $f$
>[!example]- Quinova metoda
>![[Minimizacija preklopnih funkcij-Image-1.png|350]]
>![[Minimizacija preklopnih funkcij-Image-2.png|450]]

==Veitcheva metoda minimizacije==:
Sosednji mintermi so v [[Preklopne funkcije in vezja#Veitchev diagram|Veitchevem diagramu]] so kar v sosednjih poljih, pri čemer imajo mintermi na robi diagrama sosede tudi na drugi strani diagrama
![[Minimizacija preklopnih funkcij-Image-3.png|250]]
## Minimalne normalne oblike
==Minimalna disjunktivna normalna oblika (MDNO)==: dobimo jo z minimizacijo funkcije po zgornjih metodah
==Minimalna konjunktivna normalna oblika (MKNO)==:
1. Funkcijo negiramo
2. Dobljeno funkcijo minimiziramo (dobimo MDNO negirane funkcije)
3. Rezultat ponovno negiramo
4. S pomočjo [[Boolova algebra|DeMorganovega pravila]] jo pretvorimo v MKNO

## Minimizacija nepopolnih funkcij
Funkcija je lahko le ==delno definirana== - pri nekaterih mintermih funkcija ni določena
To nedefiniranost lahko pri minimizaciji upoštevamo kot $1$ ali $0$, kar je ugodneje za minimizacijo
Primer: Rdeč kvadrat predstavlja manjši izraz, kot če bi vzeli le posamezno enico
![[Minimizacija preklopnih funkcij-Image-4.png|250]]