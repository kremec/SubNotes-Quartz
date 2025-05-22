## Porazdeljeni sistem
Vozlišče: fizični stroj (npr. strežnik, telefon) / programski proces (npr. brskalnik)
==Porazdeljeni sistem==: skupina vozlišč, ki si prek komunikacijskih povezav izmenjujejo sporočila, da bi izvedla neko nalogo

Mnoge aplikacije so že po naravi porazdeljene: splet - brskalniki, strežniki, ...; telefon - oddajni stolpi, drugi telefoni, ...
Prednosti:
- zagotavljanje visoke stopnje ==zanesljivosti==: več vozlišč $\rightarrow$ ob izpadu ostala prevzamejo naloge
- obdelava ==prevelikih poslov== za eno vozlišče: npr, superračunalniki, spletni iskalniki, ...
- aplikacije z ==visokimi zahtevami zmogljivosti==: npr. ponudniki pretočnih vsebin, ...

Izzivi pri gradnji:
- ==obdelovanje napak==: sistem detekcije napak na kompleksnem sistemu vozlišč in omrežju
- ==komunikacija==: napake ob izpadu omrežja, pri prenosu, prisluškovanje, ...
- ==usklajevanje==: možne napake pri komunikaciji usklajevanja vozlišč
- ==raztegljivost==: učinkovitost sistema pod obremenitvami (veliko porabo virov - npr. procesorski čas, pomnilnik, pasovna dolžina, ...)
    - Merjenje obremenitve: št. obdelanih poslov v časovni enoti / št. hkratnih uporabnikov
    - Opažovanje količin: prepustnost - št. obdelav v časovni enoti / odzivni čas
    - Tipičen odziv: z večanjem obremenitev prepustnost raste do dosega kapacitete, po tem prepustnost ne narašča / sesutje sistema
    - Odvisna od: arhitekture, izvedbe, fizičnih omejitev (npr. pomnilnik, frekvenca, latenca, ...)
- ==odpornost==: ob napakah (npr. odpoved vozlišča, napake omrežja, ...) se delo nadaljuje nemoteno
- ==dostopnost==: delež časa, ko je sistem na voljo
- ==vzdrževanje==: običajno dražje od same vzpostavitve sistema
### Zgradba
Z vidika strojne opreme: skupina naprav, ki komunicirajo preko omrežja
Z vidika izvajanja: skupina procesov, ki komunicirajo preko mehanizmov medprocesorske komunikacije (npr. TCP, HTTP, ...)
Z vidika razvoja programske opreme: skupina šibko povezanih storitev, ki komunicirajo preko programskih vmesnikov (npr. RPC) - strežnik in odjemalec
## Komunikacijski sklad
Plasti:
- fizična plast
- ==povezovalna plast - Ethernet==: lokalni omrežni protokoli
- ==internetna plast - IP==: usmerjanje paketov podatkov v omrežju
- ==transportna plast - TCP==: zanesljiv prenos podatkov med procesi
- ==aplikacijska plast - HTTP/DNS/...==

Prenos podatkov:
- na pošiljatelju od višje proti niži plasti
- na prejemniku od nižje proti višji plasti
### UDP - nezanesljiv prenos podatkov
Kadar potrebujemo ==večjo prepustnost namesto zanesljivosti== $\rightarrow$ ni vzpostavljanja povezav, potrjevanja paketov ali nadzora pretoka in zasičenosti omrežja
### TCP - Zanesljiv prenos podatkov
Prenos paketa preko množico usmerjevalnikov:
- rabimo naslove vozlišč (IPv4/IPv6) in usmerjevalne tabele
- vsakemu procesu dodelimo ==vrata (port)==: logična oznaka procesa v omrežju

TCP nadgrajuje protokol IP:
- ==oštevilčeni paketi== $\rightarrow$ zagotavlja vrstni red paketov, ni manjkajočih/podvojenih paketov
- ==kontrolna vsota== (npr. CRC) $\rightarrow$ v paketih ni napak
- ==ekspresivna komunikacija== $\rightarrow$ potrjevanje prejema, sporočanje prostora v medpomnilniku prejemnika

==Vtičnica==: vmesnik med transportno in aplikacijsko plastjo - ==naslov vozlišča + vrata + protokol==
<br><br><br><br><br><br>
#### Povezava strežnik-odjemalec / pasivni-aktivni partner
##### Vzpostavitev povezave
Strežnik pripravi vtičnico in pasivno čaka, da se odjemalec nanjo poveže
Odjemalec pripravi vtičnico in aktivno dela na vzpostavitvi povezave
==Tristopenjsko rokovanje==:
![[Posredovanje sporočil-Image-1.png|300]]
##### Vzpostavljena povezava
==Nadzor pretoka==: mehnizem preprečevanja preobremenitve prejemnika
- prejemnik poleg ACK pošlje velikost prostega medpomnilnika

