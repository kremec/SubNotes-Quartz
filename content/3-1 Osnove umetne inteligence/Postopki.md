# Strojno učenje
### Gradnja dreves
**Zgradi odločitveno drevo za napovedovanje ciljne spremenljivke, izbira najboljšega atributa z (razmerjem) informacijskega prispevka:**
1. (Binarizacija atributov)
2. I
3. Za vsak atribut Gain, Ires (in GainRatio, I)
4. Deliš po najvišjem Gainu
5. Ponavljaš rekurzivno

**Zgradi regresijsko drevo:**
1. Za vsak zvezen atribut poskusi vse delitve, za vsak zvezni atribut 1 delitev
2. Za vsako delitev izračunaj MSE in Ires(A)
3. Od vseh izberemo tisto delitev z najmanjšim Ires
4. Ponavljaš rekurzivno
### Ovrednotenje dreves/primerov
**Ovrednoti kvaliteto drevesa s testno množico:**
1. Vse primere spusti po drevesu, štej TP, TN, FP, FN
2. Računaš po formulah

**Ovrednoti klasifikacijsko točnost z x-kratnim prečnim / leave-one-out preverjanjem:**
1. Za vsako testno skupino / vsak primer naredi drevo (iz ostalih skupin)
2. Za vsako drevo se s testnimi primeri spusti po drevesu, štej TP, TN, FP, FN
3. Računaš po formulah

