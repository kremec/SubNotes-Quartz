## Bayesovske mreže
==Bayesovske mreže==: verjetnostni model za predstavitev ==odvisnosti med slučajnimi spremenljivkami==, iz katerega sklepamo na verjetnost resničnosti spremenljivke ob upoštevanju danih (ne)odvisnosti
Predstavitev z ==usmerjenim acikličnim grafom==:
- vozlišča ... slučajne spremenljivke (dejstva, hipoteza)
- povezave ... odvisnosti med spremenljivkami (vpliv starša na naslednika)

Stanje sveta povzamemo z vektorjem logičnih spremenljivk
Za opis stanja z $n$ spremenljivkami bi morali poznati ==popolno verjetnostno porazdelitev== $\rightarrow$ $2^n-1$ možnih stanj $\rightarrow$ nepraktično za veliko št. spremenljivk
## Pogojne verjetnosti
Problem lahko opredelimo le s ==pogojnimi verjetnostmi==, zaradi česar lahko podamo manj podatkov kot s popolno verjetnostno porazdelitvijo
### Izračun verjetnosti dogodka
S pogojnimi verjetnostmi preprosteje izračunamo verjetnost dogodka iz popolne verjetnostne porazdelitve

Neodvisne spremenljivke (ki niso starši iskane spremenljivke) lahko izpustimo iz konjunkcije pogojnih spremenljivk:
$$
P(X_1X_2\ ...\ X_n)=\prod_{i=1}^nP(X_i/starši(X_i))
$$
## Verjetnostno sklepanje
Upoštevanje ==evidence==: ==podane informacije o resničnih dogodkih== lahko vpliva na verjetnosti ostalih dogodkov v mreži
2 smeri sklepanja:
- ==vzročno==: od vzrokov k posledicam
- ==diagnostično==: od posledic k vzrokom
### Odvisnosti v mreži
#### Skupni prednik (divergentno vozlišče)
Odvisnost naslednikov - če vemo za resničnost enega, to vpliva na verjetje drugega
Vendar poznavanje resničnosti prednika omogoči neodvisno obravnavanje naslednikov
#### Skupni naslednik (konvergentno vozlišče)
Neodvisnost predhodnikov - če vemo za resničnost enega, to ne vpliva na verjetje drugega
Vendar poznavanje resničnosti naslednika omogoči odvisno obravnavanje prednikov
#### Veriga
Odvisnost predhodnika in prednika - le vemo za resničnost enega, to vpliva na verjetje drugega
Vendar poznavanje resničnosti vmesnega vozlišča omogoči neodvisno obravanje predhodnika in naslednika
### Določanje neodvisnosti v Bayesovski mreži
#### Neodvisnost od nenaslednikov
Vozlišče je neodvisno samo od svojih predhodnikov staršev, če:
- so podani vsi starši in
- so podani samo starši
#### Ovojnica Markova
Vozlišče je neodvisno od vseh ostalih vozlišč, če so podani starši, otroci in starši otrok (sorojenci)
#### d-ločevanje
Vozlišči sta neodvisni, če obstaja množica vozlišč $E$, ki d-ločuje (blokira odvisnost) med njima
Posledica: $P(A/EB)=P(A/E)$
Množica $E$ ločuje vozlišči, če na vsaki poti med vozliščema obstaja takšno vozlišče, ki pot blokira
Blokirajoče vozlišče:
- $X$ je ==divergentno vozlišče==: iz njega kažeta povezavi na vozlišča $\implies$ $X\in E$
- $X$ je ==zaporedno vozlišče==: veriga $\implies$ $X\in E$
- $X$ je ==konvergentno vozlišče==: vanj kažeta povezavi iz vozlišč $\implies$ $X\cup X-ovi\ nasledniki \notin E$