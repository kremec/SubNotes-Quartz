Idea:
- ==divide== the problem into several (equal) parts
- (recursively) ==conquer/solve== each of the sub problems
- ==combine== sub problem solutions
### Recursive function analysis
==Recurrent equations==, proven by induction
### Analysis of divide and conquer algorithms
#### Substitution method
1. Guess the solution
2. Using induction find the constants
3. Prove solution validity with induction

> [!example] Example
> $T(n)=2T(\frac n2)+nlogn$
> Assume: $T(n)=O(nlogn)$
> Prove: $T(n)\leq c*nlogn \ \ ; \ c>0,\ n>n_0$
> Inductive assumption: $T(n)\leq c*2*\frac n2log\frac n2+n=\ ...\ =cn*logn-n(1-c)$
> Base case: $T(1)$ not, but $T(2)$ yes
#### Recursive tree
1. Draw recursive tree
2. Sum complexity level-wise and altogether
3. Prove solution validity with induction

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
$$
\begin{align}
f(n)=O(n^{log_ba-\epsilon}) &\implies T(n)=\Theta(n^{log_ba}) \\
f(n)=\Theta(n^{log_ba-\epsilon}) &\implies T(n)=\Theta(n^{log_ba}logn) \\
f(n)=\Omega(n^{log_ba+\epsilon}) &\implies T(n)=\Theta(f(n))
\end{align}
$$
    - Less leafs in recursion tree $\rightarrow$ peak dominates (1. rule)
    - More leafs in recursion tree $\rightarrow$ bottom dominates (3. rule)

> [!example] Example
> $T(n)=3T(\frac n4)+nlogn$
> $a=3$, $b=4$, $f(n)=nlogn$
> $n^{log_ba}=n^{log_43}\in(0,1)$
> - $nlogn\neq O(n^{log_43-\epsilon})$
> - $nlogn\neq\Theta(n^{log_43-\epsilon})$
> - $nlogn=\Omega(n^{log_43+\epsilon})$ $\rightarrow$ $T(n)=\Theta(nlogn)$
#### Akra-Bazzi theorem
1. Get all $a_i$, $b_i$ and $f(n)$ which must be polinomially limited
2. Calculate $p$ in $\sum a_i*(b_i)^p = 1$
3. Use it to determine the asymptotic bounds of $T(n)$:
$$
T(x)=\Theta(x^p(1+\int_1^x\frac{f(u)}{u^{p+1}}du))
$$

> [!example] Example
> $T(n)=T(\frac {3n}4)+T(\frac n4)+n$
> $a_1=1$, $b_1=\frac 34$, $a_2=1$, $b_2=\frac 14$, $f(n)=nlogn$
> $1*(\frac 34)^p+1*(\frac 14)^p=1$ $\rightarrow$ $p=1$
> $T(x)=\ ...\ =\Theta(xlnx)$