**Oceni kvaliteto napovedi k-NN z x-kratnim prečnim / leave-one-out preverjanjem:**
1. (Normalizacija atributov)
2. Medsebojne razdalje med primeri (tabela)
3. Za vsak primer vzemi k najbližjih sosedov (ne iz istega bloka)
4. Napoved bo povprečje njihovih vrednosti, kvadratna napaka (vrednost-napoved)^2, kvadratne napake znotraj skupin povprečiš
5. Izračunaj MSE_CV / MSE_LOO = (vsota povprečnih kvadratnih napak skupin oz. primerov) / št. primerov
### Rezanje dreves
**Odločitveno drevo reži z REP (, rezalna množica):**
1. (Vse primere spusti po drevesu) - šteješ \[#pravilnih, \#napačnih] klasifikacij
2. Od vključno staršev listov drevesa navzgor - št. napačnih v listih poddrevesa $\geq$ št. napačnih v vozlišču -> reži

**Odločitveno drevo reži z MEP,  _ ocena verjetnosti:**
1. Od listov navzgor, računaš statične in vzvratne napake - upoštevaj oceno verjetnosti
2. Pri staršu statična $\lt$ vzvratna -> reži
### Naivni Bayes
**Klasificiraj primer z naivnim Bayesom, _ ocena verjetnosti:**
1. Za vse vrednosti ciljnega razreda: h(ciljni/atributi primerov) npr. DA, NE ali A, B, C
2. Višji h normaliziraj v verjetnost
### Nomogram
**Naredi nomogram po naivnem Bayesu za ciljni razred, _ ocena verjetnosti, _ logaritem:**
1. Za vsak atribut izračunaj za vse možne vrednosti atributa točke(Ciljni razred/vrednost)
2. Nariši
### kNN in regresija
**Klasificiraj primer z k-NN, _ razdalja:**
1. (Normalizacija vrednosti - isti max, min na učnih in testnih podatkih)
2. Za vse primere izračunaj razdaljo do iskanega primera
3. Vzemi jih k najbližjih - klasificiraj kot njihov večinski razred

**Lokalna utežena regresija, utež, _razdalja:**
1. (Normalizacija vrednosti - isti max, min na učnih in testnih podatkih)
2. Za vse primere izračunaj razdaljo do iskanega primera, iz nje pa utež po dani formuli
3. Izračunaj uteženo vsoto - napoved
### Razvrščanje
**Gručenje s k-voditelji (k-means), _ razdalja, začetni primeri:**
1. Centroidi gruč: povprečja atributov
2. Razdalje primerov do centroidov + prerazporedi
3. Ponavljaj dokler se ne ustalijo

**Dendrogram, hierarhično gručenje, _ razdalja, _ povezanost:**
1. (Normalizacija atributov)
2. Medsebojne razdalje med primeri (tabela)
3. Primera z najmanjšo medsebojno razdaljo poveži - povezanost upoštevaj pri računanju novih vrednosti
4. Ponavljaj, dokler nimaš 1 skupine
# Preiskovanje
Tabela: (meja), razvita, generirana, vrsta
### Neinformirani preiskovalni algoritmi
**BFS**: razvij najbolj plitvo nerazvito vozlišče $\rightarrow$ FIFO vrsta razvijanja, končamo ob razvitju konca
**DFS**: razvij najglobje nerazvito vozlišče $\rightarrow$ LIFO sklad, končamo ob razvitju konca
**Iterativno poglabljanje**: DFS po iteracijah globine, končamo ob razvitju konca
**Dvosmerno iskanje**: vzporedna BFS iz vsake strani, končamo ob sklenitvi poti
**Cenovno-optimalno iskanje**: BFS, razvij vozlišče z najmanjšo dosedanjo skupno ceno poti $\rightarrow$ fronta v prioritetni vrsti, končamo ob generaciji konca
### Informirani preiskovalni algoritmi
$f(n)$ ... cenilna funkcija, $h(n)$ ... hevristika, $g(n)$ ... znana cena poti
**Požrešno iskanje**: $f(n)=h(n)$
**A\***: $f(n)=g(n)+h(n)$
**IDA\***: iterativno poglabljanje dokler je $f(n)\leq meja$
### Lokalno preiskovanje
**Plezanje na hrib**:
1. (Naključna začetna rešitev)
2. Generiramo sosednje rešitve (vse možne postavitve ob zamenjavi 2 elementov)
3. Izberemo najbolje ocenjeno
4. Ponavljamo dokler niso vse sosednje rešitve slabše od trenutne

**Simulirano ohlajanje**:
1. (Naključna začetna rešitev)
2. Naključno izberemo sosednjo rešitev
3. $e^{\frac{\Delta E}{t}} > naključno\ generirano\ število\ med\ 0\ in\ 1$ $\rightarrow$ vzemi novo, sicer ohrani staro
4. Zmanjšaj temperaturo $t$
5. Ponavljaj dokler $t>0$

**Lokalno preiskovanje v snopu**:
1. Hranimo k aktualnih stanj, izbiramo k optimalnih sosedov
2. Ocenjujemo kakovost cele generacije
### Preiskovanje stanj
**MINIMAX**:
3. Izriši drevo vseh potez
4. Ovrednoti končna stanja (liste)
5. Ovrednoti stanja navzgor glede na to, kdo je na vrsti - MIN bo vzel najmanjšo oceno od otrok, MAX največjo

**Alfa-beta rezanje**:
6. Začetno vozlišče: $[\alpha,\beta]=[-\infty,\infty]$
7. Na vsakem koraku prenašamo $[\alpha,\beta]$ v globino
8. Ob vračanju posodabljamo $[\alpha,\beta]$ glede na najdene vrednosti
    - MAX posodablja le $\alpha$ (najvišji že najdeni maksimum)
    - MIN posodablja le $\beta$ (najnižji že najdeni minimum)il67ujkjk8zhji
9. V nekem vozlišču $\alpha\geq\beta$ $\rightarrow$ prekinemo preiskovanje ostalih poddreves
### Prostor stanj
**Nariši prostor verjetnih stanj in prehodov, najdi pot do cilja z _ preiskovalnim algoritmom**
### Regresiranje ciljev
**Preiskovanje iz začetnega do ciljnega stanja z _ preiskovalnim algoritmom, definicije akcij ki jih vzemamo v _ vrstnem redu**:
10. Stanje: \[...\]
11. Cilji: \[...\], vzamemo prvega ki še ni narejen (če so vsi narejeni končamo)
12. Najdemo akcijo ki vzpostavi ta cilj, v akciji imamo lahko spremenljivke
13. Za vse možne vrednosti spremenljivke zpišemo tabelo možnosti akcij in predpogojev
14. Tabelo uredimo po št. neizpolnjenih predpogojev
15. V plan dodamo prvo akcijo kjer $cilji\cap del=0$, $regresirani\ cilji=cilji\cup predpogoji(A) - add(A)$
16. Ponavljamo dokler ne dosežemo ciljev začetnega stanja ali omejitve dolžine plana, v slednjem primeru se vrnemo in poskusimo naslednjo možnost
### Razporejanje opravil
**Razporejanje opravil**:
1. Nariši graf z vejitvijo
2. Od začetka proti koncu vozliščem določi ES
3. Od konca proti začetku vozliščem določi LS
4. Vsem vozliščem določi rezervo

**Upoštevanje resursov**:
1. Graf, ES, LS in rezerve
2. Na vsaki iteraciji dodeli najbolj zgodnji možen začetek akciji z najmanjšo časovno rezervo in izpolnjeni predhodniki
3. Ponavljaj dokler ne obdelaš vseh vozlišč
# Bayesovske mreže
**Poišči množice vozlišč, ki d-ločujejo pare vozlišč**:
1. Poišči vse preproste poti med parom vozlišč
2. Za vsako vozlišče na poti najdi množico $E$, ki d-ločuje
3. Množice $E$ za vozlišča nato združi v unijo
4. Ponovi za vse poti
5. Množice $E$ za poti združi s presekom

**Poenostavi pogojni del v izrazu**:
1. Za vse pare $x$-$a$ gledaš, da mora biti množica ostalih danih pogojnih vozlišč v $E$
    Če sta $x$ in $a$ po definiciji pogojno odvisna (povezana), $a$ ne moremo dati ven
2. $a$ lahko damo ven ($x$ je neodvisen od $a$), če je množica ostalih danih pogojnih vozlišč element $E$

**Ali sta vozlišči pogojno neodvisni pri danih znanih vozliščih**:
1. Dana znana vozlišča (če jih ni mora biti prazna množica) morajo biti v $E$
2. Da/ne, utemeljitev iz grafa

**Ali velja $P(x/y,z,w)=P(x/y)$**:
1. 2 možnosti
    - Za vse pare $x$-$a$ gledaš, da morajo biti ostala dana pogojna vozlišča v $E$
    - Vse poti med $x$ in $z$ morajo biti zaprte, poznamo $y$
2. Da/ne, utemeljitev iz grafa - če da je $x$ pogojno odvisen od $a$, zato $a$ ne moremo odstraniti