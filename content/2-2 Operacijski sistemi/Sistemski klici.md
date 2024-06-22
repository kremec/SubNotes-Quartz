Topics: #TODO-LINKS 
- - -
==Sistemski klic==: zahteva uporabniškega programa po jedrni storitvi - klic podprograma v jedru
Vsak klic ima svojo ==številko== in lahko prejme ==argumente== (preneseta se po pregistrih/skladu)

Preklop nivoja zaščite procesorja: jedro - ==priviligirani način== / klicoči program - ==zaščiten način==
Sistemski vmesnik:
- ==namenski strojni ukazi== za sistemski klic in vrnitev iz njega
- ==programska prekinitev== procesorja, da izvede preklop in pokliče nameščeni rokovalnik **prekinitve**

Ostali mehanizmi:
- ==klicna vrata== - zahteva oddaljeni klic v drug segment
- ==pomnilniška vrsta== - sistemske klice postavimo v vrsto, ki jo jedro periodično pregleduje

Izvedba sistemskega klica:
1. Priprava na sistemski klic - podajanje št. sistemskega klica in aregumentov
2. Vstop v jedro preko sistemskega vmesnika, preklop v priviligiran način
3. Izvedba rokovalnika sistemskega vmesnika - klic specifičnega rokovalnika
4. Izvedba rokovalnika sistemskega klica - kic rutine znotraj jedra
5. Izstop iz jedra, preklop v uporabniški način

Sistemski klici vs običajni funkcijski klici:
- počasnejši, kompleksnejši
- varnejši - nadzor operacij, avtorizacija pred izvedbo ukazov, stabilnejši (tveganje sesutja programa/sistema)

==Ovojna funkcija== zahevno izvedbo sistemskega klica pretvori v sistemski klic - sama pripravi in preverja pogoje pred vstopom v jedro

Izvedba sistemskega klica:
- ==neposredno== - nastavitev registrov in vstop v jedro v zbirniku
- preko ==specifične ovojne funkcije== iz knjižnice
- preko ==splošne ovojne funkcije== `syscall()`, ki ji podamo št. specifičnega sistemskega klica
- preko ostalih funkcij (npr. `printf()`)
![[OS_SistemskiKlici_OvojneFunkcije.png|400]]

Vmesniki za uporabo programskih knjižnic:
==Aplikacijski programski vmesnik (API)== temelji na simbolični predstavitvi z imeni funkcij
Primer: Windows NT OS:
- dinamična knjižnica `ntdll.dll` (Native API) - ovojne funkcije neporednih izvedb sistemskih klicev, nedokumentirana
- dinamična knjižnica `kernel32.dll` (Windows API) - ovojne funkcije, ki kličejo ovojne funkcije iz `ntdll.dll`

==Aplikacijski dvojiški vmesnik (ABI)==: temelji na številski predstavitvi s številskimi oznakami funkcij

==Portable Operating System Unterface Unix (POSIX)== - IEEE 1003: definira programski vmesnik med aplikacijami in OS - predpisuje funkcije, ukazno lupino, okoljske spremenljvke, datotečno hierarhijo, ...
==Single Unix Specificatioon (SUS)== - IEEE in Open Group: temelji na IEEE POSIX
Skladnost s SUS standardom:
- ==certificirani Unix sistemi==: HP-UX, macOS, ...
- ==necertificirani Unix sistemi==: Linux, BSDs, ...
- ==ostali necertificirani sistemi==: WSL, Cygwin, ...