==Nadzor zasičenosti omrežja==: mehnizem preprečevanja preobremenitve omrežja
- ==okno zasičenosti== (congestion window) = št. poslanih paketov na poti brez prejete potrditve
  potrjen paket $\rightarrow$ okno eksponentno povečamo / izgubljen paket $\rightarrow$ zmanjšamo okno

Odjemalec in strežnik sta enakovredna - dvosmerna komunikacija
##### Zapiranje povezave
Zapiranje spet zahteva večstopenjsko rokovanje $\rightarrow$ če bomo povezavo kmalu spet rabili, je ==raje ne zapremo==
Sistem mora še počakati na morebitne pakete, ki so še na poti $\rightarrow$ ==povezave ne zapemo takoj==
### TLS - varnost v omrežjih
Nadgradnja TCP:
- ==enkripcija== $\rightarrow$ vsebino lahko bere le prejemnik
    - ==vzpostavitev povezave: asimetrična enkripcija== - dogovor za simetrični ključ
    - ==prenos podatkov: simetrična enkripcija== - hitrejše, simetrični ključ se redno spreminja
- ==avtentikacija== $\rightarrow$ overovitev sogovornika s certifikatom
- ==integriteta== $\rightarrow$ overovitev vsebine s hashem (preprečimo napake pri prenosu / zlonamerno spreminjanje vsebine)
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
## Programski vmesniki (API-ji)
Odjemalec kliče poeracije, ki jih strežnik ponuja preko programskega vmesnika
Vmesnik skrbi za prevajanje sporočil v klice funkcij na strežniku - ==RPC== (Remote Procedure Call)
Komunikacija je lahko:
- neposredna / posredna (preko posrednika)
- sinhrona (odjemalec blokira, dokler strežnik ne odgovori) / asinhrona

==Idempotenca metod==: v shrambi se ne sme nič spremeniti, četudu metodo izvedemo večkrat zapored (npr. zaradi napake omrežja odjemalec ponovno pošlje zahtevo)
- Create Read Update Delete (CRUD): 4 osnovne operacije na podatkovnih shrambah

Standardizacija zahtev in odgovorov:
- tekstovno - XML / JSON
- binarno - Protocol Buffers (hitrejše zaradi binarnega zapisovanja)
### REST
==REST==: priporočila oblikovanja programskih vmesnikov za protokole HTTP
==RESTful==: programski vmesniki, zgrajeni po načelih REST
Glavna načela:
- ==obdelave nimajo stanja== $\rightarrow$ vsaka zahteva mora vsebovati vse informacije za obdelavo
- odzivi so označeni z ==dovoljenjem za medpomnenje==
- koncept ==zahteva-odgovor== (ni dvosmerne komunikacije)
- za (de)kodiranje podatkov uporabljamo XML/==JSON==

Omejitve na HTTP/1.1: povezavo ohranja odprto, zaporedni prenosi
Izboljšave s HTTP/2 in HTTP/3: binarni protokol, multipleksiranje povezav
Primeren za enostavne programske vmesnike
#### Koncept zahteva-odgovor
Odjemalec:
- lokacijo vira poda z URL (`http(s)://strežnik:vrata/vir?filter`)
- v glavi zahteve poda: želeni format (`application/json`) in HTTP metodo (GET, POST, PUT, ...)

Strežnik:
- v glavi odgovora poda: format zapisa in kodo odgovora (200, 300, 500, ...)
- v telesu odgovora poda vsebino
### gRPC
==gRPC==: vzorec klicanja oddaljenih metod
Glavna načela:
- za kodiranje podatkov uporablja ==binarni protokol Protocol Buffers== $\rightarrow$ neodvisen od programskega jezika
- za prenos podatkov uporablja protokol HTTP/2
- omogoča dvosmerni tok podatkov, majhno latenco in veliko pasovno dolžino

Primeren za kompleksne programske vmesnike
#### Vzorec RPC
Klicanje oddaljenih metod na podoben način kot lokalne:
1. Odjemalec:
    - vhodne argumente metode zakodira (marshalling)
    - jih prenese na strežnik skupaj z zahtevo za izvajanje metode
2. Strežnik:
    - argumente dekodira (unmarshalling)
    - zažene metodo
    - rezultate zakodira in pošlje nazaj
3. Odjemalec:
    - dekodira sporočilo
    - zahtevane strukture vrne kot rezultat
#### Protocol Buffers
==Opisna datoteka vključuje strukture in metode==
==Prevajalnik protoc== iz opisne datoteke pripravi paket za objekte in klice metod na strežniku
- paket prevedemo skupaj s kodo