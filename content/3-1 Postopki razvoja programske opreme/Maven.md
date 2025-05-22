Pomemben del DevOps razvoja je ==Continuous Integration/Continuous Delivery==: avtomatizacija buildov in inštalacij aplikacij, ustrezna priprava in namestitev:
- preverjanje kode
- upravljanje z odvisnostmi
- izvajanje testov
- priprava dokumentacije

Najpopularnejši: Apache Maven, Gradle, Make, ...
## Maven
Standardizirana projektna struktura z dobrimi praksami (npr. verzioniranje)
### Struktura projekta
- src
    - main
        - java
            - si.fri
        - Resources
    - test
- pom.xml
#### pom.xml
Project Object Model definira metapodatke:
- naziv projekta
- verzijo: `ime_projekta.major.minor.release-SNAPSHOT`
- odvisnosti
- ...
### Življenjski cikli
Default: koraki gradnje in nameščanja
- Faze: validate, initialize, ..., compile, ..., test, ..., install, deploy

Clean: čiščenje rezultatov prejšnjih buildov
- Faze: pre-clean, clean, post-clean

Site: oblikovanje dokumentacije
- Faze: pre-site, site, post-site, site-deploy
<br><br><br><br><br><br>
### Odvisnosti (dependencies)
==Podvajanje odvisnosti==: zasede več prostora, počasen "check-out", težavno sledenje verzijam
==Binarni repozitorij==: ena kopija - shranjena izven projekta, odvisnost definirana v pom.xml
- ==Maven Central== hrani artefakte $\rightarrow$ varnost, hitrost
- Maven iz pom.xml razbere odvisnosti in jih samodejno namesti, verzije se dedujejo
- Določanje ==dosega odvisnosti==: compile, runtime, test, ....
### Vtičniki (plugins)
Spreminjanje in konfiguracija Maven build procesa
### Maven ukazi
`mvn + faza življenjskega cikla + parametri`
- mvn package: preverjanje in prevajanje (JAR)
- mvn test: izvedba (unit) testov
- mvn site: generiranje spletne strani
- mvn deploy: namestitev v skupni Maven repozitorij
- mvn clean deploy -X -P test: čiščenje, namestitev, debug in aktivacija profila test