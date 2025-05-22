Z API endpointi navzven odpremo operacije, ki zaganjajo poslovno logiko
API klici počasnejši od interne logike $\rightarrow$ čim manj komunikacije preko API klicev
### Zgodovina
- RPC / RMI / CORBA: stare tehnologije
- SOAP / REST: dandanes standard
- GraphQL / gRPC: novejši načini
## REST (REpresentational State Transfer)
### Sestava
- ==HTTP metoda==: operacija 
- ==URL pot virov==: vir zbirke (npr. `/razmerja`) ali instance (npr. `/razmerja/312`)
### HTTP HEADER
#### HTTP metoda
==CRUD== (Create Read Update Delete) operacije:
- GET: branje - odgovor 200 OK
- HEAD: branje HTTP zaglavja brez vsebine
- POST: ustvarjanje novega vira - odgovor 201 Created
- PUT: posodabljanje obstoječega vira - odgovor 200 OK
- PATCH: delno posodabljanje obstoječega vira
- DELETE: brisanje - odgovor 204 No Content

Ostale operacije:
- obravnavamo kot podvir (npr. `/razmerja/312/skleni`, `.../prekini`, ...)
- ustvarimo nov navidezen vir (npr. POST `/iskanje`)
#### MIME formati
Specifikacija formata sporočil:
- application/json
- application/xml
- application/pdf
- image/jpeg
- ...

V HTTP zaglavje dodamo header `Content-Type: ...` oz. `Accept: ...`
<br><br><br><br><br>
#### HTTP kode
Kode uspešnih procesiranj:
- 200 OK – Odgovor na uspešno akcijo
- 201 Created – Odgovor na uspešno akcijo, ki rezultira v kreiranje vira.
- 204 No Content – Odgovor na uspešno akcijo brez vsebine odgovora
- 304 Not Modified – Informacija odjemalcu, da drži aktualno medpomnjeno instanco

Kode napak:
- 400 Bad Request – Zahteva je neustrezno oblikovana, vsebine ni mogoče razčleniti, podatki manjkajo
- 401 Unauthorized – Avtentikacija uporabnika ni uspešna
- 403 Forbidden – Avtorizacija uporabnika do vira ni uspešna
- 404 Not Found – Zahteva po viru, ki ne obstaja
- 405 Method Not Allowed – HTTP metoda uporabniku ni dovoljena
- 410 Gone – Vir na URL ne obstaja več (uporabno za verzioniranje)
- 415 Unsupported Media Type – Tip vsebine zahteve ni veljaven
- 422 Unprocessable Entity – Validacijska napaka
- 429 Too Many Requests – Zahteva zavrnjena zaradi preobremenitve strežnika ali preveč zahtev (uporaba X-Rate-Limit-... značk)
- 500 Internal Server Error – Generalna napaka na strežniku
### URL
URL gnezdimo do max 3-4 nivoje, zmeraj se začne z verzijo APIja (`https//.../v1/...`)
#### Ostranjevanje (seznamov)
Omejujemo z URL parametri: `?offset=...&limit=...`; v response HTTP zaglavje dodamo `X-Total-Count`
#### Sortiranje, filtriranje in iskanje
Omogoča generično poizvedovanje po več poljih hkrati. URL parametri: sortiranje z `?order=...`, filtriranje z `?where=...`, iskanje z `?q=...`
#### Delne predstavitve virov
Omogoča pošiljanje le relevantnih polj v responsu. URL parametri: `?fields=...`

#### Povezovanje virov
V JSON odgovor lahko namesto dejanskih podatkov podamo link do njih
Prvi klic krajši, potreben še nov klic če te podatke rabimo $\rightarrow$ lazy loading