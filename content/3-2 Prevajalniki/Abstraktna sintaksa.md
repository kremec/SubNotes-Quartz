Vhod: drevo izpeljav
Izhod: abstraktno sintaksno drevo

==Abstraktno sintaksno drevo==: vmesnik med sintaktno analizo in kasnejšimi fazami prevajanja, ki ne vsebuje balasta konkretnega sintaksnega drevesa (ki ne vpliva na semantiko programa)

==Semantične akcije==: akcije za generacijo semantičnih vrednosti v obliki vozlišč abstraktnega sintaksnega drevesa
### Sintaksno usmerjeno prevajanje
Prevajanje dobljenih poddreves abstraktnega sintaksnega drevesa, ki poleg razumevanja programa tako določa še potek prevajanja
Orodje: atributne gramatike (KNG, atributi in semantična pravila za izračun atributov)
### Pozicije napak
Enoprehodni prevajalnik izvaja leksikalno, sintaksno in semantično analizo istočasno $\rightarrow$ pozicijo napake lahko dobimo iz leksikalne analize.
Prevajalnik, ki uporablja abstraktna sintaksna drevesa, pa lahko izvaja posamezni del analize neodvisno od ostalih $\rightarrow$ v drevo dodamo podatke o pozicijah

LL algoritem prevajanja vedno pozna trenutno lokacijo simbola, ker dela v smeri $\downarrow$
### Vzorec obiskovalcev
Delitev definicij kasnejših akcij (npr. generacija kode, preverjanje tipov, optimizacije, ... ) od definicij tipov vozlišč abstraktnega sintaksnega drevesa
### ANTLR
ANTLR omogoča specifikacijo semantičnih akcij zraven produkcij sintakstne gramatike ($A\rightarrow X_1\ ...\ X_n$)

> [!example] Primer
> Primer stavka za nadaljne primere: `num * id + id * (num + id)`
> 
> Abstraktno sintaksno drevo:
> ![[Abstraktna sintaksa-Image-1.png|150]]

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
#### Levo-rekurzivna / LR gramatika
Uvedemo podedovan atribut AST, atribute računamo v smeri $\uparrow$
- `attr(A) = f( attr(X1), ..., attr(Xn) )` ... vrednost atributov na levi je vedno odvisna od vrednosti atributov na desni

> [!example] Primer
> Gramatika
> ```
> E -> E + T    -    E.ast = + (E1.ast, T.ast)
> E -> T        -    E.ast = T.ast
> T -> T * F    -    T.ast = * (T1.ast, F.ast)
> T -> F        -    T.ast = F.ast
> F -> id       -    F.ast = id
> F -> num      -    F.ast = num
> F -> ( E )    -    F.ast = E.ast
> ```
> ![[Abstraktna sintaksa-Image-2.png|200]]
#### LL(1) kompatibilna gramatika
Uvedemo podedovan atribut AST, atribute računamo v smeri $\downarrow$
- `attr(Xk) = f( attr(A), attr(X1), ..., attr(Xk-1) )`

> [!example] Primer
> Gramatika
> ```
> E -> T E'       -    E'.ast' = T.ast  ;  E.ast = E'.ast
> E' -> + T E1'   -    E1'.ast' = + (E'.ast', T.ast)  ;  E'.ast = E1'.ast
> E' -> empty     -    E'.ast = E'.ast'
> T -> F T'       -    T'.ast' = F.ast  ; T.ast = T'.ast
> T' -> * F T2'   -    T.ast = * (T'.ast', F.ast)  ;  T'.ast = T2'.ast
> T' -> empty     -    T'.ast = T'.ast'
> F -> id         -    F.ast = id
> F -> num        -    F.ast = num
> F -> ( E )      -    F.ast = E.ast
> ```
> ![[Abstraktna sintaksa-Image-3.png|200]]