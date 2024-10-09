Ne moremo vsega znanja vključiti v program: nezmožnost predikcij vseh možnih situacij
$\rightarrow$ Samodejno izboljševanje algoritmov ob pridobivanju izkušenj
$\rightarrow$ Gradnja modela z analizo učnih podatkov
### Nadzorovano (supervised) učenje
Učni primeri so podani kot vrednosti vhodov in izhodov - označenih učnih primerov
$\rightarrow$ Učimo se funkcije, ki preslika vhode v izhode
$$
\begin{aligned} (x_1,y_1),...,(x_n,y_n) \ \ &... \ \ učni\ primeri \\ x_j \ \ &... \ \ atributi \\ y_j \ \ &... \ \ vrednost\ neznane\ funkcije\ y=f(x) \end{aligned}
$$
Naloga: najti funkcijo $h$ ... ==hipoteza==, ki je najboljši približek funkciji $f$
#### Klasifikacijski problemi
$y$ je ==diskretna== spremenljivka - ==razred== (končen nabor vrednosti)
Atributna predstavitev podatkov: vsak učni primer (vrstice) ima vrednosti atributov (stolpci)
#### Regresijski problemi
$y$ je ==zvezna== spremenljivka - ==označba== (npr. število)
#### Evalviranje hipotez
==Prostor hipotez== lahko vsebuje več hipotez, ki so konsistentne z učno množico
Dobra hipoteza je dovolj ==splošna==: pravilno napoveduje vrednost $y$ tudi za še nevidene primere
Kriteriji evalviranja hipotez: konsistentnost (z učnimi primeri), splošnost, razumljivost
Točnosti hipotez: TP, TN, FP, FN
Klasifikacija točnosti:
$$
\begin{aligned} CA=\frac{TP+TN}{TP+TN+FP+FN}=\frac{TP+TN}{N} \end{aligned}
$$
### Nenadzorovano (unsupervised) učenje
Učni primeri niso označeni (nimajo ciljne spremenljivke)
$\rightarrow$ Učimo se vzorcev v podatkih
### Spodbujevalno (reinforced) učenje
Agent se uči preko zaporedja nagrad in kazni