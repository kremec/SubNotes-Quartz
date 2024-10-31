 Ne moremo vsega znanja vključiti v program: nezmožnost predikcij vseh možnih situacij
$\rightarrow$ Samodejno izboljševanje algoritmov ob pridobivanju izkušenj
$\rightarrow$ Gradnja modela z analizo učnih podatkov
## Vrste strojnega učenja
### Nadzorovano (supervised) učenje
Učni primeri so podani kot vrednosti vhodov in izhodov - označenih učnih primerov
$\rightarrow$ Učimo se funkcije, ki preslika vhode v izhode
$$
\begin{aligned} (x_1,y_1),...,(x_n,y_n) \ \ &... \ \ učni\ primeri \\ x_j \ \ &... \ \ atributi \\ y_j \ \ &... \ \ vrednost\ neznane\ funkcije\ y=f(x) \end{aligned}
$$
Naloga: najti funkcijo $h$ ... ==hipoteza==, ki je najboljši približek funkciji $f$
#### Vrste problemov
##### Klasifikacijski problemi
$y$ je ==diskretna== spremenljivka - ==razred== (končen nabor vrednosti)
Atributna predstavitev podatkov: vsak učni primer (vrstice) ima vrednosti atributov (stolpci)
##### Regresijski problemi
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
## Učenje odločitvenih dreves
### Odločitveno drevo
Model, ki ponazarja relacijo med atributi in odločitvijo / ciljno spremenljivko:
- notranja vozlišča - pogoji glede na vrednost atributa
- listi - odločitev
- pot - konjunkcija pogojev na poti do lista

Cilj: gradnja **čim manjšega drevesa**, ki je **konsistentno z učnimi podatki**
### Top Down Induction of Decision Trees
**Hevristični požrešni algoritev**:
- izberi najpomembnejše atribute - najbolj vpliva na klasifikacijo primera
- rekurzivno razdeli primere v poddrevesa glede na njihove vrednosti
- če vsi elementi v listu pripadajo istemu razredu, ustavi gradnjo
#### Iskanje najpomembnejšega atributa
**Entropija / nedoločenost**: (želimo jo znižati)
$$
H=-\sum_kp_k*log_2p_k \ \ [bit \ informacije]
$$
**Informacijski prispevek**: (želimo ga povečati)
$$
\begin{align} Gain(A)&=I-I_{res}(A) \\ I_{res}=\sum_ip_{v_i}*H(c/v_i)&=-\sum_ip_{v_i}*\sum_cp(c/v_i)*log_2(c/v_i) \end{align}
$$
$$
\begin{align} I \ ... \ &začetna \ entropija \\ I_{res} \ ... \ &residualna \ entropija \\ I(A) \ ... \ &entropija\ atributa \end{align}
$$
#### Večvrednostni atributi
Problem: informacijski prispevek precenjuje njihovo kakovost (višja entropija zaradi več vrednosti, namesto zaradi kakovosti)
Rešitve:
1. **Normalizacija** informacijskega prispevka - **relativni informacijski prispevek (information gain ratio)**:
$$
GainRatio(A)=\frac{Gain(A)}{I(A)}
$$
2. Uporaba **alternativnih mer** - **Gini index**:
$$
\begin{align} Gini&=\sum_{c_1\neq c_2}p(c_1)*p_(c_2) \\ Gini(A)&=\sum_vp(v)\sum_{c_1\neq c_2}p(c_1/v)*p(c_2/v) \end{align}
$$
3. **Binarizacija atributov** - zalogo vrednosti razbijemo v 2 množici
   (npr. {R, M, Z} $\rightarrow$ {{R}, {M, Z}})
#### Kratkovidnost
Požrešni algoritem izbira "lokalni" najboljši atribut, ne upošteva povezav med atributi, ki pripeljejo do optimalne rešitve
### Prostor hipotez
**Diskretni atributi**: odločitvena drevesa delijo prvotno množico na vse manjše podmnožice
**Zvezni atributi**: delitev podmnožice glede na smiselno mejo izbranega atributa
- v vozliščih testiramo primerjavo zveznega atributa z izbrano mejo
- prostor tako delimo na particije (hiper-kvadre), katerih meje so vzporedne koordinatnim osem
### Privzeta točnost
**Verjetnost večinskega razreda v učni množici**: smiselna mera minimalne pričakovane točnosti odločitvenega drevesa
Drevo je uporabno, če je njegova točnost **višja od privzete točnosti** (sicer samo uporabimo splošno bolj verjetno opcijo)
### Pristranost na učni množici
**Pretirano prilagajanje (overfitting)**: pri maksimizaciji pričakovane točnosti drevesa na učnih podatkih se lahko preveč prilagodimo učnim podatkom - **izgubimo splošnost**
Zato uporabimo **nevidene - testne primere**, ki jih vzamemo iz množice učnih primerov za sprotno preverjanje med gradnjo drevesa
## Učenje dreves iz šumnih podatkov
Nepopolni podatki z napakami $\rightarrow$ učenje šuma, slaba razumljivost, nižja klasifikacijska točnost, overfitting

