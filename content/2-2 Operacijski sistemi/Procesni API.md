### Windows
Stvaritev procesa:
```
CreateProcess(
  ime programa,
  ukazna vrstica,
  atributi procesa, atributi niti,
  dedovanje ročajev,
  zastavice, okolje
  trenutni imenik,
  zagonske informacije, procesne informacije
)
```
Končanje procesa:
`ExitProcess(status)`
`TerminateProcess(process, status)`
`GetExitCodeProcess(process, status)`

Čakanje procesa:
`WaitForSingleObject(hadle, miliseconds)`
### UNIX-like sistemi
Info o procesu:
`int getpid()`, `int getppid()`, `int getuid()`, `int getgid()`, `int geteuid()`, `int getegid()`

Ostalo:
`int sleep(uint seconds)`
`clock_t times(struct tms *buf)` ... vrne izvajalne čase procesa

Ustvaritev procesa - fork:
==Starš ustvari kopijo sebe (procesa) - otroka==: nov deskriptor procesa (razen PID in PPID isto) in enak naslovni prostor (kopija sklada in kopice)
`int fork()` ... naredi dva procesa, starš vrne PID otroka, otrok vrne `0`
```c
int pid = fork();
if (pid > 0)       // STARŠ
else if (pid == 0) // OTROK
else if (pid < 0)  // NEUSPEH
```
Končanje procesa - exit:
`exit(int status)` ... ==proces se zaključi s podanim izhodnim statusom==, jedro sprosti vire, ...
Izhodni status je 8b vrednost: `0` - uspešen zaključek, `1-127` - koda napake, `128-255` - ostalo
- shrani se v deskriptorju procesa, dokler ga ne prevzame starš

Prevzem izhodnega status otroka - wait:
`int waitpid(pid, &status, opcije)` ... ==čakanje na otroka== - določenega
`int wait(&status)` ... čakanje na otroka - poljubnega

Zagon programa - exec:
==Nadomestitev trenutnega procesa== - nov naslovni prostor (koda, sklad, kopica, ...) in trenutni deskriptor procesa se ponastavi (ohranijo se PID , PPID, odprte datoteke, trenutni imenik, ...)
Pri klicu lahko podamo tudi argumente in okoljske spremenljivke (vse je lokalno)
![[OS_ProcesniAPI_exec.png|400]]
### Primerjava
Prednosti `fork` in `exec`: preprosto ustvarjanje, ločeno ustvarjanje in nalaganje
Slabosti `fork` in `exec`: kopiranje celotnega naslovega prostora je neučinkovito
- optimizacija`vfork()` ... če je takoj za tem kicem `exec()` se kopiranje preskoči
- optimizacija Copy-On-Write ... leno kopiranje po potrebi (ob prvem pisanju)