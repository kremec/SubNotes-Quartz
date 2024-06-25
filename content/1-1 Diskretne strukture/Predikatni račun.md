==Področje pogovora==: neprazna množica konstant
==Predikati==: logične funkcije, ki lahko za svoje argumente dobijo posamezne **konstante** iz področja pogovora, pri čemer dobimo [[Izjave#Izjave|izjave]].
- Delitev: enomestni (npr. P(x)) / večmestni (npr. P(x,y))

Namesto konstant lahko v predikate vstavljamo tudi **spremenljivke**, pri čemer dobimo formule (ki niso nujno izjave).
Iz formule lahko naredimo izjavo na več načinov:
- spremenljivke zamenjamo s konstantami
- formulo zapremo s kvantifikatorji
### Kvantifikatorji
==Kvantifikatorja==:
- $\forall$ - **univerzalni kvantifikator** ("za vsak")
- $\exists$ - **eksistenčni kvantifikator** ("obstaja")

Istovrstnim kvantifikatorjem znotraj istega predikata lahko menjaš vrstni red (različnim pa ne)
Doseg kvantifikatorja je najmanjši možen - najmanjša izjavna formula, ki jo preberemo desno od kvantifikatorja
Kvantifikator veže svojo spremenljivko in istoimenske proste spremenljivke v svojem dosegu:
- **prosta spremenljivka** (npr. $x+5$)
- **vezana spremenljivka** (npr. $\int_1^3 x+5 \ dx$)

Kvantifikatorji imajo isto prednost kot negacija

==Termi==: drugo ime za konstante in spremenljivke
==Atom==: termi, vstavljeni v predikat
==Izjavne formule==:
1. Atomi so izjavne formule
2. Če sta W in V izjavni formuli in je $x$ spremenljivka, potem so tudi $(\neg W), (W \land V), \ ..., \ (\exists x W) \ in \ (\forall x W)$ izjavne formule

==Splošno veljavna izjavna formula==: resnična v vsaki interpretaciji (ustreza tavotogliji iz [[Izjave#Izjave|izjav]])
==Neizpolnljiva izjavna formula==: neresnična v vsaki interpretaciji (ustreza protislovju iz [[Izjave#Izjave|izjav]])
## Zakoni predikatnega računa
$$
\begin{aligned} \neg \forall xW &\sim \exists x\neg W \\ \neg \exists xW &\sim \forall x\neg W \\ \\ \forall x \forall yW &\sim \forall y \forall xW \\ \exists x \exists yW &\sim \exists y \exists xW \\ \\ \forall x(W \land V) &\sim \forall xW \land \forall xV \\ \exists x(W \lor V) &\sim \exists xW \lor \exists xV  \end{aligned}
$$
Če se $x$ ne pojavi (prosto) v formuli $C$, veljajo tudi naslednje enakovrednosti:
$$
\begin{aligned} \forall x(C \lor W) &\sim C \lor \forall xW \\ \exists x(C \lor W) &\sim C \lor \exists xW \\ \\ \forall x(C \land W) &\sim C \land \forall xW \\ \exists x(C \land W) &\sim C \land \exists xW \\ \\ \forall x(W \implies C) &\sim \exists xW \implies C \\ \forall x(C \implies W) &\sim C \implies (\forall xW) \end{aligned}
$$

$W(x/a)$ - v formuli $W$ vse spremenljivke $x$ nadomestimo z $a$, če se $a$ ne pojavi drugje v $W$
Če je $W$ formula imen prostih spremenljivk ne smemo preimenovati, vezane pa lahko

==Preneksna normalna oblika (PNO)== izjavne formule $W$ je izjavna formula $W_{PNO}$, za katero velja:
- $W_{PNO}$ je enakovredna $W$
- $W_{PNO}$ ima na začetku vse kvantifikatorje

Kako do PNO:
1. Preimenuj vezane spremenljivke v formuli, da vsi kvantifikatorji uporabljajo spremenljivke z raličnimi imeni
2. Premakni kvantifikatorje proti levi (pri čemer lahko $\implies$ in $\iff$ zamenjaš z $\neg$, $\land$ in $\lor$)

==Enakovrednost izjavnih formul== $W \sim V$: v vseh možnih interpretacijah imata isto logično vrednost
Preverjamo enakovrednost: primerjava PNO
Preverjamo neenakovrednost: iščemo interpretacije, v kateri imata $W$ in $V$ različni logični vrednosti