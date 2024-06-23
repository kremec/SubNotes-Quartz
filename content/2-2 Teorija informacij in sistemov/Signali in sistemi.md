#TODO-EXAMPLES #TODO-LINKS FOURIEROVA TRANSORMACIJA V PRAKSI ZA SIGNALE
### Invariantnost sinusoid
Vhodni signal:
$$
x(t)=Asin(2\pi\nu t+\Theta)
$$
se pri prehodu skozi medij popači v izhodni signal: ==drugačna amplituda== $A$ in/ali ==faza== $\Theta$; a ==ohranja frekvenco== $\nu$
### Fourierova vrsta in transformacija
==Vsako periodično funkcijo lahko zapišemo kot kombinacijo sinusoid==, nakar lahko obravnavamo obnašanje posameznih sinusoid in združimo ločene rezultate
#### Fourierova vrsta
$sin(t)$ ima periodo $T=2\pi$ $\rightarrow$ $sin(\frac{2\pi t}{T})$ ima periodo $T$ in frekvenco $\nu_0=\frac1T$
$$
\omega_0=2\pi\nu_0=\frac{2\pi}{T}
$$
Višji harmoniki sinusoide s frekvenco $\nu_0$ so sinusoide s frekvencami večkratniki osnovne frekvence
Vsako periodično funkcijo $x(t)$ s periodo $T$ lahko zapišemo kot:
$$
x(t)=\frac{a_0}{2}+\sum_{n=1}^{\infty}a_n*cos(n\omega_0t)+\sum_{n=1}^{\infty}b_n*cos(n\omega_0t)
$$
$$
a_0=\frac 2T\int_0^Tx(t)dt
$$
$$
a_m=\frac 2T\int_0^Tx(t)*cos(m\omega_0t)dt
$$
$$
b_m=\frac 2T\int_0^Tx(t)*sin(m\omega_0t)dt
$$
ali z uporabo Eulerjeve formule:
$$
x(t)=\sum_{n=-\infty}^{\infty}c_n*e^{in\omega_0t}
$$
$$
c_m==\frac 1T\int_0^Tx(t)*e^{-im\omega_0}
$$
Zdaj združimo oba zapisa:
$$
x(t) = c_0+\sum_{n=1}^{\infty}c_n*(cos(n\omega_0t) + isin(n\omega_0t) + \sum_{n=1}^{\infty}b_n*(cos(n\omega_0t) + isin(n\omega_0t)
$$
#### Fourierova tranformacija
Fourierovo vrsto poslošimo s periodo $T\rightarrow \infty$: vsaka funkcija ima lahko periodo v neskončnosti
FT:
$$
x(t)=\int_{-\infty}^{\infty}X(\nu)*e^{i2\pi\nu t}
$$
IFT:
$$
X(\nu)=\int_{-\infty}^{\infty}x(t)*e^{-i2\pi\nu t}
$$
Lastnosti Fourierove transformacije:
- ==linearnost==: $f(t)=ax(t)+by(t) \rightarrow F(\nu)=aX(\nu)+bY(\nu)$
- ==skaliranje==: $f(t)=x(at) \rightarrow F(\nu)=\frac1{|a|}X(\frac 1a\nu)$
- ==premik==: $f(t)=x(t-t_0) \rightarrow F(\nu)=e^{-i2\pi\nu t_0}*X(\nu)$
- ==modulacija==: $f(t)=e^{i2\pi t\nu_0}*x(t) \rightarrow F(\nu)=X(\nu-\nu_0)$
- ==konvolucija==: $f(t)=\int_{-\infty}^{\infty}x(t-\tau)y(\tau)d\tau \rightarrow F(\nu)=X(\nu)Y(\nu)$
#### Resonanca
Do resonance pride, ko je frekvenca vsiljenega nihanja enaka frekvenci lastnega nihanja $\rightarrow$ pride do ojačitve aplitud
#### Modulacija in frekvenčni premik
$$
sin(2\pi\nu_1t)sin(2\pi\nu_2t)=\frac12[ \ cos(2\pi(\nu_1-\nu_2)t)-cos(2\pi(\nu_1+\nu_2)t) \ ]
$$
$$
cos(2\pi\nu t)=sin(2\pi\nu t + \frac\pi2)
$$
Produkt sinusiod z različnima frekvencama lahko pretvorimo v vsoto sinusoid $\rightarrow$ hkraten prenos več signalov po istem mediju
#### Energija signala
==Parsevalov teorem==:
$$
E=\int_{-\infty}^{\infty}x(t)^2dt = \int_{-\infty}^{\infty}X(\nu)^2f\nu
$$
### Teorem vzorčenja
Diskreten signal je definiran le ob točkah vzorčenja $x_k=x(k*\Delta)$, pri čemer je $\Delta$ perioda vzorčenja
Za zajemanje signalov z računalniki se uporabljajo ADC (Analog Digital Converter) pretvorniki, ki imajo končno natančnost - signal po kvantizaciji opišemo s končno mnogo aplitudami po shemi USB (Unipolar Straight Binary):
![[TIS_SignaliInSistemi_USB.png|300]]

Pretvorba analogno v digitalno:
$$
b=min(\lfloor \frac{x}{x_{FS}}*2^n+\frac 12 \rfloor, \ 2^n-1)
$$
Pretvorba digitalno v analogno:
$$
x=\frac{b}{2^n}*x_{FS} \ \ \pm \frac{x_{FS}}{2^{n+1}}
$$

Kako pogosto vzorčiti, da ne izgubimo informacij? $\rightarrow$ $\nu_c$ ... najvišja opažena frekvenca v signalu $\implies$ $2\nu_c$ ... potrebna frekvenca vzorčenja
 ### Diskretna Fourierova transformacija
DFT:
$$
X_n=\sum_{k=0}^{N-1}x_k*e^{-i2\pi nk / N}
$$
IDFT:
$$
X_n=\frac 1N\sum_{k=0}^{N-1}x_k*e^{i2\pi nk / N}
$$
Diskretna različica Parsevalovega teorema:
$$
\sum_{k=0}^{N-1}|x_k|^2=\frac 1N\sum_{n=0}^{N-1}|x_n|^2
$$