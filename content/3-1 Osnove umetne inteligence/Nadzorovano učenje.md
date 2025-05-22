 Samodejno izboljševanje algoritmov ob pridobivanju izkušenj $\rightarrow$ gradnja modela z analizo učnih podatkov

Učni primeri so podani kot vrednosti vhodov in izhodov - označenih učnih primerov
$$
\begin{aligned} (x_1,y_1),...,(x_n,y_n) \ \ &... \ \ učni\ primeri \\ x_j \ \ &... \ \ atributi \\ y_j \ \ &... \ \ vrednost\ neznane\ funkcije\ y=f(x) \end{aligned}
$$
Učimo se funkcije, ki preslika vhode v izhode: iščemo funkcijo $h$ ... ==hipoteza==, ki je najboljši približek funkciji $f$
### Vrste problemov
#### Klasifikacijski problemi
$y$ je ==diskretna== spremenljivka - ==razred== (končen nabor vrednosti)
Atributna predstavitev podatkov: vsak učni primer (vrstice) ima vrednosti atributov (stolpci)
#### Regresijski problemi
$y$ je ==zvezna== spremenljivka - ==označba== (npr. število)
### Evalviranje hipotez
==Prostor hipotez== lahko vsebuje več hipotez, ki so konsistentne z učno množico
Dobra hipoteza je dovolj ==splošna==: pravilno napoveduje vrednost $y$ tudi za še nevidene primere
Kriteriji evalviranja hipotez: konsistentnost (z učnimi primeri), splošnost, razumljivost
Točnosti hipotez: TP, TN, FP, FN
Klasifikacija točnosti:
$$
\begin{aligned} CA=\frac{TP+TN}{TP+TN+FP+FN}=\frac{TP+TN}{N} \end{aligned}
$$
## Odločitvena drevesa
==Odločitveno drevo==: model, ki ponazarja relacijo med atributi in odločitvijo / ciljno spremenljivko:
- notranja vozlišča ~ pogoji glede na vrednost atributa
- listi ~ odločitev
- pot ~ konjunkcija pogojev na poti do lista

Cilj: gradnja ==čim manjšega drevesa==, ki je ==konsistentno z učnimi podatki==
### Top Down Induction of Decision Trees
==Hevristični požrešni algoritev==:
- izberi najpomembnejši atribut - najbolj vpliva na klasifikacijo primera
- rekurzivno razdeli primere v poddrevesa glede na njihove vrednosti
- če vsi elementi v listu pripadajo istemu razredu, ustavi gradnjo

Požrešni algoritem je ==kratkoviden== - izbira "lokalni" najboljši atribut, ne upošteva povezav med atributi, ki pripeljejo do optimalne rešitve
#### Iskanje najpomembnejšega atributa
==Entropija / nedoločenost== minimiziramo:
$$
H=-\sum_kp_k*log_2p_k \ \ [bit \ informacije]
$$
==Informacijski prispevek== maksimiziramo:
$$
\begin{align} Gain(A)&=I-I_{res}(A) \\ I_{res}=\sum_ip_{v_i}*H(c/v_i)&=-\sum_ip_{v_i}*\sum_cp(c/v_i)*log_2p(c/v_i) \end{align}
$$
$$
\begin{align} I \ ... \ &začetna \ entropija \\ I_{res} \ ... \ &residualna \ entropija \\ I(A) \ ... \ &entropija\ atributa \end{align}
$$
#### Večvrednostni atributi
Problem: ==informacijski prispevek precenjuje kakovost večvrednostnih atributov== (višja entropija zaradi več vrednosti, namesto zaradi kakovosti)
Rešitve:
1. Normalizacija informacijskega prispevka - ==relativni informacijski prispevek== (information gain ratio):
$$
GainRatio(A)=\frac{Gain(A)}{I(A)}
$$
2. Uporaba alternativnih mer - ==Gini index==:
$$
\begin{align} Gini&=\sum_{c_1\neq c_2}p(c_1)*p_(c_2) \\ Gini(A)&=\sum_vp(v)\sum_{c_1\neq c_2}p(c_1/v)*p(c_2/v) \end{align}
$$
3. ==Diskretizacija / binarizacija atributov== - zalogo vrednosti razbijemo v 2 / več diskretnih množic
   Diskretni atributi: odločitvena drevesa delijo prvotno množico na vse manjše podmnožice
   Zvezni atributi: delitev podmnožice glede na smiselno mejo izbranega atributa
    - intervali enake širine / z enako frekvenco primerov / maksimizirajo informacijski prispevek
    - prostor tako delimo na particije (hiper-kvadre), katerih meje so vzporedne koordinatnim osem
