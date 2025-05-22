### Agilni razvoj
- iterativni razvoj v pogostih inkrementih
- zajem zahtev, načrt, izvedba in testiranje so prepleteni - zmeraj se pričakuje spreminjanje zahtev
- tesno sodelovanje z naročnikom: specifikacija prednostnih nalog/zahtev in vrednotenje iteracij
- lastni pristop do dela brez predpisanih procesov
- aktivno odpravljanje zapletenosti sistema
- minimalna dokumentacija - fokus na hitro zagotovitev delujoče programske opreme

==Prilagajanje navzgor==: uporaba agilnih metod za razvoj večjih sistemov programske opreme, ki jih majhna skupina ne more razviti
==Prilagajanje navzven==: uvedba agilnih metod v veliko organizacijo z dolgoletnimi izkušnjami pri razvoju programske opreme

Agilne metode so zato tudi najprimernejše za razvoj nove programske opreme in ne za vzdrževanje programske opreme:
- pomanjkanje dokumentacije izdelka,
- vključenost naročnika v razvojnem procesu,
- ohranjanje kontinuitete razvojne skupine
### Ekstremno programiranje (XP)
Tehnika agilnega razvoja:
- nove različice se lahko izdelajo večkrat na dan
- inkrementi se dostavijo strankam vsaka 2 tedna, izgradnja se sprejme le ob vseh uspešno opravljenih testih

Dobre prakse:
- ==inkrementalno načrtovanje==: zahteve kot uporabniške zgodbe se razdelijo v razvojne naloge
- ==majhne izdaje==: funkcionalnosti se dodajajo šele po razvitju MVP
- ==enostaven načrt==: načrtovanje le trenutnih zahtev (nič več)
- ==razvoj z vnaprejšnjim testiranjem==: avtomatizacija testov funkcionalnosti pred implementacijo
- ==preurejanje kode (refactoring)==: ohranjanje enostavnosti s stalnim preurejanjem izvorne kode
- ==programiranje v paru==: delo razvijalcev v parih za medsebojno podporo
- ==skupinsko lastništvo==: razvijalci delajo - prevzamejo odgovornost - na vseh področjih sistema
- ==stalna integracija==: takoj po koncu dela na nalogi se to integrira v celotni sistem
- ==trajnostni tempo==: nesprejemljivost nadurnega dela - manjša kakovost kode in produktivnosti
- ==stalna prisotnost stranke==: stranka mora biti na voljo polni delovni čas
### SCRUM
Agilna metoda, ki se osredotoča na ==upravljanje iterativnega razvoja programske opreme== namesto na specifične prakse agilnega razvoja
3 faze:
1. ==Začetna faza načrtovanja==: določitev splošnih ciljev projekta in oblikovanje arhitekture sistema
2. ==Vrsta ciklov sprinta==: razvoj inkrementov sistema v okviru vsakega cikla
3. ==Faza zaključka projekta==: dopolnitev dokumentacije (npr. ogrodja sistemske pomoči,  uporabniški priročniki, ... ) in vrednotenje pridobljenih izkušenj na projektu

Pomembni termini:
- ==razvojna skupina==: samoorganizirana skupina max 7 razvijalcev
- ==potencialno dostavljiv inkrement izdelka==: izdelek v končnem stanju brez potrebnega dodatnega dela za njegovo vključitev v končni izdelek
- ==backlog izdelka==: seznam opravil razvojne skupine
- ==lastnik izdelka==: zahteve iz backloga prednostno razvrsti za razvoj
- ==Scrum==: vsakodnevno srečanje celotne razvojne skupine - pregled napredka in načrtov
- ==Scrum master==: vodi razvijalce in jih ščiti pred motilnimi zunanjimi vplivi (stranka)
- ==Sprint==: razvojna iteracija, ki običajno traja od 2 do 4 tedne
- ==hitrost==: ocena deleža možne implementacije zahtev v enem sprintu - ocenjevanje razvoja
### Zajem zahtev
![[Agilni razvoj programske opreme in zajem zahtev-Image-1.png]]
Vrste zahtev:
- uporabniška zahteva: namenjena stranki - izjave v naravnem jeziku / diagrami storitev in operativne omejitve
- sistemska zahteva: namenjena stranki in izvajalcu - strukturiran dokument z opisi funkcij sistema

Tipi zahtev:
- ==funkcionalne zahteve==: podrobnosti zahtevanih storitev in načinov delovanja sistema
- ==nefunkcionalne zahteve==: lastnosti sistema (npr. zanesljivost, odzivni čas, ... ) in omejitve storitev (npr. časovne, razvojne, ... )
    - zahteve izdelka: določeno obnašanje izdelka
    - organizacijske zahteve: določeni organizacijski pristopi
    - zunanje zahteve: zunanji dejavniki

Zahtevane lastnosti izdelka razdelimo v kategorije
- MUST-have
- SHOULD-have
- COULD-have
- WON’T-have

Zahteve so lahko osnova za
- ponudbo - odprte za različne interpretacije
- pogodbo - natančno opredeljene
#### Pridobivanje zahtev
1. Tehnično osebje s strankami pridobi informacije o problemski domeni, zahtevah in omejitvah sistema
2. Razvrstitev in organizacija zahtev po prioriteti

Možne težave:
- stranka slabo opisuje želje
- nasprotujoče zahteve različnih strank
- spreminjanje zahtev tekom analize ali razvoja
#### Specifikacija zahtev
Čim bolj natančen in popoln opis zahtev:
- opredelitev entitete
- opis vhodov in rezultatov
- pogoji za delovanje
#### Vrednotenje zahtev
Dokazovanje, da zahteve določajo sistem, ki si ga stranka želi:
- Veljavnost (Ali sistem zagotavlja funkcije, ki kar najbolje podpirajo potrebe stranke?)
- Skladnost (Ali obstajajo med zahtevami kakšni konflikti?)
- Celovitost (Ali so vključene vse funkcije, ki jih zahteva stranka?)
- Realističnost (Ali se lahko zahteve izvedejo glede na razpoložljivi proračun in tehnologijo?)
- Preverljivost (Ali lahko zahteve realno preverimo?)
#### Upravljanje zahtev
Obvladovanje spreminjajočih se zahtev med analizo in razvojem
- Identifikacija zahtev: enolična ==identifikacija zahtev==
- Proces upravljanja sprememb: ==ocenjujevanje vpliva in stroškov sprememb==