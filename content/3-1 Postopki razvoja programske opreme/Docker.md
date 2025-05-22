Vsebniška virtualizacija:
- neodvisnost od platform in programskih jezikov
- varnostno izolirano izvajanje
- optimalna izraba strojne opreme
- enostavno deljenje Docker slik
## Arhitektura
==Docker server/deamon==: izvaja gradnjo, izvajanje in distribucijo Docker vsebnikov
==Docker client==: komunicira z deamonom
Tečeta lahko na istem ali ločenem sistemu
Komunikacija poteka preko REST API-ja:
![[Docker-Image-1.png|400]]
## Vsebnik
### Docker slike
READ-ONLY predloge vsebnika
Nivoji:
- READ-ONLY: osnovna slika, uporabniške datoteke - aplikacija in odvisnosti
- READ_WRITE: izvajanje aplikacij

Nivoji se združijo v skladen datotečni sistem
Spremembe zahtevajo ponovno gradnjo le tega nivoja $\rightarrow$ prenos le nivojev, ki so bili dodani/spremenjeni
### Zagon vsebnika
1. Prenos slike: preveri lokalno verzijo, ni najnovejša $\rightarrow$ prenos iz repozitorija
2. Ustvari vsebnik na podlagi slike
3. Alocira READ datotečni sistem + priklopi READ-WRITE nivo
4. Alocira omrežni vmesnik + dodeli IP naslov
5. Zažene specificiran proces
6. Zajema izhod aplikacije
## Dockerfile
Format: `INSTRUCTION arguments`
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
## Docker Compose
Zagon aplikacij z več vmesniki
Definicije odvisnosti (npr. DB mora biti dostopna pred zagonom aplikacije)
  