### Newtonov zakon za vrtenje
Iz [[Dinamika#Newtonovi zakoni za toga telesa|2. Newtonovega zakona]] se da za kroženje izpeljati navor - silo, ki prek ročice deluje na vrtišče:
$$
\vec M=\vec r\times\vec F=J\vec \alpha
$$
Medsebojne smeri vektorjev: $\vec r$ - palec, $\vec F$ - kazalec, $\vec M$ - sredinec
Smer vrtenja: $\vec M$ - palec desne roke, ostali prsti kažejo v smeri urinega kazalca (pozitivna) oz obratno (negativna)

$$
\begin{aligned} A&=\vec M\cdot\vec \varphi \\ P&=\vec M\cdot\vec w \end{aligned}
$$
### Vztrajnostni moment
Vztrajnostni moment je odvisen od oblike telesa in porazdelitve mase - več mase leži dlje od osi vrtenja, večji bo vztrajnostni moment:

Točkasto telo:
$$
J=mr^2
$$
Sistem teles:
$$
J=\sum_im_ir_i^2
$$
Zvezna telesa:
$$
J=\int dm\ r^2
$$
Zvezna homogena telesa:
$$
J=\int\rho r^2\ dV
$$

Krogla: $J=\frac{2}{5}mr^2$
Disk: $J=\frac{1}{2}mr^2$
Pokončen valj: $J=\frac{1}{2}mr^2$
Ležeč valj okoli središča (osi): $J=\frac{1}{12}mh^2$
Ležeč valj okoli krajišča: $J=\frac{1}{3}ml^2$
Pokončen tulec: $J=mr^2$

Steinerjev izrek: pri premiku osi vrtenja za razdaljo $R$ se osnovni $J^*$ poveča (oddaljujemo od osnovnega) / pomanjša (približujemo se osnovnemu):
$$
J=mR^2\pm J^*
$$

$$
W_k=\frac{1}{2}mv_t^2(1+\frac{J}{mr^2})
$$
### Energija vrtenja
$$
\begin{aligned} A&=\int\vec M \ d\vec \varphi \\ P&=\vec M \ \frac{d\vec \varphi}{dt}=\vec M\vec w \\ A&=J\int\vec\alpha \ d\vec\varphi=\Delta(\frac 12Jw^2) \end{aligned}
$$

> [!example]- Kotaljenje
> $$
> \begin{aligned} w&=\frac{v_t}{R} \\ W_k&=\frac 12 mv_t^2(1+\frac{J}{mR^2}) \end{aligned}
> $$

### Vrtilna količina
Podobno kot [[Dinamika#Newtonovi zakoni za toga telesa|2. Newtonov zakon]] - samo menjamo količine: $\vec M\to\vec F$, $J=m$, $\vec\alpha=\vec a$
$$
\vec M=J\vec\alpha
$$
Izrek o vrtilni količini (podobno kot [[Gibalna količina in trki#Gibalna količina|gibalna količina]], a pri vrtenju z navori)
$$
\int\vec M \ dt=J\int\vec\alpha \ dt=J\vec w=\vec \Gamma
$$
$$
\vec \Gamma=\vec r\times\vec G=\ ... \ =mr^2\vec w
$$
### Precesija
Način gibanja osno simetrične vrtavke (npr. giroskopa) pod vplivom zunanjega navora, denimo takrat, ko vrtavka ni podprta v težišču
![[Navor in vrtilna količina-Image-1.gif]]
$$
\begin{aligned} \vec\Gamma&=J\vec w_0 \\ \vec M_g&=\vec r\times\vec F_g \end{aligned}
$$
$\vec\Gamma$ je ves čas pravokotna na $\vec M_g$ in opisuje krožnico