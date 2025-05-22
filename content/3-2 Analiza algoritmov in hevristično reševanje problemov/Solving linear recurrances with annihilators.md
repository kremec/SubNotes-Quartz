==Linear reccurance==: $T(n)$ is a linear combination of nearby values $T(n-1)$, $T(n-2)$, ...
==Operator==: higher order function, taking other functions as arguments (eg. integral, differential, ... )

| Operator       | Definition                                            |
| -------------- | ----------------------------------------------------- |
| Addition       | $(f+g)(n)=f(n)+g(n)$                                  |
| Substraction   | $(f-g)(n)=f(n)-g(n)$                                  |
| Multiplication | $(\alpha*f)(n)=\alpha*(f(n))$                         |
| Shift          | $Ef(n)=f(n+1)$                                        |
| $k$-fold shift | $E^kf(n)=f(n+k)$                                      |
| Composition    | $(X+Y)f=Xf+Yf$<br>$(X-Y)f=Xf-Yf$<br>$XYf=X(Yf)=Y(Xf)$ |
| Distribution   | $X(f+g)=Xf+Xg$                                        |
### Annihilator
==Annihilator==: nontrivial operator transforming function to 0
- every function composed of polinomial/exponential functions has a unique minimal annihilator

| Operator                   | Function annihilated               |
| -------------------------- | ---------------------------------- |
| $E-a$                      | $\alpha*a^n$                       |
| $(E-a_0)(E-a_1)...(E-a_k)$ | $\sum_{i=0}k\alpha*a_i^n$          |
| $(E-a)^d$                  | $(\sum_{i=0}^{d-1}\alpha_in^i)a^n$ |
- $X$ annihilates $f$ $\implies$ $X$ annihilates $Ef$
- $X$ annihilates $f$ $\implies$ $X$ annihilates $\alpha f$ for any constant $\alpha$
- $X$ annihilates $f$ and $g$ $\implies$ $X$ annihilates $f\pm g$
- $X$ annihilates $f$ and $Y$ annihilates $g$ $\implies$ $XY$ annihilates $f\pm g$
#### Annihilating recurrances
1. Write recurrance in operator form
2. Extract an annihilator for the recurrance
3. Factor the annihilator (if necessary and possible)
4. Extract the generic solution from the annihilator
5. Solve for coefficients using the base cases (if known)

> [!example] Example
> $\tau(n)=5\tau(n-1)\ ; \ \tau(0)=3$
> $$
> \begin{align}
> \tau(n)-5\tau(n-1)=0 \\
> \tau(n+1)-5\tau(n)=0 \\
> E\tau-5\tau=0 \\
> (E-5)\tau(n)
> \end{align}
> $$
> $\tau(n)=\alpha*5^n$ ... generic solution
> $\tau(0)=3 \implies 3=\alpha*5^0 \implies \alpha=3$
> $\tau(n)=3*5^n$