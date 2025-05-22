# (Metodologije razvoja)
Metodologije razvoja:
- klasičen pristop
- agilno iterativen pristop
- agilni pristop (npr. scrum, kanban, ...)

Agilno iterativen pristop: več iteracij, v vsaki delamo:
1. zajem zahtev in predlog projekta
2. analiza
3. načrtovanje
4. implementacija
5. predaja naročniku

### SCRUM
Agilna metoda
==Product backlog==: zgodbe uporabnika (user stories)
==Sprint 0==: vzpostavitev okolja
==Izdaje (release)==: sestavljeni iz večih iteracij
==Iteracij (sprint)==: trajajo 2-4 tedne
- sprint planning meeting (naročnik): na začetku definiramo naloge v iteraciji
- delo (npr. 3 tedne): 1 točka = 1 delovni dan (6 ur dela)
- sprint review meeting (naročnik): pregled narejenega
- retrospective meeting (ekipa): dobre in slabe izkušnje, komentar prešnjih sprememb dela
Vloge:
- product owner: skrbi za funkcionalnosti izdelka
- ==scrum master==: skrbi za dogovorjeno delo, sestanke
- team member
# Predlog projekta (project proposal)
### Povzetek projekta
200-250 besed
### Projektna ideja (project introduction)
1. Ozadje: opis domene in konteksta projekta (kaj že obstaja, kaj se dogaja)
2. Področje in motivacija: opis problema in motivacije/namena za reševanje (kaj so problemi in kako bi jih rešili)
3. Namen: koristi projekta za organizacijo/stroko/znanost (kakšna je zamisel in kaj nameravamo doseči - koristi za uporabnika)
4. Cilji: konkretni, preverljivi in možno ovrednoteni cilji projekta (kaj želimo s projektom doseči, kaj bo končni rezultat)
5. Smernice za rešitev: možne preference in omejitve
6. Končni uporabniki: opis končnih uporabnikov

Pred bullet-pointi zmeraj vsaj en stavek
### Upravljanje projekta
Kako si bomo razdelili delo - kdo bo za kaj odgovoren, kdo je backup če kdo manjka (za splošno področje)
Kako bomo organizirani (scrum/..., če ni čisti napiši prilagoditve)
Kako se bomo usklajevali in razreševali napake

Tabela: oštevilčena opravila in podopravila (1.2, 12.3, ...) - član1 | član2 | ... (za vsako opravilo/podopravila določi % koliko bo kater član sodeloval pri projektu)
### Projektni načrt
Identifikacija aktivnosti (npr. vodenje projekta, analiza, načrtovanje izdelka, izdelava backenda, izdelava unit in integracijskih in uporabniških testov, testiranje, pregled literature, vzpostavitev okolja, zajem zahtev, pisanje poročila, analiza)
#### Ganntogram
Nariši v PlantUML (Microsoft Project) - https://plantuml.com/plantuml/ ti izriše diagram
- časovnica
- naloge/aktivnosti
- stolpci (predstavljajo trajanje projekta)
- mejniki (pomembne faze)
- puščice (odvisnosti med aktivnostmi)
- barve - označi kritično pot (če se podaljša katera od aktivnosti na kritični poti se podaljša cel projekt) z drugo barvo (vodenje projekta zihr, ampak to ignoriraj)

Aktivnosti morajo bti poslavljene na najzgodnejši začetek
Planira se, da se ne dela med vikendi in prazniki, od 2.5 do 5 ur delovnika
Projekt se je začel 24.2.2025, konča se 25.5.2025 -> 62 delovnih dni
Iteracije naj bodo označene

Popravljamo skozi celoten projekt
#### Diagram Pert
Narišemo samo na začetku projekta, izračunamo čas projekta in kritično pot, in to je to!
Vsaka aktivnost ima pripisan čas, povezave, lepše vidna kritična pot

OUI - ES EF LF EF moment (**Slika na telefonu**)
### Predstavitev skupine
Kdo bo projektni vodja
Za vsakega člana: znanje, izkušnje, kakšna bo njegova vloga, kdo ga nadomešča, notranje motivacije za nalogo (če so), katere jezike uporablja
### Načrt obvadovanja tveganj
Identificiraj 25 tveganj, jih uredi z matriko -> vsaj 12 (vsaj nekaj iz vsake vrste/kategorije/tipa) jih je potrebno načrtovati

