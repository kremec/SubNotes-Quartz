Vhod: AST + atributi
Izhod: vmesna koda za posamezne funkcije

Vmesna predatavitev omogoča delitev prevajanja na:
- sprednji del: leksikalna, sintaksna in semantična analiza (specifično za programski jezik)
- zadnji del: prevajanje in optimizacija strojne kode (specifično za arhitekturo)

Neodvisno od zadnjega dela lahko definiramo vse razen definicij funkcij/metod, ki jih dodamo kasneje glede na podprte ciljne arhitekture

### Zgradba
- prolog (Labela 1): inicializacija sklada, ..., $\rightarrow$ skok na Labelo 2
- prevod funkcije v vmesni kodi (Labela 2) $\rightarrow$ vsak `return` je skok na Labelo 3
- epilog (Labela 3): deinicializacija sklada, priprava vrnitvene vrednosti

Prolog, epilog: zelo odvisna od procesorja $\rightarrow$ pišemo v asm
Vmesna koda: čim manj odvisna od procesorja $\rightarrow$ različne oblike predstavitve:
- 3-adresna koda: `op arg1 arg2` (npr. `ADD $1,$2` ~ `$1=$1+$2`)
- 4-adresna koda: `op arg1 arg2 arg3` (npr. `ADD $1,$2,$3` ~ `$1=$1+$2+$3`)
- drevesna vmesna koda: kasneje potrebna še linearizacija
- skladovna koda: npr. Java bytecode

Praksa: več iteracij vmesnih kod in optimizacij (postopno zmeraj bližje ciljni obliki)

Vmesna koda mora izračunati klicne zapise, ker kasneje ni več koncepta globine funkcij.