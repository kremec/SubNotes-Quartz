## JDBC
==Open Database Connectivity (ODBC)==: standardni API protokol za dostop do DBMS
==Java Database Connectivity (JDBC)==: javanska knjižnica za vzpostavljanje povezave na bazo, izvajanje SQL povpraševanj in strukturo rezultatov povpraševanj
### Sestava
JDBC API: javanski API
JDBC Driver Manager: komunikacija s produktno-specifičnimi gonolniki za komunikacijo z DB
- ==Tip 1 - JDBC-ODBC most==: pretvorba JDBC v ODBC klice
- ==Tip2 - delni javanski gonilnik==: JDBC klici direktno na specifičen gonilnik DB
- ==Tip 3 - javanski/mrežni gonilnik==: vmesni sloj pretvori ukaze
- ==Tip 4 - čisti javanski gonilnik==: direktna komunikacija z DB
### Uporaba
1. Nalaganje ustreznega gonilnika + sestavljanje URL za povezavo na DB
   `jdbc:vendorName://host:port/databaseName`
2. Vzpostavitev povezave: URL, username, password
3. Kreiranje objekta:
    - Statement: string brez parametrov
    - PreparedStatement: string s parametri (`?` $\rightarrow$ setString/setInt(indeks, velikost)) - boljša zmogljivost in preprečitev SQL injection-a
    - CallableStatement: klic shranjenih procedur
4. Izvršitev SQL povpraševanj / shranjenih procedur + obdelava rezultatov:
    - `SELECT` $\rightarrow$ `ResultSet`
    - `INSERT`/`UPDATE`/`DELETE` $\rightarrow$ `int` (št. obdelanih vrstic)
    - `CREATE`/`DROP` $\rightarrow$ `boolean`
5. Zapiranje povezave
#### Transakcije
Privzeto se SQL ukazi samodejno potrdijo (`autoCommit`)
Transakcijsko izvajanje: `autocommit=false` $\rightarrow$  ... $\rightarrow$ `commit()`/`rollback()`
### Connection pooling
==Bazen povezav==: predpomnilnik povezav na DB
Vzpostavljanje in prekinjanje povezav počasno, povezave lahko uporabimo večkrat
- zmanjšano št. hkratnih povezav (namesto za vsako aplikacijo svoja povezava)
- izognemo se ročnemu zapiranu povezav
- lažji razvoj in nameščanje
### Vzorec DAO
Ločitev nizkonivojskih operacij dostopa do podatkov in visokonivojske poslovne logike - vmesnik
Uporaba objektov za prenos podatkov (Data Transfer Object)
## ORM
==Object Relational Mapping==: tehnika premoščanja razkoraka med objektnim in relacijskim modelom
- avtomatska preslikava objekti $\leftrightarrow$ relacijske tabele
- ni pisanja SQL stavkov, lažje upravljanje transakcij
- lažja konfiguracija in logiranje
### JPA
Javansko ogrodje za upravljanje relacijskih podatkov brez pisanja SQL stavkov:
- API - povpraševalni jezik za CRUD operacije
- deklarativen način izvedbe preslikave
#### Anotacije
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
#### Osnovne operacije nad entitetami
Kreiranje - `persist()`: če obstaja proži napako
Brisanje - `remove()`: sinhronizacija ob `flush()`
Posodabljanje - `merge()`: sinhronizacija ob `flush()`, razveljavitev lokalnih sprememb ob `refresh()`
Povpraševanje:
- `find(entitetni razred, primarni ključ)`: če ne najde vrne null
- `getReference(entitetni razred, primarni ključ)`: če ne najde proži napako
#### JPQL
Jezik povpraševanja po entitetah, ki kombinira sintakso SQL z izraznostjo OOP
- statična povpraševanja - `createNamedQuery("...")`: definiramo v anotacijah / XML
- dinamična povpraševanja - `createQuery("...")`: če ne poznamo scenarija povpraševanja vnaprej
Število rezultatov: `getSingleResult()` / `getResultList()`
Uporaba parametrov kot pri PreparedStatementih (zaporedna številka / po imenu)
Ostranjevanje rezultatov: `setMaxResults()` / `setFirstPosition()`