==Anonimna cev (pipe)==: posredni sinhroni način enosmerne komunikacije z medpomnenjem
`int pipe(int fd[2])` ustvari in odpre cev z:
- bralnim koncem `fd[0]`$\rightarrow$ `read(fd[0])`
- pisalnim koncem `fd[1]`$\rightarrow$ `write(fd[1])`
![[OS_MedprocesnaKomunikacijaAPI_Cev.png|300]]

Komunikacija preko cevi je omejena na procese z istim potomcem (tipično starš - otroci)

==Cevovod (pipeline)==: zaporedna uporaba cevi s strani otrok istega starša
V lupini: zaporedje ukazov, ločenih z `|` - lupina poskrbi za cevi, otroke, preusmeritve, ...
![[OS_MedprocesnaKomunikacijaAPI_Cevovod1.png|350]]
![[OS_MedprocesnaKomunikacijaAPI_Cevovod2.png|500]]

==Imenovana cev (named pipe / fifo)==: poseben tip datoteke (pipe) z imenom (imeniški vnos), ki se jo lahko naslavlja in preko nje neomejeno komunicira
`mkfifo <cev>` ustvari imenovano cev

==Sporočilna vrsta (mesage queue)==: posredni asihroni način komunikacije - hramba sporočil v vrsti
Sporočila so lahko različno dolga, vsako ima identifikator vrste

==Segment (deljeni kos pomnilnika)==: z vidika procesa sklenjen kos okvirjev strani
- ==sistemsko pogojen==: OS omejuje št. segmentov in skupno velikost deljenega pomnilnika

Potek komunikacije: ustvarjanje - priklopi in odklopi segmentov - sprostitev

### Vtičnice
Posredna dvosmerna medprocesna in mrežna komunikacija (tipično odjemalec - strežnik)
- Strežnik vzpostavi vtičnico na znanem naslovu in čaka na zahteve odjemalcev
- Odjemalec se poveže na vtičnico $\rightarrow$ izmenjava sporočil
![[OS_MedprocesnaKomunikacijaAPI_Vtičnice.png|250]]

Vrste vtičnic:
- ==AF_LOCAL==: lokalna vtičnica (naslavljanje preko datoptek brez posebnih protokolov)
- ==AF_INET==: internetni protokol v4 (TCP, UDP, IP, ICMP, ...)
- ==AF_INET6==: internetni protokol v6