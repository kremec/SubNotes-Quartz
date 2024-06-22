## Delo z lupino
#### Pisanje / branje - stdout / stdin
```bash
# Pisanje na standardni izhod #
echo "Operacijski   Sistemi"
echo -n "Without newline"
echo -e "escape\t\tcharacters\nhello"
printf "Answ=%10d\!\n" 42
printf "%.10f\n" 3.14
date

# Branje iz standardnega vhoda #
read -p "Vpiši ime: " ime

# Kombinacija obojega #
cat
```
#### Tip ukazov
==Vgrajeni (builtin)== ali ==zunanji (external)==
```bash
# Ugotavljanje tipa ukaza # 
type echo
type -a echo

# Izvajanje vgrajenega ukaza #
builtin echo

# Izvajanje zunanjega ukaza #
/usr/bin/ls
```
#### Spremenljivka PATH
```bash
# Izpis $PATH #
echo $PATH

# Izpis imenika, kjer se nahaja dani ukaz #
which echo
```
#### Zgodovina vnešenih ukazov
```bash
# Izpis ukazov v dnevniku #
history

# Izbris dnevnika #
history -c

# Kapaciteta dnevnika #
echo $HISTSIZE

# Izvedba ukaza št. 2 #
!2

# Izvedba predhodno izvedenega ukaza #
!!
```
#### Kombinacije tipk
- `CTRL+C` ... prekinitev
- `CTRL+Z` ... zaustavitev
- `CTRL+D` ... konec vnosa podatkov
#### Vgrajen uporabniški priročnik
```bash
man echo
man man
man bash
```
#### Delo z imeniki
Upoštevaj ==absolutno / relativno pot==
```bash
# Trenutni delovni imenik #
pwd
echo $PWD

# Domači imenik #
echo $HOME

# Premiki po imenikih #
cd
cd ~
cd imenik
cd .
cd ..
cd /

# Ustvarjanje imenikov #
mkdir imenik
mkdir imenik1 imenik2 imenik3
mkdir -p imenik1/imenikZnotraj

# Delo z imeniki #
cp -R src dest

# Odstranjevanje imenikov #
rmdir razenImenik
rmdir -rf neprazenImenik
```
#### Delo z datotekami
Ujemanje vzorcev z imeni datotek:
```bash
ls *
ls *.txt
ls A*
ls A?
echo test[[:digit:]].txt
```
Pregled: `more`, `less`, `od`, `hexdump`, ...
Urejanje: `vi`, `vim`, `emacs`, `nano`, ...
```bash
cp /etc/shadow ~/geslo
mv geslo gesla
rm gesla

# Drugi uporabni ukazi #
cat  # izpis vsebine podane datoteke
head / tail  # izpis začetnega / končnega dela datoteke
cut  # rezanje po stolpcih
sort / shuf / rev  # urejanje / permutiranje po vrsticah / obrat vrstic
uniq  # izločanje zaporedno podvojenih vrstic
nl  # številčenje vrstic
tr  # menjava znakov
wc  # štetje vrstic, besed in znakov
grep  # filtriranje vrstic glede na podani vzorec - regularni izraz
```
#### Terminal
Mreža znakov
```bash
$TERM  # vrsta terminala
$LINES / $COLUMNS  # št. vrstic / stolpcev tekstovne mreže terminala
clear  # brisanje zaslona terminala
tty  # izpiše ime trenutnega terminala
tset  # resetiranje terminaa
stty  # lastnosti terminala
```
## Skriptiranje
Zgradba skripte:
- =="Shebang"== `#!/bin/bash`
- Zaporedje ukazov in komentarjev
- Zaključek skripte - impliciten zaključek ali `exit STATUS`
  [[Procesni API|Izhodni status]] nazadnje izvedenega ukaza: `echo $?`

