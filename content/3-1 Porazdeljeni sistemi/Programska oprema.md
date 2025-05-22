### Operacijski sistem
Most med strojno opremo in uporabniško programsko opremo:
- upravljanje z viri (procesorji, pomnilnik, V/I naprave, datotečni sistem, ...)
- nadzor delovanja sistema, spremljanje porabe sredstev
### Programski in izvajalni model
==Sočasnost==: več niti v procesu se izvaja v istem časovnem okvirju - časovne rezine
- Programski model: logična organizacija programa (programski vzorec)

==Vzporednost==: več niti se hkrati izvaja na različnih procesorskih jedrih
- Izvajalni model: način izvajanja v ciljnem sistemu (odvisen od sistema)

Sočasnost $\subseteq$ vzporednost
### Proces
==Osnovna enota, ki ji procesor dodeli vire== za izvajanje funkcije main()
Dodeljevanje pomnilnika:
![[Programska oprema-Image-1.png|180]]
### Nit
==Osnovna izvajalna enota==, zmeraj obstaja vsaj ena - glavna nit
==Niti se izvajajo v poljubnem vrstnem redu== (odvisno od razvrščevalnika - OS)
Na niti se procesi izvajajo sinhrono, z več niti ustvarimo več asinhrono delujočih sinhronih tokov
Vrste niti: programske / strojne
Dodeljevanje pomnilnika:
![[Programska oprema-Image-2.png|300]]
Niti se izvajajo v istem naslovnem prostoru $\rightarrow$ enostavna komunikacija med njimi preko statičnih spremenljivk
#### Življenjski cikel niti
![[Programska oprema-Image-3.png|400]]
Pripravljena: čaka v bazenu niti, da ji razvrščevalnik dodeli procesor
Blokirana: OS jo vrne v stanje pripravljenosti, na jedru se začne izvajati druga nit
#### OS razvrščevalnik niti
Razvršča N niti na (N) jeder (običajno želimo N=št. jeder $\rightarrow$ ni potrebnega razvrščanja)
Procesor ima več niti kot jeder, ali pa nit čaka na vire $\rightarrow$ ==preklapljanje med nitmi je cenejše od preklapljanja med procesi== (ni treba shraniti konteksta)
### Naloge
Model abstrakcije - ne delamo neposredno z nitmi
1. Program ustvari niti, ki čakajo v ==bazenu niti==
2. Program ustvarja naloge, ki čakajo v ==bazenu nalog==
3. Ko so niti na voljo, jim razvrščevalnik določi naloge

==Naloge se izvajajo v poljubnem vrstnem redu== (odvisno od razvrščevalnika - OS)
Življenjski cikel naloge je podoben niti
#### Programski razvrščevalnik nalog
Razvršča M nalog na N niti (M > N)
Jedro ima več nalog kot niti, ali pa naloga čaka na vire $\rightarrow$ ==preklapljanje med nalogami je cenejše od preklapljanja med nitmi==