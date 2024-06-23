### Shannonov kod
1. Znake razvrstimo po padajočih vrednostih
2. Dolžine kodnih besed:  $l_i = \lceil log_r(p_i) \rceil$
3. Kumulativne verjetnosti:  $P_k=\sum_{i=1}^{k-1}p_i$
4. Kodno besedo predstavlja prvih $l_i$ znakov za decimalno vejico $P_k$
![[TIS_Stiskanje_ShannonovKod.png|350]]

Shannon: Več osnovnih znakov združujemo v sestavljene znake, bolj se približujemo entropiji (a imamo zmeraj več znakov - ==kombinaciska eksplozija==)
### Fanojev kod
1. Znake razvrstimo po padajočih vrednostih
2. Znake razvrstimo v $r$ skupin s čim bolj enako vsoto verjetnosti
3. Vsaki skupini dodelimo en znak kodne abecede
4. Postopek ponovimo na vsaki novi skupini, dokler ni v vsaki skupini po 1 znak
![[TIS_Stiskanje_FanojevKod.png|300]]
### Huffmanov kod
Združevanje:
1. Vzamemo $r$ najmanj verjetnih znakov
2. Združimo jih v sestavljeni znak, katerega verjetnost je vsota verjetnosti vzetih znakov
3. Postopek ponovimo, dokler ne ostane 1 znak

Razdruževanje:
1. Sestavljeni znak razstavimo v znake, iz katerih smo ga sestavili
2. Vsakemu priredimo enznak kodne abecede (veje)
3. Postopek ponovimo, dokler imamo sestavljene znake
4. Kodne besede preberemo od korena proti listom drevesa
![[TIS_Stiskanje_HuffmanovKod.png|450]]

==Huffmanovi kodi so podmnožica optimalnih kodov==, dokaz:
- Optimalen kod ne sme imeti neizrabljenih vej
- Najdaljše kodne besede so v $r$-terčkih najmanj verjetnih znakov
- Osnovni kod = $L$ $\rightarrow$ kod z združenima znakoma = $L-1*(p_a+p_b)$
- Pri združevanju dobimo dva sestavljena znaka $L=1$, bolj optimalen kod bi moram imeti manjši $L$ (kar ni mogoče)

Paziti moramo na neizrabljene veje - preveri, ali je dovolj $n$ znakov:
$$
n=r+k(r-1); k\in \mathbb N_0
$$
![[TIS_Stiskanje_HuffmanovKodNeizrabljenost.png|500]]
### Kanonični Huffmanov kod
Enolična določitev Huffmanovega drevesa

1. Zgradimo Huffmanovo drevo
2. Znake razvrstimo najprej po dolžinah kodnih zamenjav naraščajoče, nato po abecedi
3. Prvemu znaku priredimo same ničle
4. Binarna koda naslednjega znaka: <koda prejšnjega znaka> + 1
5. Če je koda naslednjega znaka daljša, na koncu dodamo ničlo
6. Postopek ponovimo za vse zamenjave
![[TIS_Stiskanje_KanoničniHuffmanovKod.png|350]]
### Aritmetični kod
Blizu optimalnemu kodu, hiter, ni težav s kombinacijsko eksplozijo
Ne tako učinkovit kot Huffmanov kod

Vsak niz je predstavljen kot realno število med 0 in 1 - z natančnostjo omogočamo dolžino niza
1. Znakov ni treba razvrstiti
2. Začnemo z intervalom $[0, 1)$
3. Vsaemu znaku kodirne abecede priredimo podinterval, katerega velikost je sorazmerna verjetnosti znakov
4. Izberemo podinterval, ki ustreza iskanemu znaku
5. Postopek ponovimo na izbranem podinteralu
![[TIS_Stiskanje_AritmetičniKod.png|450]]
<br><br>
## Stiskanje na osnovi slovarja
Konstrukcija slovarja na osnovi ponavljajočih se vzorcev - ne uporabljamo (vnaprej znanih) verjetnosti znakov
Kodirnik gradi slovar in zapisuje reference, dekodirnik rekonstruira slovar in znake
### Kod LZ77
Kodirnik:
- preiskuje že poslana besedila, da poišče najdaljši (ponovljeni) niz
- namesto niza pošlje referenco na niz
- uporablja drseče okno z bralnim medpomnilniku in išče podobne nize v iskalnem medpomnilniku
Referenca:
- odmik - razdalja od začetka enakega podniza v pomnilniku
- dolžina enakega podniza
- naslednji znak
![[TIS_Stiskanje_LZ77.png|300]]

![[TIS_Stiskanje_LZ772.png|300]]
### Kod DEFLATE
Predelan LZ:
- $1$ ali $2$ ponovljena osnovna znaka $\rightarrow$ osnovni znak
- $\geq 3$ ponovljeni osnovni znaki $\rightarrow$ par (odmik, dolžina)

Potrebujemo 2 kodni tabeli:
- ==tabela znakov==: $[0, 255]$ - osnovni znaki (dolžine 1), $256$ - konec bloka, $257$ - dolžine 3, ..., $264$ - dolžine 10, ...
- ==tabela odmikov==: 5b enakomerni kod + do 13 dodatnih bitov (do 32000)

Niz znakov se razdeli na bloke, vsak blok se kodira na enega od treh načinov:
- brez stiskanja - osnovni znaki se prepišejo
- statični Huffman (vnaprej podane verjetnosti - hitrejše)
- Huffman (verjetnosti izračunamo - bolj stisnjeno)

Vsak blok ima glavo: 1b za označbo zadnjega bloka, 2b za tip stiskanja, v 3. primeru drevo (uporabimo kanonični Huffman za standardizacijo)
### LZW
Doseže optimalno stiskanje, a rabimo velik slovar

Kodiranje: vnaprej definiran osnovni slovar sproti dopolnjujemo
Dekodiranje: med branjem rekonstruiramo slovar, vendar vedno zaostajamo za eno kodno zamenjavo ()
![[TIS_Stiskanje_LZW.png|550]]
## Verižno kodiranje
Izkorišča ponavljanje podatkov, namesto originalnih podatkov shranjuje dolžino verige
npr. `aaaabbc` $\rightarrow$ `4a2b1c`
### BMP
- 1b za: 0 - verižno kodiranje / 1 - brez kodiranja
- št. znakov
- znak

Primer:  `05a 04d 13edf` $\rightarrow$ `aaaaaddddedf`
## Stiskanje z izgubami
Učinkovito pri slikah in zvoku - upoštevanje nepopolnosti človeških čutil
==Kompresijsko razmerje==:
$$
R=\frac{stisnjen \ binarni \ zapis}{binarni \ zapis}
$$
### JPEG
Shema: $Y \ C_r \ C_b$ - svetlost in dve barvi, svetlost je pomembnejša
1. Aprokcimacija vsake komponente z **DCT**
2. Odrežemo nepomembne koeficiente (informacije)
3. Predikcija na podlagi sosednjih točk z RLE
4. S Huffmanom zakodiramo nove koeficiente
### MP3
1. DCT
2. Odstranimo za človeka neslišne frekvence
3. Odstranitev šibkih zvokov med glasnimi
4. Če sta L in R podobna, se pošilja Mono
5. S Huffmanom zakodiramo nove koeficiente
### MPEG
Tipi okvirjev:
- ==I - cela slika==: JPEG
- ==P - prediktivno kodiranje==: poslane so spremembe in vektor premika (če ni veliko sprememb)
- ==B - interpolacija==: kodiranje iz predhodnjega in nasldnjega okvirja
- ==D==: močno stisnjen I