#### Manjkajoči atributi
Učenje: ignoriramo / uporaba vrednosti NA/UNKNOWN / nadomestimo z npr. povprečjem
Napovedovanje: verjetnostna klasifikacija glede na vse možne vrednosti atributa
#### Uporabnost odločitvenega drevesa
==Privzeta točnost==: minimalna pričakovana točnost drevesa je verjetnost večinskega razreda v učni množici (če je manjša vzamemo kar splošno bolj verjetno opcijo)
==Pretirano prilagajanje== (overfitting): ==izguba splošnosti== ob prevelikem prilagajanju učnim podatkom $\rightarrow$ ==uporaba nevidenih/testnih primerov== iz množice učnih primerov za sprotno preverjanje med gradnjo drevesa
## Učenje dreves iz šumnih podatkov
Nepopolni podatki z napakami $\rightarrow$ učenje šuma, slaba razumljivost, nižja klasifikacijska točnost, overfitting
==Rezanje odločitvenega drevesa==: posplošitev drevesa z rezanjem šumnih in pretirano prilagojenih nižjih delov drevesa
### Strategije rezanja
#### Rezanje vnaprej (forward pruning)
Uporaba dodatnega kriterija glede na obseg šuma za zaustavitev gradnje drevesa $\rightarrow$ ==hitrejše==, a ==kratkovidno==
#### Rezanje nazaj (post-pruning)
Po gradnji drevesa odstranimo manj zanesljive dele drevesa $\rightarrow$ ==počasnejše==, a upoštevamo informacijo ==celega drevesa==
##### Rezanje z zmanjšanjem napake (Reduced Error Pruning)
Uporaba ==rezalne/validacijske množice== primerne velikosti za zanesljivost (npr. vzamemo 30% učnih primerov)
Postopek:
1. Potuj po vozliščih od vključno staršev listov drevesa navzgor
2. št. napačnih klasifikacij v listih poddrevesa $\geq$ št. napačnih klasifikacij v vozlišču $\rightarrow$ ohrani samo vozlišče (reži potomce)
##### Rezanje z minimizacijo napake (Minimal Error Pruning)
Uporaba učne množice (in ne ločene rezalne množice)
Cilj: minimizacija klasifikacijske napake $E$ / maksimizacija točnosti $CA$
Postopek:
1. Za vozlišče izračunamo:
    - ==statično napako== - verjetnost klasifikacije v napačen razred
$$
e(v)=p(razred\neq C/v)
$$
    - ==vzvratno napako==
$$
\sum_ip_iE(T_i)=p_1E(T_1)+p_2E(T_2)+...
$$
2. Režemo, če: $\text{statična napaka < vzvratna napaka}$
3. Napaka optimalno obrezanega drevesa:
$$
\begin{align} E(T)&=e(v)\ &; \ \ v\ je\ list \\ E(T)&=min(e(v),\sum_ip_iE(T_i))\ &; \ \ sicer \end{align}
$$
### Ocenjevanje verjetnosti
Relativna frekvenca: v listih z malo primeri ni dobra ocena (hitro spreminjajoča)
==Ocena verjetnosti==: boljša stabilnost z upoštevanjem ==apriorne verjetnosti==: domensko znanje verjetnosti o problemu (npr. 50% pri metu kovanca)
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
- $m$ ... parameter vpliva apriorne verjetnosti ($m$ linearno korelira z močjo rezanja)
## Ocenjevanje učenja
Nasprotujoča cilja: potrebujemo hkrati ==čimveč podatkov za učenje in za ocenjevanje točnosti==
- učnih podatkov dovolj $\rightarrow$ naključno ali stratificirano izločimo ==testno množico==
- učnih podatkov premalo $\rightarrow$ ==večkratne delitve== na učno in testno množico
### Prečno preverjanje
==k-kratno prečno preverjanje== (k-fold cross-validation): najpogosteje $k=10$
1. Celo učno množico razbij na $k$ disjunktnih množic
2. Za vsako od $k$ podmnožic izberi testno množico $\rightarrow$ ostale so učne in vsakič oceni točnost
3. Povpreči dobljenih $k$ ocen točnosti v končno oceno

