# Izjave
==Izjava==: stavek, ki je bodisi resničen bodisi neresničen - ima logično vrednost
 - Delitev po vsebini: resnične / neresnične
 - Delitev po obliki: osnovne (npr. "Sije sonce") / sestavljene (npr. "Peter je zunaj in sije sonce")
### Izjavni vezniki
Enomestni (ne) / Dvomestni (in, ali, če ... potem ..., niti ... niti ...)

==Izjavni konstanti==: 0 in 1
==Izjavne spremenljivke==: p, q, r označujejo osnovne izjave

==Resničnostna tabela==: tabela logičnih vrednosti izjavnega izraza za vse nabore logičnih vrednosti izjavnih spremenljivk

==Negacija==: $\neg$
==Konjunkcija==: $\land$
==Disjunkcija==: $\lor$
==Implikacija==: $\implies$
==Ekvivalenca==: $\iff$
==Eksplozivna disjunkcija==: $\veebar$
==Shefferjev veznik==: $\uparrow$
==Pierce-Lukasiewiczev veznik==: $\downarrow$

| $P$ | $Q$ | $\neg P$ | $P \land Q$ | $P \lor Q$ | $P \implies Q$ | $P \iff Q$ | $P \veebar Q$ | $P \uparrow Q$ | $P \downarrow Q$ |
| --- | --- | -------- | ----------- | ---------- | -------------- | ---------- | ------------- | -------------- | ---------------- |
| T   | T   | F        | T           | T          | T              | T          | F             | F              | F                |
| T   | F   | F        | F           | T          | F              | F          | T             | T              | F                |
| F   | T   | T        | F           | T          | T              | F          | T             | T              | F                |
| F   | F   | T        | F           | F          | T              | T          | F             | T              | T                |

Dogovor o prioriteti operatorjev:
$$
\neg \ \lt \  \land,\uparrow,\downarrow \ \lt \ \lor,\veebar \ \lt \ \implies \ \lt \ \iff
$$
==Tavtologija==: izjavni izraz, ki je resničen pri vseh naborih logičnih vrednosti vsebovanih izjavnih spremenljivk (npr. "$1$", "$p \lor \neg p$", "$p \implies (q \implies p)$")
==Protislovje==: izjavni izraz, ki je neresničen pri vseh naborih logičnih vrednosti vsebovanih izjavnih spremenljivk (npr. "$0$", "$p \land \neg p$")

==Enakovredna== izjavna izraza:
- pri vseh naborih logičnih vrednosti izjavnih spremenljivk imata enako vrednost
- izraz $A \iff B$ je tavtologija
## Zakoni izjavnega računa
1. Zakon dvojne negacije: 
$$
\begin{aligned} \neg\neg A &\sim A \end{aligned}
$$
2. Idempotenca:
$$
\begin{aligned} A \land A &\sim A \\ A \lor A &\sim A \end{aligned}
$$
3. Komutativnost:
$$
\begin{aligned} A \land B &\sim B \land A \\ A \lor B &\sim B \lor A \\ A \iff B &\sim B \iff A \end{aligned}
$$
4. Asociativnost:
$$
\begin{aligned} (A \land B) \land C &\sim A \land (B \land C) \\ (A \lor B) \lor C &\sim A \lor (B \lor C) \\ (A \iff B) \iff C &\sim A \iff (B \iff C) \end{aligned}
$$
5. Absorpcija:
$$
\begin{aligned} A \land (A \lor B) &\sim A \\ A \lor (A \land B) &\sim A \end{aligned}
$$
6. Distributivnost:
$$
\begin{aligned} (A \lor B) \land C &\sim (A \land C) \lor (B \land C) \\ (A \land B) \lor C &\sim (A \lor C) \land (B \lor C) \end{aligned}
$$
7. de Morganova zakona:
$$
\begin{aligned} \neg(A \lor B) &\sim \neg A \land \neg B \\ \neg(A \land B) &\sim \neg A \lor \neg B \end{aligned}
$$
8. Kontrapozicija:
$$
\begin{aligned} A \implies B &\sim \neg B \implies A \end{aligned}
$$
9. Lastnosti 0 in 1:
$$
\begin{aligned} A \implies A &\sim 1 \\ A \iff A &\sim 1 \\ A \lor \neg A &\sim 1 \\ A \land \neg A &\sim 0 \end{aligned}
$$
10. Še lastnosti 0 in 1:
$$
\begin{aligned} A \land 0 &\sim 0 \\ A \lor 0 &\sim A \\ A \land 1 &\sim A \\ A \lor 1 &\sim 1 \\ A \implies 0 &\sim \neg A \\ 0 \implies A &\sim 1 \\ A \implies 1 &\sim 1 \\ 1 \implies A &\sim A \end{aligned}
$$
11. Lastnosti implikacije:
$$
\begin{aligned} A \implies B &\sim \neg A \lor B \\ \neg (A \implies B) &\sim A \land \neg B \end{aligned}
$$
12. Lastnosti ekvivalence:
$$
\begin{aligned} A \iff B &\sim (A \implies B) \land (B \implies A) \\ A \iff B &\sim (A \land B) \lor (\neg A \land \neg B) \\ \neg (A \iff B) &\sim \neg A \iff B \end{aligned}
$$
13. Ekskluzivna disjunkcija:
$$
\begin{aligned} A \veebar B &\sim \neg(A \iff B) \\ A \veebar B &\sim B \veebar A \\ (A \veebar B) \veebar C &\sim A \veebar (B \veebar C) \end{aligned}
$$
14. Shefferjev veznik:
$$
\begin{aligned} A \uparrow B &\sim \neg(A \land B) \\ A \uparrow B &\sim B \uparrow A \end{aligned}
$$
15. Pierceov veznik:
$$
\begin{aligned} A \downarrow B &\sim \neg(A \lor B) \\ A \downarrow B &\sim B \downarrow A \end{aligned}
$$
Dualne zakone dobimo z zamenjavo konjunkcije in disjunkcije ter 0 in 1 v (večini) zakonov