Nižji deli drevesa simpolizirajo lokalno prilagajanje učnim podatkom in šumu $\rightarrow$ ==rezanje== teh delov posploši drevo
### Strategije rezanja
#### Rezanje vnaprej (forward pruning)
Uporaba dodatnega kriterija glede na obseg šuma za zaustavitev gradnje drevesa $\rightarrow$ ==hitrejše==, a ==kratkovidno==
#### Rezanje nazaj (post-pruning)
Po gradnji drevesa odstranimo manj zanesljive dele drevesa $\rightarrow$ ==počasnejše==, a upoštevamo informacijo ==celega drevesa==
##### Rezanje z zmanjšanjem napake (Reduced Error Pruning)
Uporaba ==rezalne/validacijske množice== primerne velikosti za zanesljivost (npr. vzamemo 30% učnih primerov)
Postopek:
1. potuj od vključno staršev listv drevesa navzgor
2. za vsako vozlišče izačunaj
$$
\text{dobitek rezanja = št. napačnih klasifikacij v listih - št. napačnih klasifikacij v vozlišču}
$$
3. $dobitek\geq0$ $\rightarrow$ obreži in nadaljuj s staršem; sicer ustavi postopek
##### Rezanje z minimizacijo napake (Minimal Error Pruning)
Uporaba učne množice (in ne ločene rezalne množice)
Cilj: minimizacija klasifikacijske napake $E$ / maksimizacija točnosti $CA$
Postopek:
1. Za vozlišče izračunamo:
    - ==statično napako== - verjetnost klasifikacije v napačen razred
$$
e(v)=p(razred\neq C/v)
$$
    - ==vzvratno napako== (backed-up error)
$$
\sum_ip_iE(T_i)=p_1E(T_1)+p_2E(T_2)+...
$$
2. Režemo, če: $\text{statična napaka < vzvratna napaka}$
3. Napaka optimalno obrezanega drevesa:
$$
\begin{align} E(T)&=e(v)\ &; \ \ v\ je\ list \\ E(T)&=min(e(v),\sum_ip_iE(T_i))\ &; \ \ sicer \end{align}
$$
### Ocenjevanje verjetnosti
==Relativna frekvenca==: $\frac nN$; $N$ ... št. primero v vozlišču, $n$ ... št. primerov, ki pripadajo večinskemu razredu $C$
Čeprav je lahko v študiji veliko primerov, je v listih pogosto malo primerov $\rightarrow$ ni dobra ocena (hitro spreminjajoča)

