## Teorija
Vhod: AST z atributi
Izhod: AST z dodatnimi atributi
### Spremenljivke
Tipi:
- ==statične== (definirane zunaj funkcij): ==ime labele, velikost, začetna vrednost==
    - fiksni pomn. naslov
    - življenjska doba celega programa
- ==avtomatske== (definirane v funkciji - lokalne spremenljivke in/ali parametri): ==odmik of SP, velikost==
    - spremenljiv pomn. naslov
    - življenjska doba izvajanja funkcije
- ==registrske==
- ==zunanje==

==Komponente zapisov== "znotraj" spremenljivke
#### Pomnilnik
Vrednosti na skladu dobimo z odmiki
Vrednosti na kopici dobimo preko kazalcev, ki kažejo nanje
![[Klicni zapisi in spremenljivke-Image-1.png|250]]
### Klicni zapisi
Lokalne spremenljivke (in parametri) funkcije se instancirajo ob klicu in uničijo ob izhodu
Implementacija:
- navaden LIFO sklad: slab za veliko `push` in `pop` operacijami hkrati (ob vstopih in izstopih iz funkcije), ni dostopa do poljubne vrednosti na skladu
- seznam s kazalcem na sklad, ki se pomika glede na potreben prostor informacij funkcije

==Klicni zapis / okvir sklada==: del pomnilnika (sklad), ki pripada funkciji med izvajanjem
![[Klicni zapisi in spremenljivke-Image-2.png|400]]
Stara vrednost FP: ob koncu funkcije SP = FP, FP moramo od prej shraniti
Začasne spremenljivke: v primeru premalo registrov za večje operacije/izračune

FP izhodiščna točka + zbliža lokacije:
- navzdol lokalne spremenljivke
- navzgor statična povezava in parametri

Odvisno od dogovora:
- SP: kazalec na zadnjo zasedeno lokacijo
- FP: kazalec na prvo lokacijo tik pred klicnim zapisom
- Povratni naslov: hramba vrednosti posebnega registra, ki se ob vsakem klicu spremeni

==Klicna konvencija==: dogovor o načinu pošiljanja argumentov, parametrov, rezultatov; upravljanju z registri ob klicih
- Dogovor koliko/katere/kakšne in v katerem vrstnem redu prenašamo argumente po registrih (hitrost), ostalo preko sklada (več prostora)
- Shranjevanje registrov s strani klicočega procesa (zavarovanje) / klicanega procesa (točno ve katere registre bo uporabljal, ostalih ne shranjuje)

Čim večja uporaba registrov $\rightarrow$ prevajalnik lahko optimizira uporabo registrov na podlagi analize delovanja funkcij (ne shranjuje registrov, novo neuporabne registre prepiše)
Razlogi, da vseeno uporabimo pomnilnik:
- pošiljanje vrednosti preko reference (kazalca na pomnilniški naslov)
- seznami, ki potrebujejo aritmetiko kazalcev za upravljanje z vrednostmi
- premalo prostora za vse vrednosti
- prevelika vrednoswt za en register (čeprav prevajalnik lahko razporedi vrednost po delih preko več registrov)
#### Gnezdene funkcije
Notranja funkcija lahko dostopa do parametrov zunanjih funkcij / dosegov:
- ==statična povezava==: kazalec na sklad zunanje funkcije
- ==display==: globalni seznam kazalcev na klicne zapise funkcij po globinah
- ==lambda lifting==: potrebne spremenljivke zunanjega dosega prevajalnik poda kot dodatne argumente
>[!example] Primer
>```
>fun f1 (p1: )
>  var v1
>  fun f2 (p2: )
>    var v2
>    fun f3 (p3: )
>      var v3
>  fun f2' (p2': )
>    var v2'
>```
>![[Klicni zapisi in spremenljivke-Image-3.png|200]]
>Ko `f2` kliče `f3` pusti na skladu argument in statično povezavo, ki kaže na vrh klicnega zapisa `f2`
>(preko katerega `f3` lahko pride do `v2`, `p2` ali do statične povezave do `f1`, preko katere pride do `p1`)
#### Funkcije višjega reda
==Funkcije višjega reda==: podpora gnezdenih funkcij in funkcijskih spremenljivk $\rightarrow$ vrednosti lokalnih spremenljivk (klicni zapis notranje funkcije) je potrebno tudi po izhodu obdržati $\rightarrow$ shranjevanje na skladu
>[!example] Primer
>Gnezdene funkcije in funkcijske spremenljivke:
>```
>fun f(x) =
>  let fun g(y) = x+y
>  in g
>  end
>
>val h = f(3)
>val g = h(5)
>```
>Viseči kazalec:
>```
>int* f (int x) { return &x; }
>```
## Implementacija
Različne arhitekture imajo različne standarde strukture okvirja sklada $\rightarrow$ uporabimo abstrakcijo, na podlagi katere naredimo implementacije za posamezne arhitekture
