Vhod: program izvornega jezika
Izhod: zaporedje leksikalnih simbolov
### Leksikalni simbol
Lastnosti:
- vrsta - različne funkcije (določene z izvornim jezikom): ime, konstanta, simbol, ...
- znakovna predstavitev
- položaj v izvorni datoteki: št. vrstice + odmik v vrstici (npr. za izpis napak)

> [!example] Primer leksikalnih simbolov v C programu
> ```
> int main() { for (int i=0; i<10; i++) printf("%d\n", i+1); return 0; }
> ```
> Vzeti simboli: `int`, `main`, `(`, `)`, `{`, `for`, ..., `i`, `++`, ..., `0`, `;`, `}`
> Leksikalni simboli: `INT`, `ID(main)`, `LeftParentesis`, `RightParentesis`, `LeftBrace`, `FOR`, ...
> 
> Ključne besede imajo svoje simbole (npr. `FOR`, `RETURN`), npr. `main` in `printf` pa sta dogovora / konstrukta
### Leksikalna analiza
Tipično ignorira/izpusti:
- belo besedilo (whitespaces) - presledki, tabulatorji, nove vrstice
- komentarje

==Pravilo najdaljšega ujemanja==: na vsakem koraku iz vhodnega niza vzame najdaljši možen ujemajoč leksikalni simbol
Obravnava napak:
- prekinemo analizo in vrnemo napako
- prenesemo napako naprej sintaksnemu analizatorju za ukrepanje/popravljanje napake

Numerične konstante so nepredznačene - `+` in `-` sta ločena leksikalna simbola
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
### Implementacija
#### Regularni izrazi
Primeri:
- ime (spremenljivke/funkcije): `[a-zA-Z_][a-zA-Z0-9_]*`
- ključna beseda `for`: `for`
- belo besedilo: `[␣\t\n]+`
- cela števila: `[+-]?[0-9]+`
#### Končni avtomati
Implementacija regularnih izrazov:
- Posamično: ![[Leksikalna analiza-Image-1.png|500]]
- Nedeterministični končni avtomat: ![[Leksikalna analiza-Image-2.png|500]]
- Deterministični končni avtomat: ![[Leksikalna analiza-Image-3.png|500]]
#### Leksikalna orodja
Podamo opis želenega leksikalnega analizatorja, ki ga orodje generira-implementira
Primeri: ANTLR (Java), LEX/JAX (C/...)