Potrebujemo ==oceno verjetnosti==: približek prave verjetnosti dogodka z zaželenimi matematičnimi lastnostmi in boljšo stabilnostjo
- smiselno je upoštevati ==apriorno verjetnost==: domensko znanje verjetnosti o problemu (npr. 50% pri metu kovanca)
#### Laplaceova ocena verjetnosti
==Ne upošteva apriorne verjetnosti==
$$
p=\frac{n+1}{N+k}
$$
- $n$ ... št. primerov v razredu C
- $N$ ... št. vseh primerov
- $k$ ... št. vseh razredov
#### m-ocena verjetnosti
Posplošitev Laplaceove ocene za $m=k$ in $p_a=\frac1k$
$$
p=\frac{n+p_am}{N+m}=p_a\frac{m}{N+m}+\frac nN\frac{N}{N+m}
$$
- $p_a$ ... apriorna verjetnost razreda C
- $m$ ... parameter vpliva apriorne verjetnosti
## Ocenjevanje učenja
Ocenjevanje točnosti na podatkih: učnih / testnih / novih oz. nevidenih
Nasprotujoča cilja: potrebujemo hkrati ==čimveč podatkov za učenje in za ocenjevanje točnosti==
- učnih podatkov dovolj $\rightarrow$ izločimo ==testno množico== - naključno/nenaključno ali poljubno/stratificirano
- učnih podatkov premalo $\rightarrow$ ==večkratne delitve== na učno in testno množico
### Prečno preverjanje
==k-kratno prečno preverjanje== (k-fold cross-validation): najpogosteje $k=10$
1. Celo učno množico razbij na $k$ disjunktnih množic
2. Za vsako od $k$ podmnožic izberi testno množico $\rightarrow$ ostale so učne in vsakič oceni točnost
3. Povpreči dobljenih $k$ ocen točnosti v končno oceno
Negiranje vpliva izbranega razbitja na podmnožice:
- večkrat ponovimo preverjanje z različnimi razbitji
- metoda ==izloči enega== (Leave-One-Out): $k=\text{št. primerov}$ $\rightarrow$ testna množica je 1 primer
## Obravnava atributov
### Zvezni atributi
==Diskretizacija== v 2 (binarizacija) ali več diskretnih intervalov:
- intrevali enake širine
- intervali z enako frekvenco primerov
- intervali, ki maksimizirajo informacijski prispevek
### Manjkajoči atributi
Učenje:
- se ne oziramo
- ignoriramo cele učne primere
- uporaba posebne vrednost NA/UNKNOWN
- nadomestimo manjkajočo vrednost - povprečje, modus, naključna, napovedana
Napovedovanje:
- verjetnostna klasifikacija glede na vse možne vrednosti atributa
## Naivni Bayesov klasifikator
**Bayesovo pravilo** izraža diagnostično pogojno verjetnost na podlagi vzorčne pogojne verjetnosti
$$
P(hipoteza/opažanje)=\frac{P(opažanje/hipoteza)*P(hipoteza)}{P(opažanje)}
$$
Verjetnost razreda C (hipoteze) pri podanih vrednostih atributov:
$$
P(C/X_1X_2...X_n)=\frac{P(C)*P(X_1/X_2...X_n)}{P(X_1X_2...X_n)}
$$
Poznavanje velikega števila pogojnih verjetnosti verižnega pravila je v praksi težavno:
$$
P(X_1X_2...X_n)=P(X_1/X_2...X_n)*P(X_2/X_3...X_n)*...*P(X_{n-1}/X_n)*P(X_n)
$$
Zato predpostavimo medsebojno neodvisnost - dobri približki:
$$
P(C/X_1X_2...X_n)\sim\frac{P(C)*\prod_iP(X_i/C))}{\prod_iP(X_i)}
$$
==Bayesov klasifikator==: primer klasificiramo v najbolj verjeten razred
$$
h(C/X_1X_2...X_n)=P(C)*\prod_{i=1}^nP(X_i/C)
$$
- učenje: ocenimo verjetnosti $P(C_k)$ in $P(X_i/C_k)$ za vse razrede $C_k$ in vrednosti atributov $X_i$
- napovedovnje: uporaba zgornje enačbe za napoved razreda novim primerom
Poenostavitev formule $\rightarrow$ $\sum P(C)\ne1$ $\rightarrow$ ==normalizacija rezultatov==
### Nomogrami
==Nomogram==: grafična upodobitev numeričnih odnosov med spremenljivkami $\rightarrow$ pristop k vizualizaciji naivnega Bayesovega modela
- pomembnost posameznih ==vrednosti== vsakega atributa na ciljni razred
- pomembnost posameznih ==atributov== na ciljni razred
Vsaka vrednost atributa doprinaša določeno št. točk k ==skupni vsoti točk==, ==razpon točk atributa== predstavlja pomembnost atributa na napoved ciljnega razreda
#### Izračun nomograma
==Logistična funkcija==: verjetnost na intervalu $[0,1]$ preslika na interval $(-\infty,\infty)$
$$
logit\ P=log\frac{P}{1-P}
$$
$$
logit\ h(C/X_1X_2...X_n)=\ ...\ =logit\ P(C)+\sum_i log\frac{P(X_i/C)}{P(X_i/\overline C)} = logit\ P(C)+\sum_i log\ OR(X_i)
$$
Edino ==razmerje verjetja== (Odds Ratio) je odvisno od vrednosti atributov $X_i$ $\rightarrow$ uporabimo za točkovanje doprinosa atributa
$$
točke(C/X_i)=log\ OR(X_i)=log\frac{P(X_i/C)}{P(X_i/\overline C)}
$$
$$
točke(C/X_1X_2...X_n)=\ ...\ =\sum_ilog\frac{\frac{P(X_i/C)}{P(X_i/\overline C)}}{\frac{P(C)}{P(\overline C)}}
$$
## Metoda k najbližjih sosedov
