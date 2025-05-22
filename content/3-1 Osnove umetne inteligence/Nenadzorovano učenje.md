==Nenadzorovano učenje==: učni primeri niso označeni (atributi brez ciljne spremenljivke) $\rightarrow$ ==porazdelitev primerov v smiselne skupine== - učenje vzorcev v podatkih
Bolj subjektivno, a velikokrat ne moremo pridobiti označenih primerov

==Gručenje==: iskanje homogenih podskupin v učnih podatkih
### Hierarhično gručenje
Neznano št. iskanih gruč
Pristopa: ==združevalni== - od listov (najmanjših gruč) proti korenu (enotni gruči) / ==delilni== - obratno
Lastnosti:
- Normalizacija atributov
- Časovna zahtevnost: združevanje $O(n^2logn)$ + deljenje $O(2^n)$
![[Nenadzorovano učenje-Image-1.png]]
#### Merjenje razdalj
Med učnimi primeri: [[Nadzorovano učenje#Metoda k najbližjih sosedov|znane mere razdalj]]
Med učnim primerom in gručo / med gručami:
- razdalja med ==najbližjima primeroma - enojna povezanost== (single linkage)
- razdalja med ==najbolj oddaljenima primeroma - popolna povezanost== (complete linkage)
- ==povprečna razdalja med vsemi primeri - povprečna povezanost== (average linkage)
![[Nenadzorovano učenje-Image-2.png|250]]
### Metoda voditeljev (k-means gručenje)
Znano želeno št. gruč = $k$
1. ==Naključno priredi učne primere eni od gruč==
2. V vsaki gruči izračunaj ==centroid==: srednja točka po vrednosti atributov vseh primerov gruče
3. Spremeni pripadnost vseh primerov glede na najbližji centroid

Ponavljaj 2/3 do konvergence
Lastnosti:
- ne najdemo globalnega optimuma (odvisno od inicializacije)
- občutljivost na šum
- težka objektivna evalvacija
![[Nenadzorovano učenje-Image-3.png]]