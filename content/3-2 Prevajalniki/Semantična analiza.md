Vhod: abstraktno sintaksno drevo
Izhod: abstraktno sintaksno drevo + atributi

==Atributi==: informacije pridružene vozliščem AST

Pristopa:
- ==statično==: prevajanje s strožjimi pravili, a lažje za programerja in hitrejše
- ==dinamično==: izvajanje s sproščenimi pravili, a počasnejše

Problem izračunljivosti: v prejšnjih fazah še ni Turingove izračunljivosti - predvidevanja kaj se bo izvršilo/izračunalo (npr. nedosegljiva koda, preverjanje tipov pri senčenju tipov, ...)
### Razreševanje imen
Povezovanje (mesto) definicije - (mesto) uporabe simbola
> [!example] Primer
> ```c
> {
>     int x ;              // mesto definicije
>     x = 7 ;              // mesto uporabe
>     x = 2\*x ;           // mesto uporabe
>     printf("%d", x) ;    // mesto uporabe
> }
> ```

==Imenski prostor== (namespace): definirana različna ali celo enaka imena (ki pa niso ista)
- Enaka imena različnih imenskih prostorov lahko uporabljamo istočasno

==Doseg== (scope): obseg videnosti imena po definiciji, izven dosega se preslikava izniči
==Senčenje==: nova definicija v notranjem dosegu zasenči definicijo iz zunanjega bloka
#### Simbolna tabela / okolje
Vzdrževanje preslikav ime - (mesto) definicije
Načina implementacije:
- imperativni tip: zgošnega tabela, definicije v povezanih seznamih + ločen povezan seznam po dosegih
- funkcijski tip: nova tabela za vsak nivo (slabo, ker so vključeni simboli standardnih knjižnic namesto le v eni tabeli v vseh tabelah $\rightarrow$ počasnejše iskanje)

Implementacija: slovar (npr. zgoščena tabela / AVL drevo / ... )
Obhod AST drevesa (v pravem vrstnem redu):
- na mestu definicije imena:
    - če ime ni vidno v trenutnem dosegu: vstavimo preslikavo v simbolno tabelo
    - če ime je vidno v trenutnem dosegu: senčenje / javimo napako dvojne definicije imena
- na mestu uporabe imena:
    - če definicija obstaja: usmerimo kazalec na definicijo
    - če definicija ne obstaja: javimo napako

Funkcije:
- vstavljanje: dodaj preslikavo v simbolno tabelo / javi napako
- vrni definicijo danega imena / javi napako
- začni doseg: začni novo področje dosega
- končaj doseg: končaj trenutno področje dosega in se vrni v staro

<br><br><br><br><br><br>
### Preverjanje tipov
==Tip==: množica vrednosti in operacije nad njo
==Statična/dinamična tipizacija==: v času prevajanja/izvajanja
==Statično preverjanje tipov==: hitrost, določanje tipov spremenljivk
- Vsakemu tipu v programu določimo opis in predstavitev
    - ==vgrajeni tipi== (npr. `int`, `char`, ...) $\rightarrow$ predstavitev odvisna od jezika in prevajalnika
      (npr. pravilo `short`<`int`, ampak velikosti določi prevajalnik glede na platformo)
    - ==definirani tipi== (iz `struct`, `union`, `class`, ...) $\rightarrow$ predstavitev odvisna od jezika
- Preverjanje pravilnosti tipov v izrazih programa (po pravilih jezika)
  (npr. `int+int`$\rightarrow$`int`, nižji tip se prevede v višji tip, ...)

Rekurzivni podatkovni tipi: kazalci (z znano velikostjo) namesto vrednost structa (neskončna struktura)

Simbolna tabela mora vsebovati preslikave:
- ime spremenljivke, "formal-parameter name" - tip
- ime metode - tip rezultata, parametri, lokalne spremenljivke
- ime razreda - deklaracije spremenljivk in metod

Preverjanje uporabe simbolov s pravili tipov - potek v 2 fazah:
1. Gradnja simbolnih tabel s pomočjo obiskovalcev (in preverjanje za večkratne deklaracije spremenljivk)
2. Preverjanje tipov vseh stavkov in izrazov s pomočjo obiskovalcev

Pogosti triki:
- overloadanje operatorja + (npr. seštevanje celoštevilskih in realnih vrednosti)
- obe strani prireditvenega stavka morata imeti enak tip (ali pa mora biti desen tip podtip levega)
- pridobitev tipov rezultata in argumentov metode iz simbolne tabele

Obravnavanje napak: kljub napaki tipa naj se previden tip vseeno vpiše v simbolno tabelo za nadaljne preverjanje ostalih tipov.
Vseeno pa ne pustimo napačnih programov v nadaljnje faze prevajanja.
### Preverjanje levih vrednosti (vrednosti z naslovom)
Potrebno, ker preverjanje tipov tega ne ujame
> [!example] Primer
> `2=3*5;` je s strani preverjanja tipov vredu
### Izračun konstantinih vrednosti
Včasih potrebno, včasih samo kot optimizacija
> [!example] Primer
> `char str[128+1];` $\rightarrow$ `char str[129];` - potrebno
> `x = sizeof(int);` $\rightarrow$ `x = 4;` - potrebno
> `x = 1+3;` $\rightarrow$ `x = 4;` - možna optimizacija
### Preobtežene metode (overloading)
Preobtežene metode z istim imenom in tipom rezultata, ki jih ločijo različni parametri:
1. Preimenovanje definicij metod (mangling)
2. Preverjanje in popravljanje uporab teh metod z novimi imeni

> [!example] Primer
> `int max(int i, int j) {...}` $\rightarrow$ `int max2(int i, int j) {...}`
> `int max(int i, int j, int k) {...}` $\rightarrow$ `int max3(int i, int j, int k) {...}`

Kazalci lokacij definicij imen metod iz razreševanja imen so tako odvisni od razreševanja tipov parametrov