Zagon skripte: `./skripta.sh` ali `bash skripta.sh`
#### Argumenti skripte
```bash
$#  # št. vseh argumentov
$0  # ime skripte
$1 / $2, ...  # posamezni argumenti skripte
$* / $@  # vsi argumenti skripte
shift  # obdelovanje argumentov zaporedoma
```
#### Spremenljivke
==Globalne== - `ime=vrednost` / ==lokalne== - `local ime=vrednost`
Pazi na presledke (pri deklariraju spremenljivk jih ni)!
Navednice: ==enojne== dobesedno predstavijo niz / ==dvojne== - izvedejo se notranje substitucije

Substitucije vrednosti spremenljivk:
```bash
$ime / ${ime}  # priklic vrednosti spremenljivke
${ime:-privzeto}  # priklic shranjene ali privzete vrednosti

${#ime}  # dolžina niza, shranjenega v `ime`
${ime:poz}  # podniz od indeksa `poz` do konca
${ime:poz:dol}  # podniz od indeksa `poz` dolžine `doz`

${ime#vzorec}  # najkrajša predpona
${ime##vzorec}  # najdaljša predpona
${ime%vzorec}  # najkrajša pripona
${ime%%vzorec}  # najdaljša pripona

${ime/vzorec/vrednost}  # prva pojavitev
${ime//vzorec/vrednost}  # vse pojavitve
```
#### Pogojni izrazi
```bash
# Ovrednotenje pogoja #
test pogoj
[ pogoj ]  # pazi na presledke!
[[ pogoj ]]  # bash-specifičen
```
Rezultat obimo preko izhodnega statusa - `$?`
```bash
# Primerjava nizov #
[[ -z niz ]]  # Je niz prazen (dolžina 0, zero)?
[[ -n niz ]]  # Je niz neprazen (dolžina >0, nozero)?
[[ niz1 = niz2 ]]  # Sta niza enaka?
[[ niz1 != niz2 ]]  # Sta niza različna?
[[ niz1 < niz2 ]]  # Je niz1 leksikografsko pred niz2?
[[ niz1 > niz2 ]]  # Je niz1 leksikografsko za niz2?

# Preverjanje datotek #
[[ -e pot ]]  # Ali datoteka obstaja?
[[ -f pot ]]  # Je datoteka navadna (regular file)?
[[ -d pot ]]  # Je datoteka imenik?
[[ -L pot ]]  # Je datoteka simbolična povezava?
[[ -b pot ]]  # Je datoteka bločna naprava?
[[ -c pot ]]  # Je datoteka znakovna naprava?

# Logični izrazi - in, ali, negacija - bash-specifično in splošno #
[[ -n "$x" && -f /etc/passwd ]]
test -n "$x" -a -f /etc/passwd

[[ -f "$f" || test -L "$f" ]]
[ -f "$f" -o test -L "$f" ]

[[ ! –f /etc/passwd ]]
test ! –f /etc/passwd

# Aritmetični pogoji #
[ a -eq b ]  # Je a enako b?
[ a -ne b ]  # Je a različno od b?
[ a -gt b ]  # Je a večje od b?
[ a -ge b ]  # Je a večje ali enako od b?
[ a -lt b ]  # Je a manjše od b?
[ a -le b ]  # Je a manjše ali enako od b?
```
Oba `&&` in `||` sta enake prioritete!
#### Ovrednotenje izraza
Samo ovrednotenje (npr. računanje): `(( izraz ))`
Ovrednotenje in substitucija: `$(( izraz ))`
#### Odločitvena stavka
```bash
if pogoj; then ukazi; elif pogoj; then ukazi; else ukazi; fi

akcija=$1
shift
case $akcija in
  help) do_help ;;
  list_all) ls –R "$1" ;;
  update) shift; do_update $* ;;
  *) echo Napačna akcija.
esac
```
#### Zanke
```bash
while pogoj; do ukazi; done
until pogoj; do ukazi; done

for var in spisek; do ukazi; done
for ((init; pogoj; inkrement)); do ukazi; done
```
#### Ujemanje vzorcev z nizi
`*` - poljuben niz, `?` - poljuben znak, `[...]` - poljuben znak znotraj oglatih oklepajev
```bash
case $niz in
  bingo) echo 1 ;;
  bin*) echo 2 ;;
  [abc]ingo) echo 3 ;;
  ???go) echo 4 ;;
  ??) echo 5 ;;
  *) echo 6 ;;
esac
```
## Funkcije
#### Izvajanje v podlupini (subshell)
==Gnezdenje lupin==: znotraj zagnane lupine lahko ustvariš novo lupino $\rightarrow$ hierarhija
Avtomatsko dedovanje spremenljivk, funkcij in odprtih datotek
```bash
# Osnoven zagon podlupine #
( hostname )
( ( ( ( echo –n $BASH_SUBSHELL ) ); echo $BASH_SUBSHELL ) )

# Zagon podlupine s substitucijo #
h=$(hostname)
dirname $(which less)

# Dedovanje spremenljivk #
x=42; echo $x
( echo $x; x=1; echo $x )
echo $x
```
#### Ukazni bloki
```bash
{ ukazi; }

[[ $(whoami) == root ]] && { echo "I'm the boss."; cat /etc/shadow; }
```
Pazi na presledke!
#### Funkcije
```bash
# Definicija funkcij #
function ime { ukazi; }
ime() { ukazi; }

function do_big_thing { cat /etc/passwd | cut -d: -f7 | sort | uniq -c } do_big_thing

# Argumenti funkcije #
function fullname {
    local name=${1:-Janez}
    local surname=${2:-Novak}
    echo $name $surname
}
fullname Klemen

# Rezultat funkcije - uporabimo standardni izhod, rezultat ujamemo  #
function vsota {
    local vsota=0
    while [[ -n $1 ]]; do
        (( vsota += $1 ))
        shift
    done
    echo $vsota
    return 0
}
vsota 1 2 4 3
```

