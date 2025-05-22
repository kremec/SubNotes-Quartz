### Arhitektura aplikacij in mikrostoritve
![[Osnove arhitekture aplikacij-Image-1.png|300]]

| **Odjemalski model**                                                                                                                                     | **Strežniški model**                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| - procesiranje v brskalniku odjemalca<br>- komunikacija s strežnikom preko REST<br>- strežnik ne vzdržuje uporabniške seje<br>- obremenitev na odjemalcu | - procesiranje na strežniku<br>- odjemalec samo procesira izgled<br>- strežnik vzdržuje uporabniško sejo<br>- obremenitev na strežniku |
==Monolit==: združene funkcije poslovne logike $\rightarrow$ nepotrebno skaliranje manj nujnih storitev
==Mikrostoritve==: razbitje na zaključene funkcionalne dele $\rightarrow$ modularnost, horizontalna skalabilnost
### Oblak
Hierarhija oblaka:
- ==Cloud==: podatkovni centri
- ==Fog==: mreža nodov (npr. CDN)
- ==Edge==: naprave

Statične vsebine streže ==Content Delivery Network== - zrcaljenje vsebine preko lokalnih nodov po svetu
==IaaS== - virtualke, networking in shramba / ==PaaS== - managed IaaS s prijavami, messeging in logiranjem
### REST API
==HTTP metode==: `GET`, `HEAD`, `POST`, `PUT`, `PATCH`, `DELETE`
- `@Get`,`@Post`, ...
==MIME formati==: `application/json` / ... $\rightarrow$ `Content-Type:` / `Accept:` - zaglavje
- `@Consumes(MediaType.APPLICATION_JSON)`, `@Produces(MediaType.APPLICATION_JSON)`
==URL pot virov==: gnezdenje max 3 nivoje; ostanjevanje $\rightarrow$ `?offset=?&filter=?` + `X-Total-Count:`; sortiranje in filtriranje $\rightarrow$ `?order=?&where=?`
- `@ApplicationPath("/v1")`- verzija, `@Path("samostalniki")`- množina
==HTTP kode==:
- `200 OK`, `201 Created`, `204 No Content`, `304 Not Modified` (imaš aktualno instanco)
- `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `500 Internal Server Error`
### Maven
Standardizacija in avtomatizacija: gradnja, testiranje in nameščanje; čiščenje; dokumentacija
==pom.xml==:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <groupId>SI.FRI.PRPO.PROJEKT</groupid>
    <artifactId>projektA</artifactId>
    <packaging>JAR/WAR/EAR/RAR</packaging>
    <version>[MAJOR].[MINOR].[RELEASE]-SNAPSHOT</version>
    
    <dependencies>
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>4.8.1</version>
            <scope>COMPILE/RUNTIME/TEST</scope>
        </dependency>
    </dependencies>
    
    <modules>
        <module>projektB</module>
        <module>projektC</module>
    </modules>
</project>
```
Ukazi:
- `mvn package`: preverjanje in prevajanje $\rightarrow$ .JAR
- `mvn test`: izvedba testov enot
- `mvn clean deploy -X -P test`: čiščenje, namestitev, debug, aktivacija profila test
- `mvn site`: generiranje spletne strani

</br></br>
### Context and Dependency Injection
Avtomatsko zagotavljanje odvisnosti objektom:
- določanje ==življenjskega cikla== in interakcij komponent
- vstavljanje ==referenc odvisnosti== komponent

Shranjevanje stanja klientov: v storitvi $\rightarrow$ stateful / v bazi $\rightarrow$ stateless (skalabilnost, varnost podatkov)

==Prestrezniki==: proženje metod ob dogodkih CDI zrn
- `@PostConstruct`: tik po inicializaciji
- `@PreDestroy`: tik pred uničenjem

==Doseg CDI zrn==:
- `@RequestScoped`: nova instanca razreda z vsakim zahtevkom
- `@SessionScoped`: nova instanca razreda za vsako sejo
- `@ApplicationScoped`: ena instanca v celem življenjskem ciklu aplikacije
- `@Singleton`: deljeno stanje ene instance 
- `@Dependant`: prevzame doseg klicatelja

==Transakcije==: izvedemo v celoti ("commit") / prekličemo in povrnemo začetno stanje ("rollback")
- `@Transactional(value="mandatory")`$\rightarrow$ klic izven transakcije proži izjemo
- `@Transactional(value="never")`$\rightarrow$ izvajanje izven transakcije
- `@Transactional(value="required")`$\rightarrow$ klic izven transakcije ustvari novo
- `@Transactional(value="required_new")`$\rightarrow$ zmeraj ustvari novo transakcijo (gnezdenje)