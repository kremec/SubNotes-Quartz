==Kod==: preslikava osnovna abeceda A $\rightarrow$ kodirna abeceda B
- ==Povprečna dolžina koda==:
$$
L=\sum_{i=1}^n p_il_i
$$
- ==Kodno drevo==: listi - vozlišča, ki predstavljajo kodne zamenjave
- ==Razvrstitev kodov==:
![[TIS_Kodiranje_RazvrstitevKodov.png|350]]
![[TIS_Kodiranje_RazvrstitevKodovTabela.png|400]]

==Singularni kodi== (5): različnim znakom je prirejena ista kodna zamenjava
==Enakomerni kodi==: dolžina vseh kodnih zamenjav je enaka
==Enoznačni kodi== (1): poljuben niz znakov lahko dekodiramo le na en sam način
==Neenoznačni kodi== (2): npr. 01 lahko dekodiramo kot $s_3$ ali $s_1 + s_2$
==Netrenutni kodi== (3): kodna beseda je lahko predpona druge kodne besede $\rightarrow$ gledati je treba vnaprej, da veš kateri zamenjavi pripada trenutni znak

==Trenutni kodi== (4):
==Zadostni pogoj trenutnosti koda==: nobena kodna beseda ni predpona nobeni drugi kodni besedi
### Kraftova neenakost
==Potrebni pogoj za trenutnost koda==:
$$
\sum_{i=1}^n r^{-l_i}\leq 1
$$
### I. Shannonov teorem
Entropija je spodnja meja $L$:
$$
H_r(X)\leq L \iff \frac{H(X)}{log(r)}\leq L
$$
==Idealni kod== - $L$ je enaka entropiji:
$$
H_r(X)=L \iff l_i=-log_r(p_i)
$$
==Gospodarni kod== - $L$ je znotraj mej $[H_r(X), H_r(X)+1]$:
$$
H_r(X) \leq L \lt H_r(X)+1
$$
==Optimalni kod==: ima najmanjšo možno povprečno dolžino kodnih zamenjav - najbolj optimalen gospodarni kod (včasih idealni kod ne obstaja):

==Učinkovitost koda==:
$$
\mu=\frac{H_r(X)}{L} = \frac{H(X)}{L*log(r)}
$$

==I. SHannonov teorem==: z združevanjem koda v bloke - večanjem $m$ se $L$ približuje entropiji:
$$
\lim_{m\to\infty}\frac{L_m}{m}=H(X)
$$