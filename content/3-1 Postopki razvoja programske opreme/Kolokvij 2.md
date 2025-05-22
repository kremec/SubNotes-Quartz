### Podatkovne baze
#### JDBC
==Open Database Connectivity (ODBC)==: standardni API protokol za dostop do DBMS
==Java Database Connectivity (JDBC)==: javanska knjižnica za vzpostavljanje povezave na bazo, izvajanje SQL povpraševanj in strukturo rezultatov povpraševanj
- Tip 1 - ==JDBC-ODBC most==: pretvorba JDBC v ODBC klice
- Tip2 - ==delni javanski gonilnik==: JDBC klici direktno na specifičen gonilnik DB
- Tip 3 - ==javanski/mrežni gonilnik==: vmesni sloj pretvori ukaze
- Tip 4 - ==čisti javanski gonilnik==: direktna komunikacija z DB

Privzeto se SQL ukazi samodejno potrdijo (`autoCommit`)
Transakcijsko izvajanje: `autocommit=false` $\rightarrow$  ... $\rightarrow$ `commit()`/`rollback()`

==Bazen povezav==: predpomnilnik povezav na DB (počasno vzpostavljanje in prekinjanje povezav)
#### ORM (JPA)
==Object Relational Mapping==: tehnika premoščanja razkoraka med objektnim in relacijskim modelom
- avtomatska preslikava objekti $\leftrightarrow$ relacijske tabele
- ni pisanja SQL stavkov
- lažja konfiguracija, upravljanje transakcij in logiranje

##### Anotacije
`@Entity`: entitetni razred
Ključi:
- `@Id`: atribut kot primarni ključ
- `@GeneratedValue`: `strategy=SEQUENCE/IDENTITY/TABLE/AUTO`

Tabele:
- `@Table`: določanje vrednosti `name, schema, uniqueConstraints, ...`
- `@SecondaryTable`: razporejanje podatkov istega tipa (objektov) po večih tabelah

Atributi:
- `@Column`: spreminjanje privzetih vrednosti `name, table, nullable, unique, ...`
- `@Temporal`: določanje oblike shranjevanja Date polj `DATE/TIME/TIMESTAMP`
- `@Transient`: označimo atribute, ki se naj ne zapišejo v DB
- `@Enumerated`: značimo naštevne tipe (enum)

Relacije med entitetami:
- `@OneToOne/@OneToMany/@ManyToOne/@ManyToMany`: določimo `FetchType=EAGER/LAZY`
- `@JoinTable`

Preslikava dedovanja: `@Inheritance`
- strategija enojne tabele: vsi atributi celotne hierarhije sploščeni v eno tabelo
- strategija pridružitve: tabela za vsak sloj hierarhije, isti primarni ključ enitete v korenski tabeli se uporablja zanjo v vseh tabelah
- strategija tabele na konkreten razred: tabela za vsak razred, atributi vrhnjih slojev se preslikujejo navzdol
##### Osnovne operacije nad entitetami
Kreiranje - `persist()`: če obstaja proži napako
Brisanje - `remove()`: sinhronizacija ob `flush()`
Posodabljanje - `merge()`: sinhronizacija ob `flush()`, razveljavitev lokalnih sprememb ob `refresh()`
Povpraševanje:
- `find(entitetni razred, primarni ključ)`: če ne najde vrne null
- `getReference(entitetni razred, primarni ključ)`: če ne najde proži napako
##### JPQL
Jezik povpraševanja po entitetah, ki kombinira sintakso SQL z izraznostjo OOP
- statična povpraševanja - `createNamedQuery("...")`: definiramo v anotacijah / XML
- dinamična povpraševanja - `createQuery("...")`: če ne poznamo scenarija povpraševanja vnaprej
Število rezultatov: `getSingleResult()` / `getResultList()`
Uporaba parametrov kot pri PreparedStatementih (zaporedna številka / po imenu)
Ostranjevanje rezultatov: `setMaxResults()` / `setFirstPosition()`
<br><br><br><br><br><br><br><br>
### OpenAPI3
Sklopi:
- ==info==: opis - title, description, contact, licence, version
- ==security==: avtorizacijska shema - scheme (npr. basic / bearer / OAuth / ...), bearerFormat
- ==paths==: URL poti do posameznih virov
- ==tags, externalDocs==: označbe in dokumentacija
- ==components==:
    - requestBodies: description, required, content/schema - uporaba referenc na tipe objektov
    - responses: code, description
    - links: uporaba rezultatov ene operacije kot vhod za drugo operacijo
#### Java anotacije
- `@Operation`: opis
- `@RequestBody`: vsebina zahtevka
- `@ApiResponse`: vsebina odgovora
- `@Callbacks`: množica zahtevkov
- `@Parameter`: parameter
- `@Link, @LinkParameters`: design-time povezava odgovora
- `@Content`: shema in primeri odgovora
- `@Schema`: vhodni izhodni podatki

- `@Info, @Contact, @Licence`: splošni metapodatki
- `@Extension, @ExtensionProperty`: razširitve in njihove lastnosti

- `@SecurityRequirement`: seznam zahtevanih varnostnih shem za operacijo
- `@SecurityScheme`: definicija varnostne sheme
- `@OAuthFlow`: definicija varnostne sheme
- `@OAuthFlows`: konfiguracija OAuth tokov
### Spletne aplikacije
==MVC==:
- Model: podatkovni model
- View: prikaz izgleda
- Controller: obravnava akcij uporabnika (npr. click, scroll, ...)

