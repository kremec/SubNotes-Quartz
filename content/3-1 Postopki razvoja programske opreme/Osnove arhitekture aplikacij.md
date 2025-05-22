### Faze razvoja
- Raziskovanje
- Razvoj
- Vzdrževanje: najdaljša faza - od zasnove arhitekture odvisna življenjska doba
### Zgodovina
- Monolitska
- Dvonivojska (UI + logika / DB)
- Tronivojska (UI / logika / DB)
- Service Oriented Architecture - vpeljani API
- Microservices in Cloud-native solutions
### Principi
- ==Konsolidacija poslovne logike== = DRY: ista koda v vseh delih IS, isti podatkovni tipi
  Nasprotje: silosna zasnova s podvajanjem kode
- ==Modularnost==: zmanjšanje odvisnosti in prekrivanja funkcionalnosti
  Nasprotje: kompleksen tesno sklopljen sistem z veliko odvisnostmi
- ==Odgovornost za le 1 komponento== brez znanja o podrobnostih drugih komponent
### Sestava
![[Osnove arhitekture aplikacij-Image-1.png|300]]
#### Uporabniški vmesniki
Tekstovni / grafični / zvočni
Načini delovanja:
- ==Native UI==: namestimo na napravo
- ==Web UI==: izvaja se v brskalniku (HTML5, JavaScript, Responsive Web Design, Single Page Application, Progressive Web Application)

| **Odjemalski model**                                                                                                                                     | **Strežniški model**                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| - procesiranje v brskalniku odjemalca<br>- komunikacija s strežnikom preko REST<br>- strežnik ne vzdržuje uporabniške seje<br>- obremenitev na odjemalcu | - procesiranje na strežniku<br>- odjemalec samo procesira izgled<br>- strežnik vzdržuje uporabniško sejo<br>- obremenitev na strežniku |
<br><br><br><br><br><br>
#### Spletni strežniki
Zgodovina izvajanja poslovne logike:
- CGI: shell skripta, kar je dala na stdout se je vrinilo v HTML na določeno mesto
- PHP, JSP, ASP.NET: nadgrajeni CGI
- dandanes strežnik pošlje kodo za izvajanje v brskalniku
Statične vsebine streže ==Content Delivery Network== - zrcaljenje vsebine preko lokalnih nodov po celem svetu
### Cloud computing
Ponudniki: AWS (Amazon), Azure (Microsoft), GCP (Google)
Prednosti: izognemo se začetni investiciji v hardware, skalabilnost
Hierarhija:
- Cloud: podatkovni centri
- Fog: mreža nodov (npr. CDN)
- Edge: naprave
#### Infrastructure as a Service
- Virtualke
- networking (npr. VPN, mreže)
- shramba (npr. bucket storage, DB)
#### Platform as a Service
Managed IaaS storitev
- prijave (npr. OAuth)
- messeging
- logging
### Skalabilnost
- ==Vertikalna==: boljši strežnik, se hitro ustavi zaradi omejitev (npr. hitrost procesorja)
- ==Horizontalna==: več instanc strežnikov - razpoložljivost 24/7