Tehnična tveganja - uporabi cca 3 iz https://owasp.org/www-project-top-ten/
#### Identifikacija tveganj
Tabela: (**Slikano na telefonu**)
- ime in šifra tveganja (T1, T2, ...)
- opis tveganja (1 stavek)
- vpliv - na projekt (slab razvoj ipd) / na izdelek (izdelek neuporaben/nedodelan - tehnične lastnosti) / na posel (posledice za firmo)
- kategorija/vrsta/tip tveganja (tehnologija / ljudje / organizacija / orodja / zahteve / ocenjevanje) (**Slikano na telefonu**)
- verjetnost in učinek (glej spodaj)
#### Analiza tveganj
Ista tabela, izpolnemo:
- verjetnost (zelo visoka / visoka / zmerna / nizka / zelo nizka)
- učinek/posledice (usodne oz. katastrofalne / zmerne / dopustne / znosne / neznatne oz. nepomembne)

Tabelo še uredimo po matriki izpostavljenosti tveganj (**Slikano na telefonu**)
Matriko sam spiši ali pa referenciraj katero si uporabil
#### Načrtovanj tveganj
Tabela: (**Slikano na telefonu**)
- tveganje (ime in šifra)
- opis strategije/načrt obvadovanja tveganja (1-2 stavka)
- vrsta tveganja: avoid / minimize / accept - nej gre vse v maloro bomo že
### Finančni načrt
ČD (Človek Dan) = 8h
ČM (Človek Mesec) = 20 ČD = 160h
Rezultat COCOMO je v enotah ČM

Mi lahko na mesec cca 50, max 100h na mesec -> Študentski ČD (2.5 - 5h na dan)
62 ŠČD * 5 članov = 310 ŠČD
To številko primerjamo z rezultatom COCOMO (naredi pretvorbo ČD -> ŠČD)
Če je COCOMO cifra večja popravi parametre / če je COCOMO cifra zelooo manjša popravi scope projekta


1. Dobljena ocena
2. Preračun v ŠČM, ŠČU (študentske-človek-ure)
3. Prerazporediti po aktivnostih (Ganntogram) -> $\sum$ napora po aktivnostih < COCOMO2 napora
4. Preračun ŠČD/ŠČU v € (določitev urne postavke)
5. Neposredni (lahko obesimo na neko aktivnost - vemo kdaj in kje je nastala, npr. material, delo, storitve, ...) in posredni (ne moremo klasificirati, npr. hrana, pijača, izobraževanja, ...) projektni stroški
6. Končni izračun
### Poročilo o stanju / dnevnik sprememb (changelog)
Nujno: datum, opis, zakaj, posledice
Opcijsko: zadolžene osebe, trajanje, vrsta spremembe, prioriteta, status, na kaj ima vpliv
*MOGOČE UPORABIMO LINEAR/JIRA??*
# Osnutek sistema
## Specifikacija zahtev
Uporabniške zgodbe $\leftrightarrow$ funkcionalnosti (kaj mora sistem delati) so 1:1
Nefunkcionalne zahteve $\leftrightarrow$ funkcionalne zahteve so 1:n (1 nefunkc. lahko razrešimo/zagotovimo z večimi funkc. zahtevami)
### 1. Funkcionalne zahteve
#### 1.1 Specifikacija zahtev
Naštejemo funkcionalnosti - zahteve morajo biti opisane nedvoumno
#### 1.2. Specifikacija vmesnikov

##### 1.2.1 Zaslonske maske
Figma / screenshot prototipa
##### 1.2.2 Vmesniki do zunanjih sistemov
Za vsak API vmesnik / komunikacijo z zunanjim sistemom:
- format vhoda in izhoda (kateri podatki in v kakšnem formatu se pošiljajo)
- primeri uporabe APIja
### 2. Nefunkcionalne zahteve
Lastnosti sistema (zanesljivost, odzivni čas, backupi, ...)
Omejitve (varnost, sposobnost IO naprav, ...)
Razvojno okolje (sistem Home Assitant, programski jezik, razvojne metode, ...)

Vsako dobro definiramo, morajo biti merljive $\rightarrow$ razdelimo v 3 skupine:
- Zahteve izdelka: **vsaj 8**
    - dobavljen izdelek se mora obnašati na točno določen način
    - določena je hitrost
    - določena je zanesljivost
    - učinkovitost
    - uporabnost
