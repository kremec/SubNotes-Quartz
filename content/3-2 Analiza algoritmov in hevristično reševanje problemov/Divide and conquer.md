Idea: ==divide== the problem into several (equal) parts $\rightarrow$ ==(recursively) conquer/solve== each of the sub problems $\rightarrow$ ==combine== sub problem solutions
#### Substitution method
Guess the solution, then find the constants using induction
Prove solution validity with induction

> [!example] Example
> $T(n)=2T(\frac n2)+nlogn$
> Assume: $T(n)=O(nlogn)$
> Prove: $T(n)\leq c*nlogn \ \ ; \ c>0,\ n>n_0$
> Inductive assumption: $T(n)\leq c*2*\frac n2log\frac n2+n=\ ...\ =cn*logn-n(1-c)$
> Base case: $T(1)$ not, but $T(2)$ yes
#### Recursive tree
Draw recursive tree, then sum complexity level-wise and altogether
Prove solution validity with induction

> [!example] Example
> $T(n)=T(\frac n3)+T(\frac{2n}3)+\Theta(n)$
> Assume: $T(n)\leq T(\frac n3)+T(\frac{2n}3)+cn$, $T(1)=\Theta(1)$
> Draw tree:
> ![[Divide and conquer-Image-1.png|400]]
> Proof by induction: $T(n)\leq d*nlogn$
#### Master theorem
1. Get $a$, $b$ and $f(n)$ from:
$$
T(n)=aT(\frac nb)+f(n)
$$
2. Calculate $n^{log_ba}$
3. Use it to determine the asymptotic bounds of $T(n)$:
   Less / more leafs in recursion tree $\rightarrow$ peak dominates (1. rule) / bottom dominates (3. rule)
$$
\begin{align}
f(n)=O(n^{log_ba-\epsilon}) &\implies T(n)=\Theta(n^{log_ba}) \\
f(n)=\Theta(n^{log_ba-\epsilon}) &\implies T(n)=\Theta(n^{log_ba}logn) \\
f(n)=\Omega(n^{log_ba+\epsilon}) &\implies T(n)=\Theta(f(n))
\end{align}
$$

> [!example] Example
> $T(n)=3T(\frac n4)+nlogn$ $\rightarrow$ $a=3$, $b=4$, $f(n)=nlogn$
> $n^{log_ba}=n^{log_43}\in(0,1)$
> $nlogn\neq O(n^{log_43-\epsilon})$, $nlogn\neq\Theta(n^{log_43-\epsilon})$
> $nlogn=\Omega(n^{log_43+\epsilon})$ $\rightarrow$ $T(n)=\Theta(nlogn)$
#### Akra-Bazzi theorem
1. Get all $a_i$, $b_i$ and $f(n)$ which must be polinomially limited
2. Calculate $p$ in $\sum a_i*(b_i)^p = 1$
3. Use it to determine the asymptotic bounds of $T(n)$:
$$
T(x)=\Theta(x^p(1+\int_1^x\frac{f(u)}{u^{p+1}}du))
$$

> [!example] Example
> $T(n)=T(\frac {3n}4)+T(\frac n4)+n$ $\rightarrow$ $a_1=1$, $b_1=\frac 34$, $a_2=1$, $b_2=\frac 14$, $f(n)=nlogn$
> $1*(\frac 34)^p+1*(\frac 14)^p=1$ $\rightarrow$ $p=1$
> $T(x)=\ ...\ =\Theta(xlnx)$

### Solving linear recurrances with annihilators
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
==Annihilator==: nontrivial operator transforming function to 0, every polinomial/exponential function has a unique minimal annihilator

| Operator                   | Function annihilated               |
| -------------------------- | ---------------------------------- |
| $E-a$                      | $\alpha*a^n$                       |
| $(E-a_0)(E-a_1)...(E-a_k)$ | $\sum_{i=0}^k\alpha*a_i^n$         |

- $X$ annihilates $f$ $\implies$ $X$ annihilates $Ef$
- $X$ annihilates $f$ $\implies$ $X$ annihilates $\alpha f$ for any constant $\alpha$
- $X$ annihilates $f$ and $g$ $\implies$ $X$ annihilates $f\pm g$
- $X$ annihilates $f$ and $Y$ annihilates $g$ $\implies$ $XY$ annihilates $f\pm g$

==Annihilating recurrances==:
1. Write recurrance in operator form
2. Extract an annihilator for the recurrance
3. Factor the annihilator (if necessary and possible)
4. Extract the generic solution from the annihilator
5. Solve for coefficients using the base cases (if known)

> [!example] Example
> $\tau(n)=5\tau(n-1)\ ; \ \tau(0)=3$
> $\tau(n)-5\tau(n-1)=0$
> $\tau(n+1)-5\tau(n)=0$
> $E\tau-5\tau=0$
> $(E-5)\tau(n)$ $\rightarrow$ $\tau(n)=\alpha*5^n$ ... generic solution
> $\tau(0)=3 \implies 3=\alpha*5^0 \implies \alpha=3$ $\rightarrow$ $\tau(n)=3*5^n$