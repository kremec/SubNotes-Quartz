### Zgodovina
- C: fokus na izkoriščanju malo virov; slabša sintaksa in kompleksnost
- C++, C# in Java: večnitno programiranje in čiščenje pomnilnika
- Python in Javascript: skupnost in veliko paketov; ni prevajan $\rightarrow$ manjša zmogljivost
- Go:
    - prevajan $\rightarrow$ zmogljiv
    - vgrajena podpora vzporedenja
    - statična tipizacija z izpeljavo tipov
    - errors-as-values
    - vzporedno delujoč garbage collection
    - ni objekten, a podpira vmesnike
    - večplatformen
### Sočasnost
Model Communicating Sequential Processes oz. model ==opravilo-kanal==:
- ==gorutine== (=[[3-1 Porazdeljeni sistemi/Programska oprema#Naloge|naloge]]): enostavne neodvisne sekvenčne funkcije z vhodom in izhodom,ki jih lahko izvajamo sočasno
- ==kanali==: komunikacija in/ali sinhronizacija gorutin; blokirajoči - gorutine čakajo na sporočilo
#### Gorutine
Vedno vsaj ==glavna gorutina==, ki se zažene ob začetku izvajanja programa
Model ==razcepi-pridruži== (fork-join):
![[Go-Image-1.png|500]]
#### Kanali
Enosmerni (samo branje ali samo pisanje) / dvosmerni (oboje)
==Blokirajoči==:
- pisanje v poln kanal $\rightarrow$ čakanje na izpraznenje kanala
- branje iz praznega kanala $\rightarrow$ čakanje na vrednost v kanalu

Velikost kanala:
- privzeta velikost kanala 0 $\rightarrow$ pisalna gorutina čaka, da je bralna gorutina pripravljena na sprejem
- kanali z medpomnilnikom (velikost > 0) $\rightarrow$ branje iz kanala po FIFO principu

Zapiranje kanalov: branje iz zaprtega kanala mogoče, `ok` zastavica postavljena na `false`
Sinhronizacija s kanali: s tipom kanala `struct{}` poudarimo, da se ne bo prenašalo vrednosti