```bash
# Ogrodje skripte #
function run_update { ... }
function get_upgrade { ... }
function print_help { ... }
  
action=$1
shift
case $action in
    update) run_update $* ;;
    upgrade) get_upgrade $* ;;
    list_home) ls -R ~ ;;
    version) echo Version 3.14
    help) print_help
esac
```
## Posli in preusmerjanje
#### Nadzor poslov
Zagon ukaza v ospredju: starševska lupina zažene proces (otroka), čaka da se otrok konča in prevzame njegov izhodni status
Zagon ukaza v ozadju: starševska lupina zažene proces (otroka), ne čaka da se otrok konča in prevzame njegov izhodni status, ko OS aktivira `SIGCHLD`

==Posel (job)==: opravilo, ki je v celoti pripravljeno izvajanje, brez posebne interakcije, običajno v ozadju
```bash
jobs  # Izpis trenutno tekočih poslov
fg jid  # Nadaljavanje posla v ospredju
bg jid  # Nadaljevanje posla v ozadju
```
Lupina se konča: pokonča svoje posle in pošlje `SIGHUP`
`Ctrl+Z` - zaustavitev posla v ospredju
Ločitev posla od lupine: `disown`
#### Preusmerjanje
```bash
ukaz <datoteka  # Preusmerjanje stdin (0)
ukaz >datoteka  # Preusmerjanje stdout (1), prepisovanje (owerwrite)
ukaz >>datoteka  # Presumerjanje stdout (1), dodajanje (append)
ukaz 2>datoteka  # Preusmerjanje samo stderr (2)
# Preusmerjanje stdout (1) in stderr (2) #
ukaz 1>datoteka 2>&1
ukaz &>datoteka


# Tukaj niz #
read a b c <<< '1 2 3'
tr '[a-z]' '[A-Z]' <<< velike-crke

# Tukaj dokument #
read –p 'Vnesi ime: ' ime
cat <<EOF >skripta.sh
#!/bin/bash
echo Živjo $ime.
EOF

cat <<'EOF' >skripta.sh
#!/bin/bash
read –p 'Vnesi ime: ' ime
echo Živjo $ime.
EOF
```
```bash
# Preusmerjanje ukazov (command pipeline) #
cat /etc/services | egrep '/tcp' | egrep '42'
cat /etc/passwd | cut –d : -f 7 | sort | uniq –c | sort –gr | head -3 | nl
```
```bash
# Branje datotek #
IFS=':'
while read user pass uid gid rest; do
  echo $((uid + gid))
done < /etc/passwd
```
## Jedro in sistemski klici
```bash
uname  # Izpis informacij od jedru in OS
arch  # Izpis arhitekture procesorja
hostname  # Izpis imena gostiteljskega računalnika
free  # Izpis informacij o pomnilniku
dmesg  # Izpis sistemskih obvestil
sysctl -a  # Izpis sistemskih nastavitev
```
Do jedra lahko dostopamo preko `/proc/` - datoteke:
- `version`, `cmdline`, `uptime`, `modules`
- `cpuinfo`, `meminfo`
- `diskstats`, `filesystems`, `mounts`, `partitions`
- `device`, `dma`, `interrupts`, `iomem`, `ioports`

