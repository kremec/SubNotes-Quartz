==Relacija pripadnosti==: $x\in A$ ("$x$ pripada $A$")
Podajanje množic:
- naštevanje elementov (npr. $A=\{0,1,2\}$)
- z [[Predikatni račun|izjavno formulo]] (npr. $A=\{x;\varphi(x)\}$)

==Prazna množica==: $A=\emptyset$

==Enakost množic==: $A=B \iff \forall x(x\in A \iff x\in B)$
==Podmnožica==: $A \subseteq B \iff \forall x(x\in A \implies x\in B)$

==Unija==: $A \cup B = \{x;x\in A \lor x\in B\}$
==Presek==: $A \cap B = \{x;x\in A \land x\in B\}$
==Razlika==: $A \setminus B = \{x;x\in A \land x\notin B\}$
==Simetrična razlika==: $A + B = \{x;x\in A \veebar x\in B\}$

Lastosti operacij:
$$
\begin{aligned} A=B &\iff A \subseteq B \land B \subseteq A \\ A \subseteq B &\implies A \cup C \subseteq B \cup C \\ A \subseteq B &\implies A \cap C \subseteq B \cap C \\ A \cap B \subseteq A &\subseteq A \cup B \end{aligned}
$$

==Univerzalna množica==: vse obravnavane množice so vsebovane v univerzalni množici $S$ (ustreza področju pogovora v [[Predikatni račun|predikatnem računu]]) 
==Komplement množice==: $A^C = S\setminus A$

Dogovor o prioriteti operacij:
$$
\cup,+ \ \lt \ \cap,\setminus \ \lt \ ^C
$$

==Potenčna množica==: $\mathcal{P}A=\{B;B\subseteq A\}$ je množica vseh podmnožic množice $A$.
Tako $\emptyset$ kot $A$ pripadata $\mathcal{P}A$

==Kartezični produkt==: $A\times B = \{(a,b);a\in A \land b\in B\}$ je množica vseh urejenih parov (urejenih n-teric) množic $A$ in $B$ z  $m*n$ elementi
$A^n := A\times A\times \ ... \ \times A$
## Enakosti množic
(podobno kot [[Izjave#Zakoni izjavnega računa|zakoni izjavnega računa]])
1. Zakon dvojnega komplementa: 
$$
\begin{aligned} (A^C)^C&=A \end{aligned}
$$
2. Idempotenca:
$$
\begin{aligned} A \cap A &= A \\ A \cup A &= A \end{aligned}
$$
3. Komutativnost:
$$
\begin{aligned} A \cap B &= B \cap A \\ A \cup B &= B \cup A \\ A + B &= B + A \end{aligned}
$$
4. Asociativnost:
$$
\begin{aligned} (A \cap B) \cap C &= A \cap (B \cap C) \\ (A \cup B) \cup C &= A \cup (B \cup C) \\ (A + B) + C &= A + (B + C) \end{aligned}
$$
5. Absorpcija:
$$
\begin{aligned} A \cap (A \cup B) &= A \\ A \cup (A \cap B) &= A \end{aligned}
$$
6. Distributivnost:
$$
\begin{aligned} (A \cap B) \cup C &= (A \cup C) \cap (B \cup C) \\ (A \cup B) \cap C &= (A \cap C) \cup (B \cap C) \\ (A+B)\cap C &= (A\cap C) + (B\cap C) \end{aligned}
$$
7. de Morganova zakona:
$$
\begin{aligned} (A \cup B)^C &= A^C \cap B^C \\ (A \cap B)^C &= A^C \cup B^C \end{aligned}
$$
8. Kontrapozicija:
$$
\begin{aligned} A \subseteq B &= B^C \subseteq A^C \end{aligned}
$$
9. Lastnosti prazne množice $\emptyset$ in univerzalne množice $S$:
$$
\begin{aligned} A \cup A^C &= S \\ A \cap A^C &= \emptyset \\ A+A &= \emptyset \\ A+A^C &= S \end{aligned}
$$
10. Še lastnosti $\emptyset$ in $S$:
$$
\begin{aligned} A \cap \emptyset &= \emptyset \\ A \cup \emptyset &= A \\ A \cap S &= A \\ A \cup S &= S \end{aligned}
$$
11. Lastnosti vsebovanosti:
$$
\begin{aligned} A \subseteq B \sim A\cup B=B &\sim A\cap B=A \sim A \setminus B=\emptyset \\ A \subseteq B &\implies A\cup C \subseteq B\cup C \\ A \subseteq B &\implies A \cap C \subseteq B \cap C \\ A\cap B &\subseteq A \\ B &\subseteq A \cup B \end{aligned}
$$
12. Lastnosti razlike množic:
$$
\begin{aligned} A\setminus B &= A\cap B^C \end{aligned}
$$
13. Lastnosti simetrične razlike:
$$
\begin{aligned} A+B &= (A\setminus B) \cup (B\setminus A) \\ A+B &= (A\cup B)\setminus (A \cap B) \end{aligned}
$$
14. Lastnosti kartezičnega produkta:
$$
\begin{aligned} A\times B &\neq B\times A \\ A\times(B\cup C) &= (A\times B) \cup (A\times C) \\ (A\cup B)\times C &= (A\times C) \cup (B\times C) \\ (A\cap B)\times C &= (A\times C) \cap (B\times C) \\ (A\cap B)\times (C\cap D) &= (A\times C) \cap (B\times D) \\ \\ A\times B=\emptyset &\iff A=\emptyset \lor B=\emptyset \\ A \subseteq C \land B \subseteq D &\implies A\times B \subseteq C\times D \\ A\times B \subseteq C\times D \land A\times B \neq \emptyset &\implies A\subseteq C \land B\subseteq D \end{aligned}
$$

### Sistem enačb z množicami
Reševanje sistemov enačb z 1 neznanko:
- $A\subseteq B \iff A\cap B^C = \emptyset$
- $A \cup B = \emptyset \iff A=\emptyset \land B=\emptyset$
- $A\cap B \subseteq A \subseteq A\cup B$
- $A+B = \emptyset \iff A=B$
- $A\cup B \subseteq C \iff A\subseteq C \land B\subseteq C$
- $A\subseteq B\cap C \iff A\subseteq B \land A\subseteq C$
### Moč množic
==Moč množice== oz. število elementov A: $|A|$
Primeri: $|\emptyset|=0$, $|\{0, 1\}|=2$, $|\{\{0,1\}\}|=1$

Lastnosti:
- $|A\times B|=|A|*|B|$
- $|\{f; \ f:A\rightarrow B\}|=|B^A|=|B|^{|A|}$
- $|\mathcal{P}A|=2^{|A|}$
- $|A\setminus B|=|A|-|A\cap B|$

==Načelo vljučitev in izključitev==: 
$$
\begin{aligned} |A\cup B|&=|A|+|B|-|A\cap B| \\ |A\cup B\cup C|&=|A|+|B|+|C|-|A\cap B|-|A\cap C|-|B\cap C|+|A\cap B\cap C| \end{aligned}
$$