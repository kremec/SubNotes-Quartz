### Specializirane vrste zbirnikov
- modularni: omogoča pisanje programa v modulih namesto eni sami datoteki
- mikro: zbiranje na še nižji nivo - mikroprocesorske ukaze
- makro: omogoča uporabo makrojev
- meta: podamo opis računalnika, za katerega naj zbira
- prečni: omogoča zbiranje za druge arhitekture, kakor na kateri teče
- "naloži in izvedi": hkratno prevajanje neposredno v pomnilnik in izvajanje
### Tabele
#### Ukazna tabela
Vsebuje sezname:
- mnemonik : operacijska koda : tip ukaza : št. operandov
- register : št. registra
- psevdoukaz
#### Simbolna tabela
- Levi naslov
- vrednost (LŠ / vrednost)
- (PROGRAMSKI BLOKI - blok)
- (VNAPREJŠNJE REFERENCE V EQU - odvisnost, odvisniki)
#### Tabela blokov
- ime
- naslov
- dolžina
#### Tabela literalov
- ime
- tip
- naslov
- dolžina
#### Tabela razdelitev pomnilnika (CSTAB)
- ime
- naslov
- dolžina
#### Tabela zunanjih simbolov (ESTAB)
- ime sekcije
- ime simbola
- vrednost - naslov znotraj sekcije
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
### SIC objektna datoteka
#### Zaglavje (Header - H)
- (1) H
- (2-7) ime programa
- (8-13) začetni naslov
- (14-19) dolžina programa $\rightarrow$ LŠ + dolžina ukaza END
#### Programski zapis (Text - T)
- (1) T
- (2-7) začetni naslov T zapisa
- (8-9) dolžina T zapisa $\rightarrow$ max 30 = 0x1E bajtov
- (10-69) objektne kode 3B ukazov $\rightarrow$ max 10 ukazov
#### Zapis za konec (End - E)
- (1) E
- (2-7) naslov prvega izvršljivega ukaza
#### Prilagoditveni zapis (M-Modification)
- (1) M
- (2-7) relativna lokacija ukaza
- (8-9) dolžina naslovnega polja (ponavadi `03`/`05` - katere pol-byte popraviti)
#### Definicijski zapisi (D - Definition)
- (1) D
- (2-7) ime zunanjega simbola
- (8-13) relativni naslov zunanjega
- (14-73) informacije o ostalih simbolih - ponavljanje 2-13
#### Referenčni zapis (R - Reference)
- (1) R
- (2-7) ime zunanjega simbola
- (8-73) informacije o ostalih simbolih - ponavljanje (2-7)
#### Prilagoditveni zapis (M - Modification)
- (1) M
- (2-7) začetni naslov polja v kodi
- (8-9) dolžina polja
- (10) smer popravka - + ali -
- (11-16) ime zunanjega simbola, katerega vrednost je treba prišteti/odšteti