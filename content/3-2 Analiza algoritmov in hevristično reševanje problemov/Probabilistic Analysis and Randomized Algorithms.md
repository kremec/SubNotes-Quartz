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
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
## Amortized analysis of computational complexity
### Aggregated analysis
Aggregate all possible functions
> [!example] Stack with multipop operation
> $n$ operations of `PUSH`, `POP` - worst case per operation: $\frac{n*\Theta(1)}{n}=\Theta(1)$
> $n$ operations of `PUSH`, `POP`, `MULTIPOP` - worst case per operation: $\frac{n*k}{n}=O(k)$
> $n-1$ operations of `PUSH`, then `MULTIPOP(n-1)` - worst case per operation: $\frac{2n-1}{n}=O(1)$
### Accounting method
Assessing worst-case upper bound for a series of $n$ operations
Amortized cost $c'_i$ $\geq$ actual cost $c_i$ $\implies$ $\sum_{i=1}^nc'_i \geq \sum_{i=1}^nc_i$
- found upper bound for amortized cost $\geq$ upper bound for actual cost

> [!example] Stack with multipop operation
> Each `PUSH`/`POP` costs 1 coin; if you put $2$ coins all push, all possible future pops are already paid for
> 
> | operation | actual cost |  amortized cost  |
| ---------- | --------- | --- |
| `PUSH`        | $1$    |  $2$  |
| `POP`      | $1$     |  $0$  |
| `MULTIPOP`      | $min(k,s)$     | $0$   |
> $n$ operations of `PUSH` - worst case: $\sum_{i=1}^nc'_i=\sum_{i=1}^n2=2n$
> Worst case per operation: $\frac{2n}n=2=O(1)$
### Potential method
Data structure $D$ has a "potential" $\Phi$ that pays for more expensive operation
- $D_i$ ... $D$ after operation $i$ applied to $D_{i-1}$
- $c'_i=\sum_{i=1}^nc_i+\Phi(D_n)-\Phi(D_{i-1})$ ... amortized cost

> [!example] Stack with multipop operation
> $\Phi$ ... number of elements on the stack
> - $\Phi(D_0)$ ... assume empty stack
> - $\Phi(D_i)$ ... number of elements on the stack after operation $i$
> 
> | operation | actual cost |  $\Delta\Phi$  | amortized cost |
| ---------- | --------- | --- | --- |
| `PUSH`        | $1$    |  $(num+1)-num=1$  | $1+1=2$    |
| `POP`      | $1$     |  $(num-1)-num=-1$  | $1-1=0$    |
| `MULTIPOP`      | $min(k,s)=k'$     | $(num-k')-num=-k'$   | $min(k,s)-k'=0$    |
>
> Worst sequence of $n$ operations: $\sum_{i=0}^nc'_i=\sum_{i=0}^n2=2n
> Worst case per operation: $\frac{2n}n=2=O(1)$
> 