Izraz $A_1 \veebar A_2 \veebar \ ... \ \veebar A_n$  je (ne glede na postavitev oklepajev) resničen, ko je liho mnogo členov resničnih.
### Osnovne normalne oblike
==Osnovna konjunkcija/disjunkcija==: konjunkcija/disjunkcija izjavnih spremenljivk in/ali njihovih negacij
==Disjunktivna Normalna Oblika (DNO)==: disjunkcija osnovnih konjunkcij
==Konjunktivna Normalna Oblika (KNO)==: konjunkcija osnovnih disjunkcij
Vsak izjavni izraz ima DNO in KNO
### Polnost nabora izjavnih veznikov
==Poln nabor izjavnih veznikov==: družina izjavnih veznikov N, če za vsak izjavni izraz A obstaja enakovreden izjavni izraz B, ki vsebuje samo veznike iz N.
Primeri: {$\neg,\land,\lor$}, {$\neg,\land$}, {$\neg,\lor$}, {$\neg,\implies$}, {$0,\implies$}, {$\uparrow$}, {$\downarrow$}
Dokaz polnosti nabora izjavnih veznikov: vsak veznik iz že znanega polnega nabora izrazimo samo z uporabo veznikov testiranega nabora
# Sklepanje v izjavnem računu
==Pravilen sklep==: Zaporedje izjavnih izrazov $A_1,A_2, \ ... \ ,A_n,B$ s predpostavkami $A_1,A_2, \ ... \ ,A_n$ in zaključkom $B$, če je zaključek $B$ resničen pri vseh naborih vrednosti izjavnih spremenljivk, pri katerih so resnične vse predpostavke
Izrek: $A_1,A_2, \ ... \ ,A_n \models B \ \iff \ (A_1,A_2, \ ... \ ,A_n) \implies B \ je \ tavtologija$

==Nepravilen sklep== dokažemo s protiprimerom - podamo nabor vrednosti izjavnih spremenljivk, pri katerem so vse predpostavke resnične in zaključek neresničen
### Pravila sklepanja
==Modus Ponens (MP)==: $A,A \implies B \ \models \ B$
==Modus Tollens (MT)==: $A \implies B, \neg B \ \models \ \neg A$
==Hipotetični silogizem (HS)==: $A \implies B, B \implies C \ \models \ A \implies C$
==Disjunktivni silogizem (DS)==: $A \lor B, \neg A \ \models \ B$
==Združitev (Zd)==: $A,B \ \models \ A \land B$
==Poenostavitev (Po)==: $A \land B \ \models \ A,B$
==Pridružitev (Pr)==: $A \models A \lor B$

Pravilnost sklepa dokažemo tako, da sestavimo zaporedje izjavnih izrazov, za vsak člen pa velja:
1. $C_i$ je ena od predpostavk
2. $C_i$ je tavtologija
3. $C_i$ je enakovreden enemu od predhodnih izrazov v zaporedju
4. $C_i$ logično sledi iz predhodnih izrazov po enem od osnovnih pravil sklepov

==Pogojni sklep (PS)==: uporabljamo, kadar ima zaključek sklepa obliko implikacije
$$
A_1,A_2, \ ... \ ,A_k \ \models \ B \implies C \ \ n.t. \ ko \ \ A_1,A_2, \ ... \ ,A_k,B \ \models \ C
$$
==Sklep s protislovjem (RA)==: lahko uporabljamo kadarkoli
$$
A_1,A_2, \ ... \ ,A_k \ \models \ B \ \ n.t. \ ko \ \ A_1,A_2, \ ... \ ,A_k,\neg B \ \models \ 0
$$
==Analiza primerov (AP)==: lahko uporabljamo, kadar ima ena od predpostavk obliko disjunkcije
$$
A_1,A_2, \ ... \ ,A_k,B_1 \lor B_2 \ \models \ C \ \ n.t. \ ko \ \ A_1,A_2, \ ... \ ,A_k,B_1 \ \models \ C \ \ in \ \ A_1,A_2, \ ... \ ,A_k,B_2 \ \models \ C
$$