- Organizacijske zahteve: **vsaj 1**
    - organizacijske politike in postopki
    - uporabljeni standardni procesi
    - implementacijske zahteve, ki morajo biti upoštevani pri razvoju
    - razvojne zahteve
    - zahteve okolja
- Zunanje zahteve: **vsaj 1**
    - dejavniki zunaj sistema in njegovega razvojnega procesa
    - zahteve glede interoperabilnosti
    - zakonodaja
    - etične zahteve
    - računovodske zahteve
![[(V) Projekt-Image-2.png]]
**Vsaka škatla bolje definirana v PDF, tudi primeri tam napisani**
### 3. Predstavitev funkcionalnih in nefunkcionalnih zahtev
#### 3.1 Primeri uporabe
Opisujejo interakcijo med sistemom in zunanjimi uporabniki, ki vodi do doseganja
določenih ciljev
##### 3.1.1 Diagram primerov uporabe
Glavni elementi: **glej PDF kaj vse mora vsebovati**
Levo vloge, na sredini primeri uporabe funkcionalnosti, desno zunanji sistemi
Polna puščica: asociacija - levi uporablja desnega (samo med primeri uporabe)
Prazna puščica: generalizacija - levi lahko uporablja vse asociacije desnega
Samo za primere uporabe:
- include: vedno ko se izvede leva se izvede tudi desna
- extend: če je pogoj Aja resničen, se izvede tudi B - pogoj se napiše v okvir ki kaže na puščico (**glej PDF**)
Avtomatično prožena funkcionalnost: prožilec narisan kot akter znotraj sistema (**glej PDF**)

Povezave med akterji so lahko samo generalizacije
Gledamo samo neposredno povezane na primere uporabe (vse kar le neposredno dostopa do sistema)
##### 3.1.2 Uporabniške zgodbe
Za vsako:
- Naslov: sporoča cilj uporabe/akterja (isto ime kot na diagramu)
- Akterji: ljudje/sistemi vključeni v primer uporabe - navedemo ali gre za vlogo, zunanji sistem ali zunanjo napravo
- Povzetek: zelo kratek (1 stavek) kaj primer uporabe počne/omogoča (**ime uporabniške vloge + lahko + navedba funkcionalnosti**)
- Osnovni tok: našteto zaporedje akcij izvedbe funkcionalnosti brez izjem
  Na koncu (možno): ime razširitvene točke : pogoj : ime primera uporabe ki se izvede ob resničnem pogoju
- Alternativni tokovi (1 ali več): razlika od osnovnega toka v enem koraku -> uspeh ali neuspeh funkcionalnosti po tem alternativnem toku (**vsaj 1 alternativni za vsak osnovni tok**)
- (Pred)pogoji: pogoji, da se primer uporabe lahko začne izvajati
- Posledice/učinki: kaj se zgodi v primeru uspeha/neuspeha primera uporabe
- Posebne zahteve: če realizacija primera uporabe zahteva posebnosti (npr. dodatna strojna oprema, zahtevani standardi, ...)
- Prioriteta:
    - Must Have (**max 60%**) - brez nje sistem ne dela
    - Should Have - pomembna za izboljšanje uporabnosti
    - Could Have (**cca 20%**) - edino če bo še čas / denar
    - Won't Have This Time - ideje za prihodnost
- Sprejemni testi: tabela (**za vsak osnovni in alternativni tok vsaj 1 sprejemni test**)
  ![[(V) Projekt-Image-3.png]]
- Pogostost uporabe: kako pogosto se bo uporabljal (**izmislimo si lestvico in ocenimo**)
### 4. Vrednotenje zahtev
Za vsako funkcionalno zahtevo:
1. Veljavnost – Ali sistem zagotavlja funkcije, ki kar najbolje zadovoljujejo potrebe stranke? Morda so se od faze pridobitve že spremenile.
2. Skladnost (angl. consistency) – Ali obstajajo med zahtevami kakšni konflikti?
3. Celovitost – Ali so vključene vse funkcije, ki jih zahteva stranka? Zajete morajo biti vse funkcije in omejitve, kot jih razume stranka.
4. Realističnost – Ali se zahteve izvedljive glede na razpoložljiv proračun in tehnologijo? Ne smemo pozabiti niti na časovno komponento izvedbe projekta (angl. schedule).
5. Preverljivost (angl. verifiability) – V izogib konfliktom med stranko in izvajalce morajo biti zahteve sistema zapisane v taki obliki, da so preverljive (priložena množica testov, ki demonstrira, da razviti sistem zadošča zahtevam).