Vhod: zaporedje leksikalnih simbolov
Izhod: drevo izpeljav (ali sled izpeljave)
### Kontekstno neodvisna gramatika
==Kontekstno neodvisna gramatika== opisuje sintakso jezika s ==produkcijami==: $simbol \rightarrow simbol\ ...\ simbol$
==Simbol== je lahko:
- ==končni==: token iz abecede jezika, ki mu pripada semantična vrednost
- ==vmesni==: pojavi se na levi strani produkcije, en mora biti začetni

==(Skrajno leva/desna) izpeljava==: postopek izpeljave niza iz začetnega simbola z razširjanjem (skrajno levih/desnih) vmesnih simbolov $\rightarrow$ leva/desna sled izpeljave
==Drevo izpeljav==: prikaz izpeljave

==Dvoumnost gramatike==: niz jezika gramatike ima več možnih dreves izpeljav
### Algoritmi
#### LL (Left-to-right scan producing the Left-most derivation)
Leva sled izpeljave, drevo gradimo od zgoraj navzdol
Šibkejši od LR, ampak lažja implementacija na roke z boljšim upravljanjem napak

==LL(k)== gramatika: gledamo največ $k$ simbolov vnaprej $\rightarrow$ v vseh celicah tabele mora biti največ $k$ produkcij
##### LL(1) gramatike
LL(1) iz prvega simbola razbere potrebno produkcijo.
Pogoj: za vsaki produkciji $X\rightarrow\gamma_1$ in $X\rightarrow\gamma_2$ mora veljati: $FIRST(\gamma_1)\neq FIRST(\gamma_2)$
- $nullable(X) = true$ ... vmesni simbol $X$ se lahko izpelje v prazen niz $\epsilon$
- $FIRST(\gamma)$ ... množica možnih končnih simbolov, ki so prvi simbol možnih nizov izpeljav $\gamma$
    - $FIRST(X\gamma)=FIRST(X);\ nullable(X)=false$
    - $FIRST(X\gamma)=FIRST(X)\cup FIRST(\gamma);\ nullable(X)=true$
##### Generacija primerne gramatike za LL analizo:
1. Pretvorba dvoumne v nedvoumno gramatiko:
> [!example] Dvoumna in nedvoumna gramatika
> Dvoumna gramatika:
> ![[Sintaksna analiza-Image-1.png|500]]
> Primera različnih dreves izpeljave istega niza `id := id + id + id`:
> ![[Sintaksna analiza-Image-2.png|500]]
> Nedvoumna gramatika: `*` je močnejši od `+`, leva asociativnost, simbol za konec niza
> ![[Sintaksna analiza-Image-3.png|500]]

<br><br>

2. Eliminacija leve rekurzije $X\rightarrow X\gamma$ z uvedbo desne rekurzije preko novega simbola:
$$
\begin{pmatrix} X \to X \gamma_1 \\ X \to X \gamma_2 \\ X \to \alpha_1 \\ X \to \alpha_2 \end{pmatrix} \Rightarrow \begin{pmatrix} X \to \alpha_1 X' \\ X \to \alpha_2 X' \\ X' \to \gamma_1 X' \\ X' \to \gamma_2 X' \\ X' \to \end{pmatrix}
$$
> [!example] Primer
> Problem stare:
> - $E\to E+T$
> - $E\to T$
> 
> Rešitev za novo:
> ![[Sintaksna analiza-Image-4.png|450]]

3. Levo faktoriranje koncev produkcij preko novega simbola:
> [!example] Primer
> Problem stare:
> - $S\to if\ E\ then\ S\ else\ S$
> - $S\to if\ E\ then\ S$
> 
> Rešitev za novo:
> $$
> \begin{align}
> S&\to if\ E\ then\ S\ X \\
> X&\to \\
> X&\to else\ S
> \end{align}
> $$
##### LL algoritem
Na vhodu prejemamo znake, na skladu imamo:
- vmesne simbole - naredimo razvoj glede na tabelo produkcij glede na prvi vhodni simbol
- končne simbole - če je prvi končni simbol na skladu enak prvemu vhodnemu simbolu naredimo pomik (zbrišemo enaka simbola)
#### LR (Left-to-right scan producing the Right-most derivation)
LR: desna sled izpeljave, drevo gradimo od spodaj navzgor
Analizira vse deterministične kontekstno neodvisne jezike

Zamakne odločitev izbire produkcije dokler ne vidi vseh simbolov desne strani produkcije
Implementacija odločanja med slednjima operacijama preko DKA:
- dodaj naslednji vhodni simbol na sklad
- odstrani simbole desne strani produkcije iz sklada in dodaj levi simbol produkcije na sklad
#### PEG (Parsing Expression Grammars) - Python
#### Sintaksni kombinatorji (Parser combinators) - novejši, nedorasli
### Parser generatorji
Podamo opis želenega sintaksnega analizatorja, ki ga orodje generira-implementira
ANTLR implementira ALL(\*) algoritem, v primeru več kot 1 produkcije uporabi KA za nadaljno analizo možnosti