Do jedra lahko dostopamo tudi preko ==sistemskih klicev== - edini pravi način:
- preko ovojnih funkcij (iz standardne C knjižnice)
- preko funkcije `syscall(...)`
- posredno preko ostalih funkcij
```bash
# Datoteke #
open(), close(), read(), write(), dup(), dup2()
rename(), link(), unlink(), chmod(), chown()

# Imeniki #
opendir(), readdir(), closedir()
chdir(), mkdir(), rmdir(), symlink(), readlink()

# Povezave #
ln -s cilj povezava  # ustvarjanje mehke povezave
readlink povezava  # izpis cilja mehke povezave

ln cilj povezava  # ustvarjanje trde povezave

# Zaščita #
getuid(), getgid(), ...

# Procesi #
fork(), wait(), waitpid(), exit(), ...

# Ostali #
getpid(), getppid(), sleep()
pipe()
kill(), signal()
time()
```

Izhodni status: uspeh `0`, neuspeh `-1`, izjeme:
- `getpid()` in `getppid()` vrneta PID
- `open()` vrne št. datotečnega deskriptorja, `read()` in `write()` vrneta št. obdelanih bajtov

Kodo zadnje napake: spremenljivka `errno`
Izpis obvestila o napaki: funkcija `perror()`

Sledenje sistemskim klicem: ukaz `strace` ali prevajanje z `gcc --static`
Sledenje klicem v libc: ukaz `ltrace`

## Uporabniki
#### Uporabniki
```bash
# Lokalni dostop #
whoami  # kdo sem?
id  # podatki uporabniškega računa
groups  # pripadajoče skupine
passwd  # nastavitev gesla
$UID  # trenutni uid
$HOME  # domači imenik

# Oddaljeni dostop #
users, who, w  # pregled prijav
last, lastb  # zgodovina uspešnih / neuspešnih prijav
$HOSTNAME  # ime računalnika


# Menjava uporabnika #
sudo  # izvajanje podanega ukaza kot drug uporabnik (običajno superuser)
su  # zamenjava uporabnika (substitute user) in zagon lupine
sg / newgrp  # zamenjava skupine

# Uporabniški računi #
useradd  # ustvarjanje uporabniškega računa
userdel  # odstranjevanje uporabniškega računa
usermod  # spreminjanje uporabniškega računa
chsh  # spreminjanje privzete lupine
chpasswd  # spreminjanje gesla
chage  # spreminjanje lastnosti gesla
chgrp  # spreminjanje skupine

# Uporabniške skupine #
groupadd  # ustvarjanje skupine
groupdel  # odstranjevanje skupine
groupmod  # spreminjanje skupine
gpasswd  # nastavitev gesla skupine


# Nadzor dostopa #
chown  # nastavitev lastnika
chgrp  # nastavitev skupine
chown uporabnik:skupina datoteka  # oboje hkrati

chmod [augo][+-=][rwx-] datoteke
chmod u+s uids  # setuid
```
Ročna administracija: datoteke `/etc/passwd`, `/etc/shadow` in `/etc/group`