Negiranje vpliva izbranega razbitja na podmnožice:
- večkrat ponovimo preverjanje z različnimi razbitji
- metoda ==izloči enega== (Leave-One-Out): $k=\text{št. primerov}$ $\rightarrow$ testna množica je 1 primer
## Naivni Bayesov klasifikator
**Bayesovo pravilo** izraža diagnostično pogojno verjetnost na podlagi vzorčne pogojne verjetnosti
$$
P(hipoteza/opažanje)=\frac{P(opažanje/hipoteza)*P(hipoteza)}{P(opažanje)}
$$
Verjetnost razreda $C$ (hipoteze) pri podanih vrednostih atributov:
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
- napovedovnje: uporaba zgornje enačbe za napoved razreda novim primerom + ==normalizacija rezultatov== (poenostavitev formule $\rightarrow$ $\sum P(C)\ne1$)
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
- ==neparametrična== metoda - ne ocenjuje parametrov
- ==leno učenje== - z učenjem odlaša vse do povpraševanja o novem primeru
- učenje na podlagi ==posameznih primerov==

Metoda: poišči k primerov, ki so najbližji glede na podano mero razdalje
- klasifikacija $\rightarrow$ napovej večinski razred
- regresija $\rightarrow$ povprečna vrednost označb sosedov

Izbira k (običajno $k=5$):
- liho št. $\rightarrow$ izognemo se neodločenim primerom
- premajhen / prevelik $\rightarrow$ pretirano / prešibko prilagajanje

Mere razdalj:
- ==razdalja Minkowskega==:
$$
L^p(x_i,x_j)=(\sum_k|x_{i,k}-x_{j,k}|^p)^\frac1p
$$
- ==evklidska razdalja==: $p=2$
- ==manhattanska razdalja==: $p=1$

Diskretni atributi $\rightarrow$ ==Hammingova razdalja== ... št. neujemajočih atributov
Zvezni atribti $\rightarrow$ razlika med vrednostma
- različno veliki intervali vrednosti $\rightarrow$ ==normalizacija==
- več dimenzij $\rightarrow$ ==prekletstvo dimenzionalnosti== ... primere to naredi bolj odmaknjene
### k najbližjih sosedov za regresijo
Naloga: najti k primerov, ki so najbližji glede na podano mero razdalje
Izračun napovedi $\rightarrow$ ==utežena vsota==: $w_i$ ... utež
$$
h(x_?)=\frac{\sum_{i=1}^kw_i*f(x_i)}{\sum_{i=1}^kw_i}
$$
za funkcijo $f$ uporabimo poljubno jedrno funkcijo, npr. ==Gaussovo jedro==
![[Strojno učenje-Image-1.png]]
### Regresijska drevesa
Listi v regresijskem drevesu zvezne ciljne spremenljivke predstavljajo nek napovedn model (npr. povprečno vrednost)

