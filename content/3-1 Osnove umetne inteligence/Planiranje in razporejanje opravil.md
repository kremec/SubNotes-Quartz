## Predstavitev problema
==Plan==: zaporedje akcij, ki pripelje od začetnega do končnega stanja
Formalni opis problema:
- začetno in ciljna stanje
- akcije - predpogoji in učinki
- ==predpostavka zaprtega sveta==: vsa neomenjena dejstva niso resnična, akcija nima neomenjenih učinkov

Predstavitev s ==formalnim jezikom==: STRIPS (1971) - ADL (1986) - PDDL (2005)
#### STRIPS
```
akcija(Spremenljivka_1, Spremenljivka_2, ...)
predpogoji: [atom(Argument_1, ...), ...]
učinki:
    add: [atomi ...]
    del: [atomi ...]
omejitve: [trditve ...]
```
Rezultat akcije $a$ v stanju $s$: $s_1=(s-del(a))\cup add(a)$
#### PDDL
```
Akcija(spremenljivka_1, spremenljivka_2, ...)
PRECOND: Atom_1(argument_1, ...) AND Atom_2 ...
EFFECT: Atomi ...
```
## Klasično preiskovanje prostora stanj
Uporaba preiskovalnih algoritmov $\rightarrow$ možna uporaba akcij, ki niso relevantne $\rightarrow$ ==kombinatorična eksplozija stanj==
Rešitve:
- dobra hevristika
- drugačen pristop k preiskovanju
## Planiranje s sredstvi in cilji
Algoritem:
1. Izberi nerešen cilj
2. Izberi akcijo, ki lahko vzpostavi (doseže) ta cilj
3. Ker ima akcija predpogoje, omogoči akcijo z izvedbo predpogojev
4. Izvedi akcijo
5. Ponavljaj, dokler niso uresničeni vsi cilji
### Sussmanova anomalija
Problem interakcije med cilji
==Linearno reševanje==: algoritem planiranja obravnava cilje "lokalno" - med reševanjem enega se ne ozira na druge
$\rightarrow$ z doseganjem enega cilja lahko razveljavi že dosežene cilje / predpogoje zanje
$\rightarrow$ vrstni red obravnavanja ciljev vpliva na nepotrebne korake
Princip varovanja / ščitenja ciljev: pri preiskovanju ne podiramo že doseženih ciljev
Rešitev:
- nelinearno planiranje - ne vztrajamo pri urejenosti ciljev
- regresiranje ciljev - drugačen algoritem
## Planiranje z regresiranjem ciljev
==Globalno planiranje==: algoritem obravnava vse cilje hkrati
$\rightarrow$ obravnavamo najbolj smiselne akcije
Algoritem:
1. Izberi akcijo, ki doseže čim večjo množico ciljev
2. Izračunaj predhodne cilje ob uporabi te akcije - regresiranje ciljev skozi akcijo
   Analiziramo: veljavnost množice ciljev glede na postopek regresiranja, protislovja v regresirani množici ciljev
   $Regresirani\ cilji=cilji\cup predpogoji(A)-add(A)$
   Veljati mora $cilji\cap del(A)=\emptyset$
3. Ponavljaj z regresiranjem, dokler niso uresničeni vsi cilji začetnega stanja ($regresirani\ cilji \subseteq cilji\ začetnega\ stanja$)
![[Planiranje in razporejanje opravil-Image-1.png|400]]
## Razporejanje opravil
Omejitve realnosti:
- ==časovne omejitve==: začetki in trajanja aktivnosti, roki zaključkov
- ==omejitve resursov==: npr. omejeno št. procesorjev, kadra, bencina, ...

Definicijo problema razširimo z:
- potrebnim vrstnim redom akcij ($Akcija1 < Akcija2$)
- trajanjem operacij
- št. razpoložljivih resursov
- količina (trajne) porabe resursov ob akciji
- količina (začasne) zasedenosti resursov med akcijo
### Časovne omejitve
==Metoda kritične poti==: najdaljša pot določa dolžino trajanja celotnega plana
Vsaki akciji priredimo par `[ES, LS]`:
- `ES` (Earliest Start) ... najbolj zgoden možen začetek
- `LS` (Latest Start) ... najbolj pozen možen začetek

Postopek računanja:
$$
\begin{align} ES(Start)&=0 \\ ES(B)&=max_{A<B}[ES(A)+Duration(A)] \\ LS(Finish)&=ES(Finish) \\ LS(A)&=min_{A<B}[LS(B)-Duration(A)] \\ rezerva&=LS-ES \end{align}
$$
Časovna zahtevnost: $O(Nb)$; $N$ ... št. akcij, $b$ ... faktor vejanja
### Omejitve resursov
Neprekrivanje aktivnosti, ki potrebujejo iste resurse
Časovna zahtevnost: NP-težek problem

==Algoritem najmanjše časovne rezerve==: hevristka
1. Na vsaki iteraciji dodeli najbolj zgodnji možen začetek akciji z izpolnjenimi predhodniki in ==najmanjšo časovno rezervo==
2. Posodobi `[ES, LS]` za cel graf
3. Ponavljaj do uresničitve vseh ciljev