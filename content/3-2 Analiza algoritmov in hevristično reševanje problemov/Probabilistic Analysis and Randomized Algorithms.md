Depends on probabilistic outcomes $\rightarrow$ we get expected bounds
Assumption: uniformly random input - ==randomization== to avoid "bad" input sequences
==Indicator random variable==: $I(A)=1$ if event $A$ occurs, otherwise $I(A)=0$
Sample space $S$, event $A$, $X_A=I(A)\implies E(X_A)=P(A)$

> [!example] Example
> Compute expected number of heads in $n$ tosses of a fair coin
> $X_i=I(the\ i-th\ flip\ resulted\ in\ heads)$ ... indicator random variable that H appeared in toss $i$
> $X=\sum_{i=1}^nX_i$ ... number of heads in $n$ flips
> $$
> E(X) = E(\sum_{i=1}^nX_i)=\sum_{i=1}^n*E(X_i)=\sum_{i=1}^n\frac12=\frac n2
> $$

### Pseudo-random numbers
Hardware RNG
Pseudo RNG: initialized with seed $\rightarrow$ get a large repeatable "random" number sequence
#### Linear congruential generators
$x_i=(a*x_{i-1}+c)\ mod\ p$ ; $p$ ... period
$u_i=\frac{x_i}m$ ; $m$ ... maximum
Simbple but bad - if current number is small, then the next will also be small
#### BBS
$x_i=x_{i-1}^2\ mod\ m$ ; $p$,$q$ ... large prime numbers, $m=pq$
If you find the primes you can reverse engineer generation (only on quantum computers in polynomial time)