==Srednja kvadratna napaka== vozlišča v: mera nedoločenosti, ki jo želimo minimizirati
$$
MSE(v)=\frac1n\sum_{i=1}^n(y_i-\overline y)^2
$$
Pričakovana rezidualna nečistost:
$$
I_{res}(A)=p_{left}*l_{left}+p_{right}*l_{right}
$$
![[Strojno učenje-Image-2.png|200]]
## Linearna regresija
==Linearna regresija==: iskanje funkcije z ==eno odvisno spremenljivko== (in večimi utežmi), ki se najbolje prilega učnim podatkom
$$
h(x)=w_1x+w_0
$$
Računanje / optimizacija z ==minimizacijo srednje kvadratne napake==:
$$
napaka(h)=\sum_{j=1}^N(y_j-(w_1x_j+w_0))^2
$$
Analitična rešitev:
$$
\begin{align} w_1&=\frac{N(\sum x_jy_j)-(\sum x_j)(\sum y_j)}{N(\sum x^2_j)-(\sum x_j)^2} \\ w_2&=\frac{\sum y_j-w_1(\sum x_j)}{N} \end{align}
$$
Uporaba: ==klasifikacija== - separator razredov / ==regresija== - prileganje skozi podane točke
### Posplošitev v več dimenzij
Več neodisnih spremenljivk:
$$
h(x)=w_0+\sum_iw_ix_{j,i}
$$
Določevanje uteži:
- ==analitično==: $\vec w=(X^TX)^{-1}X^Ty$
- ==gradientni spust== - približek, a veliko hitrejši od analitičnega
![[Linearna regresija-Image-1.png|200]]
- $\eta$ ... hitrost učenja
- $x_i$ ... vrednost $i$-tega atributa učnega primera
### Linearni modeli pri klasifikaciji
==Stohastični gradientni spust==: preprosto iskanje rešitve s posodabljanjem uteži za vsak učni primer, hitrejše učenje kot pri klasičnem gradientnem spustu
$$
w_i \leftarrow w_i+\eta*(y-h(\vec x))*x_i
$$
- $y$ ... ciljna vrednost
- $h(x)$ ... izhodna vrednost za učni primer

|          |                                  | $y-h(x)$ | $(y-h(x))*x_i$                           | rezultat                                                              |
| -------- | -------------------------------- | -------- | ---------------------------------------- | --------------------------------------------------------------------- |
| $y=h(x)$ | izhod enak ciljni vrednosti      | 0        | ni popravka                              | utež ostane enaka                                                     |
| $y>h(x)$ | potreben popravek $h(x)$ navzgor | >0       | $x_i>0\implies >0$<br>$x_i<0\implies <0$ | utež povečamo za pozitivne $x_i$<br>utež zmanjšamo za negativne $x_i$ |
| $y<h(x)$ | potreben popravek $h(x)$ navzdol | <0       | $x_i>0\implies <0$<br>$x_i<0\implies >0$ | utež zmajšamo za pozitivne $x_i$<br>utež povečamo za negativne $x_i$  |
## Nevronske mreže
Umetni nevron izračuna ==uteženo linearno kombinacijo vhodov== in jo z ==aktivacijsko funckcijo== preslika v izhodno vrednost
![[Linearna regresija-Image-2.png|400]]
$$
a_j=g(\sum_iw_{i,j}a_i)=g(z_i)
$$
==Nevronska mreža==: medsebojno povezani nevroni lahko izračunavajo bolj kompleksne funkcije (medsebojno kombiniranje funkcij)
Implementacije:
- ==feed-forward network==: aciklične povezave od vhoda proti izhodu - organizacija v plasti, možen en ali več izhodnih nevronov (napoved ene zvezne vrednosti ali klasifikacija)
- ==rekurenčna mreža==: izhodi kot ponovni vhodi v mrežo $\rightarrow$ dinamičen sistem z notranjim stanjem
- ==konvolucijske mreže==
### Vzvratno razširjanje napake
1. ==Inicializacija uteži==: majhne neničelne naključne vrednosti
2. ==Izračun napovedi== za učne primere
3. ==Izračun izgube== - funkcije napake na izhodnih nevronih
4. ==Vzvratno razširjanje napake== od izhoda proti vhodu: izračun gradienta napake za izhodni in skriti nivo
5. ==Gradientni spust== z določeno hitrostjo učenja za popravke vrednosti uteži po formuli

Ponavljaj korake 2-5 do ustavitvenega kriterija: izbrano št. epoh, znižanje napake do željene meje, ...
![[Linearna regresija-Image-3.png|300]]

### Učenje nevronske mreže
![[Linearna regresija-Image-4.png|400]]
Ovrednotimo napako s primerjavo aktivacij nevronov izhodne plasti in ciljnih vrednosti
Cilj: minimizacija napake preko nastavljanja uteži