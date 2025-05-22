## Contexts and Dependency Injection
CDI: avtomatsko zagotavljanje odvisnosti objektom (namesto ročnega ustvarjanja)
- Kontekst: določa življenjske cikle in interakcije komponent
- Vstavljanje odvisnosti: vstavljanje referenc na posamezne komponente znotraj aplikacije

CDI zrno: razred, ki ga instancira, uporablja in vstavlja CDI vsebnik
- anotiramo z dosegom in pridobivanje z anotacijo `@Inject`
### Doseg (scope) CDI zrn
- ==Doseg zahtevka== (request scoped): nova instanca ob vsakem zahtevku
- ==Doseg seje== (session scoped): nova instanca za vsako sejo
- ==Doseg aplikacije== (application scoped): ena instanca v celem življenjskem ciklu
- ==Pogojen doseg== (dependant): odvisno od klicatelja (npr. znotraj storitve isto zrno lahko kličeta app in session scoped zrni)
#### Stateless/stateful
Shranjevanje konteksta/stanja klientov (v programskih objektih):
- v storitvi $\rightarrow$ stateful
- v bazi $\rightarrow$ stateless

Stateless stortve:
- lažja horizontalna skalabilnost - load balancerji lahko katerokoli zahtevo pošljejo na katerokoli instanco
- večja varnost podatkov - če je kontekst shranjen lokalno in instanca pade so podatki izgubljeni
### Prestrezniki (interceptors)
Definicije metod, ki se prožijo ob določenih dogodkih CDI zrn (npr. inicializacija, klici metod, ....)
Implementacija z lastnimi anotacijami in metodami, ki se nanje povežejo
Tipi prestreznikov:
- ==Business Method interceptor==: klici metod zrna s strani odjemalcev zrna
- ==Lifecycle callback interceptor interceptor==: povratni klici v življenjskem ciklu s strani vsebnika
- ==Timeout method interceptor==: klici EJB timeout metod s strani vsebnika
#### Povratni (callback) klici
Ni zagotovila, da se konstruktor razreda proži $\rightarrow$ anotacija metod v razredu:
- `@PostConstruct`: tik po instanciranju
- `@PreDestroy`: tik pred uničenjem
<br><br><br><br><br><br>
### JTA in transakcije
Transakcija: zaporedje ukazov
- bodisi izvedemo v celoti (commit)
- bodisi prekličemo in povrnemo začetno stanje (rollback)
Java Transaction API: deklarativno upravljanje transakcij v CDI zrnih z anotacijo metod `@Transactional`
Tipi transakcijskega konteksta:
- ==MANDATORY==: klic metode izven transakcijskega konteksta $\rightarrow$ proženje izjeme
- ==NEVER==: klic metode izven transakcijskega konteksta $\rightarrow$ izvajanje izven transakcijskega konteksta
- ==REQUIRED==: klic metode izven transakcijskega konteksta $\rightarrow$ odpremo novo transakcijski kontekst za izvajanje
- ==REQUIRED_NEW==: vedno odpremo nov transakcijski kontekst za izvajanje