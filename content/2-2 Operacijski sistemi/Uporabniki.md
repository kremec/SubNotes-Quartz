Topics: #TODO-LINKS 
- - -
OS glede na število uporabnikov:
- ==brezuporabniški / enouporabniški==: ni nadzora nad uporabo virov
- ==večuporabniški==: sočasna uporaba sistema s strani več uporabnikov - lastništvo in nadzor uporabe virov

==Uporabniški račun==: mehanizem, ki omogoča prijavo v (in uporabo) sistema s skupkom podatkov o uporabniku
- ==gost==: anonimni običajni uporabnik, datoteke se navadno ne shranijo
- ==običajni uporabnik==
- ==superuporabnik==: običajni uporabnik, ki lahko začasno dvigne svoje pravice
- ==administrator==: vzdrževalec sistema z vsemi pravicami

==Identifikacija==: ugotavljanje identitete danega uporabnika (npr. uporabniško ime)

==Avtentikacija==: preverjanje istovetnosti danih podatkov in potrjevanje identitete (npr. geslo)
Avtentikacijski dejavniki:
- dejaniki ==znanja== - pomnenje določenih podatkov (npr. geslo)
- ==lastniški== dejavniki - posedovanje fizičnih naprav (npr. ključ)
- ==prirojeni== dejavniki - lastnosti samega uporabnika (npr. prstni odtis)

==Enodejavniška / večdejavniška avtentikacija==: uporaba enega / več dejanikov

### Uporabniki v Linuxu
==Administrator==: uid=0, gid=0, uporabniško ime root, domač imenik /root, običajno onemogočen
==Superuporabnik (sudoer)==: lahko uporablja ukaz `sudo`
==Programski uporabniki==: uporabniški računi programov, običajno uid 200-999
==Ostali uporabniki==: običajno uid > 999, domač imenik /home/username

Datoteka ==/etc/passwd==: vse razen podatkov o geslu
![[OS_Uporabniki_passwd.png|500]]
Datoteka ==/etc/shadow==: zgoščene vrednosti gesel, uporaba **soli**
![[OS_Uporabniki_shadow.png|500]]

Datoteka ==/etc/group==: seznam uporabnikov v skupinah
![[OS_Uporabniki_group.png|550]]
Datoteka ==/etc/gshadow==: zgoščena gesla skupin