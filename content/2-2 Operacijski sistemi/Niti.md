Glavni nalogi procesov - lastništvo virov in izvajanje kode - sta neodvisni
$\rightarrow$ procesi naj skrbijo za lastništvo virov, niti pa za izvajanje kode

Enonitnost vs. večnitnost:
![[OS_Niti_EnonitnostVečnitnost.png|500]]

Nit:
- skrbi za ==izvajanje kode==
- ima svoj ==izvajalni kontekst== (stanje, registri in sklad)
- pripada procesu - vse niti imajo ==isti naslovni prostor (procesa)==

==Deskriptor niti==: podatkovna struktura, ki hrani izvajalni kontekst niti

Prednosti večnitnosti: hitrejše - ni inicializacije in preklopa naslovnega prostora in praznenja TLB, hitrejša komunikacija, izkoriščenost procesorja in virov, specializacija in modularnost večnitnega dela

Izvedba na ==jedrnem nivoju==:
- podpora preko sistemskih klicev
- razvrščevalnik razvršča niti
- izkoričajo lahko več procesorjev
- OS skrbi za morebitno sinhronizacijo

Izvedba na ==uporabniškem nivoju==: OS se teh niti ne zaveda - če blokira 1 nit blokira vse
- podpora preko knjižnice za nitenje
- razvrščanje je prilagojeno aplikaciji
- tečejo lahko v kateremkoli OS