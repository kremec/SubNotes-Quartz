Topics: 
- - -
### Logična organizacija podatkov
==Datoteka==: osnovna zaključena zbirka podatkov, ki jo lahko naslovimo preko imena, sestavljena iz vsebine in atributov (meta podatkov)
==Imenik==: omogoča združevanje datotek - vsebuje datoteke ali druge imenike (hierarhija ==podimenikov==, ==nadimenikov== in ==korenskega imenika==)

Pot do datoteke: seznam imen imenikov od ustreznega izvornega imenika do dane datoteke
- ==abolutna pot==: začetek v korenskem imeniku
- ==relativna pot==: začetek v trenutnem delovnem imeniku

Ločilo poti: ==/== (Unix) oz. ==\ == (Windows)
Imeniki: ==.== - trenutni imenik, ==..== - imenik starša trenutnega imenika, ==~== - domači imenik uporabnika
### Datoteke
Tipi datotek:
==Navadna datoteka== (-): poljubna interna struktura, pogosto končnica podaja vrsto

==Imenik== (d): seznam ==imeniških vnosov== (ime datoteke + kazalca na vsebino in metapodatke)

==Simbolična povezava== (s): posebna datoteka z naslovo ciljne datoteke
Ukaz: `ln -s <original> <mehka>`
![[OS_Datoteke_MehkaPovezava.png|400]]

==Trda povezava==: dodaten imeniški vnos za isto datoteko
Ukaz: `ln <original> <trda>`
![[OS_Datoteke_TrdaPovezava.png|250]]

==Bločna naprava== (b) / ==znakovna naprava== (c): operacije na takšni datoteki se nanašajo direktno na napravo, dostop po blokih / znakih

==Imenovana cev== (p) / ==lokalna vtičnica== (s): mehanizma medprocesne komunikacije preko datotek in datotečnih dovoljenj
### Kodiranje datotek
==Kodiranje ASCII== (American Standard Code for Information Interchange):
7b kodni prostor, 95 vidnih + 33 kontrolnih kod

Internacionalizacija, saj manjkajo ne-angleški znaki:
- YUSCII
- ASCII 8b = ASCII Latin1

==Standard Unicode==: svetoven nabor znakov
21b kodni prostor, 143852 znakov in 154 pisav
Prvih 256 znakov je enakih ASCII Latin1

==UTF== (Unicode Transformation Format):
- ==UTF-32==: 4B, vsaka vrednost predstavlja eno kodo - prostorsko neučinkovito
- ==UTF-16==: 1-2B, Windows, CLI, JavaScript, ...
- ==UTF-8==: razširjen ASCII (ujemanje v prvih 128 znakih), 1-4B na znak, svetovni splet in Unix sistemi

Skok v novo vrstico: ==LF== - naslednja vrstica, ==CR== - skok na začetek vrstice
- CR+LF: zaradi "kompatibilnosti s tiskalniki", Windows
- LF: Unix, Linux, macOS, ...
- CR: ZX Spectrum, Commodore C64