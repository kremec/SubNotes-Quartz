### Pristopi implementacije
==MVC==:
- Model: podatkovni model
- View: prikaz izgleda
- Controller: obravnava akcij uporabnika (npr. click, scroll, ...)
#### Strežniški model (server-side MVC)
Procesiranje (obremenitev) na strežniku
Odjemalec delno procesira izgled, pripravljen na strežniku
Storitve poslovne logike skrite odjemalcu
![[Spletne aplikacije, Angular-Image-1.png|400]]
Problemi:
- potrebno ogrodje za generiranje HTML
- sklopljenost front-enda in back-enda
- omejitve zmogljivosti strežnika
- težavno skaliranje - stanje ohranja strežnik
#### Odjemalski model (client-side MVC)
Procesiranje (obremenitev) na odjemalcu
Spletni strežnik za serviranje statičnih vsebin preko CDN, storitveni strežnik za serviranje stateless storitev preko API
![[Spletne aplikacije, Angular-Image-2.png|400]]
### Koncepti
==Single Page Application==: nalaganje osnovnega HTML, CSS, JS se izvede le enkrat - nadaljnjo kontrolo nad izvajanjem UI ima prskalnik
==Responsive design==: prilagajanje vidnosti in velikosti elementov glede na velikost zaslona
==Fluidni koncept vmesnika==: zvezno prilagajanje vidnosti in velikosti glede na velikost zaslona, orientacije in velikosti okna
==Mobile-first design==: uporabniški vmesnik deluje na vseh tipih naprav, mobile pogled osredotočen na osnovne tokove uporabnikov
==HTML5 API==: touch gestures, geolokacija, kamera, žiroskop, pospeškometer, Bluetooth, NFC, ...
## Angular
View: izgled preko HTML in "Ng direktiv" (NgIf, NgFor, NgStyle, ...)
Controller: TS spreminja izgled in podatke
Model: TS service dostopa do API

Življenjski cikel komponent (component lifecycle)
Povezava s podatki (data binding)
Validacija vnosov (input validation)