==Strežniški model==:
Procesiranje (obremenitev) na strežniku
Odjemalec delno procesira izgled, pripravljen na strežniku
Storitve poslovne logike skrite odjemalcu
Problemi:
- potrebno ogrodje za generiranje HTML
- sklopljenost front-enda in back-enda
- omejitve zmogljivosti strežnika
- težavno skaliranje - stanje ohranja strežnik
![[Spletne aplikacije, Angular-Image-1.png|400]]

==Odjemalski model==:
Procesiranje (obremenitev) na odjemalcu
Spletni strežnik za serviranje statičnih vsebin preko CDN, storitveni strežnik za serviranje stateless storitev preko API
![[Spletne aplikacije, Angular-Image-2.png|400]]

==Single Page Application==: nalaganje osnovnega HTML, CSS, JS se izvede le enkrat - nadaljnjo kontrolo nad izvajanjem UI ima prskalnik
==Responsive design==: prilagajanje vidnosti in velikosti elementov glede na velikost zaslona
==Fluidni koncept vmesnika==: zvezno prilagajanje vidnosti in velikosti glede na velikost zaslona, orientacije in velikosti okna
==Mobile-first design==: uporabniški vmesnik deluje na vseh tipih naprav, mobile pogled osredotočen na osnovne tokove uporabnikov
==HTML5 API==: podpora touch gestures, geolokacija, kamera, žiroskop, pospeškometer, Bluetooth, NFC, ...
### Docker
==Docker server/deamon==: izvaja gradnjo, izvajanje in distribucijo Docker vsebnikov
==Docker client==: komunicira z deamonom preko REST API-ja
#### Dockerfile
Nivoji:
- READ_ONLY: osnovna slika, uporabniške datoteke - aplikacija in odvisnosti
- READ_WRITE: izvajanje aplikacij

Direktive:
- `FROM <image>`: definiramo osnovno sliko (npr. alpine, ubuntu, ...)
- `RUN <command>`: zagon ukazov
- `CMD <command>`: privzeti zagon
- `EXPOSE <port>`: definiramo vrata za dostop do vmesnika
  Ob zagonu vmesnika vseeno potrebna zastava `-p <port>`
- `ENV <key>=<value>`: definiramo okoljske spremenljivke
- `ADD <src> <dest>`: kopira datoteke / direktorije / URL-je v datotečni sistem
  Ciljna pot mora biti relativna na izvorni imenik + znotraj konteksta gradnje
- `COPY <src> <dest>`: kopiranje znotraj vsebnika
- `VOLUME <mount>`: označena točka priklopa
- `USER <user>`: uporabnik, ki se uporabi pri izvedbi direktiv
- `WORKDIR <path>`: nastavi delovni direktorij pri izvedbi direktiv
<br>
### Kubernetes
![[Kubernetes-Image-1.png|400]]
==Strok (pod)==: Najmanjša namestitvena atomarna enota enega/več vsebnikov (ne kreiramo jih neposredno)
Vsebniki znotraj stroka si delijo: shrambo, IP naslov in vrata

==Namestitev (deployment)==: Deklarativni nadzor:
- namestitev in posodobitev strokov in replikacijskih nizov
- upravljanje replik (npr. vzpostavitev ob izpadih)

Ne glede na lokacijo posameznih strokov je namestitev storitve dostopna na statičnem IP

==Storitev (service)==: Abstrakcija logičnega nabora strokov - politika dostopa (spremembe arhitekture ne smejo vplivati na odjemalce)
Tipi storitev:
- ==ClusterIP== (privzeto): storitev znotraj gruče dostopna na IP naslovu
- ==NodePort==: storitev izpostavljena na vratih na IP naslovu gostitelja $\rightarrow$ vsak gostitelj v gruči ločeno
- ==LoadBalancer==: storitev na voljo na porazdeljevalcu obremenitve

==Kubernetes master==: Vozlišče s komponentami za upravljanje gruče:
- kube-apiserver: izpostavlja Kubernetes API, hrani stanje gruče
- kube-controller-manager: izvaja nadzor stanja gruče preko API
- kube-scheduler: iskanje in določanje vozlišč za izvajanje strokov

==Kubernetes node==: Ena/več instanc vozlišč z izvajalnim okoljem:
- kube-proxy: izpostavlja storitve definirane v apiserver-ju - posredovanje TCP/UDP tokov
- kubelet: primarni agent za vzdrževanje strokov na vozlišču glede na specifikacije (yaml)
#### kubectl
- `kubectl create -f conf.yaml` ... ustvari okolje iz konfiguracijske datoteke
- `kubectl get pods` ... prikaži vse stroke
- `kubectl describe pod y` ... prikaži opis stroka
- `kubectl proxy` ... dostop do GUI
<br><br><br><br><br>
### DevOps
==DevOps==: metodologija procesa razvoja - sodelovanje razvojnega in operacijskega dela
- ==verzioniranje izvorne kode== (Git, SVN)
- ==integracija==: zmanjševanje tveganj, hitre povratne informacije
- ==gradnja== (Maven, Jenkins)
    - prevajanje
    - ==izvedba testov== (JUnit)
        - merjenje pokritosti po metodah / vejah izvajanja / vrsticah
        - testiranje enot - metode $\rightarrow$ integracijsko testiranje - povezovanje enot $\rightarrow$ funkcionalno testiranje - na nivoju API-ja $\rightarrow$ sistemsko testiranje - profiliranje obremenitev $\rightarrow$ testi sprejemljivosti - cilji naročnikov
- pregled kode: identifikacija problemov in boljših praks
- namestitev
- priprava dokumentacije