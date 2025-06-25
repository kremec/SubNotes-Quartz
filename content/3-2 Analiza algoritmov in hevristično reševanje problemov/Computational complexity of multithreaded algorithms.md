### Multi-core architecture
![[Computational complexity of multithreaded algorithms-Image-1.png|300]]
Possible problems:
- ==deadlocks== (happen under Coffman conditions): processes wait for each other
- ==livelock==: processes loop in useless work
- ==starvation==: processes don't get to use some resource
- ==race conditions==: operations must be done in proper sequence
### Race conditions
Leading to non-deterministic results
Solution - low-level synchronization mechanisms:
- ==monitor==: ability of waiting/blocking based on condition
- ==semaphore==: counting variable controlling access to resource
- ==atomic operations==: program operations that cannot be preemptied
### Dynamic threads
New constructs: Parallel, Spawn, Sync

## Computational complexity analysis of multithreaded model
Assuming constant time for thread spawning and scheduling
- complexity (total time) ~ ==span==: critical/longest path in execution graph
- work (time of parallel threads) ~ $\sum$ of all calls

$P$ ... number of processors
$T_P$ ... time using $P$ processors ($T_1$ ... time of sequential processing, $T_{\infty}$ ... time using unlimited number of processors)
$S$ ... speedup, $S_p=\frac{T_1}{T_P}$ ... speedup using $P$ processors
![[Computational complexity of multithreaded algorithms-Image-2.png|500]]
(Same work, but only `max()` of times)
> [!example] Fibonnaci
>$T_1(n)=T_1(n-1)+T_1(n-2)+\Theta(1)$
>$T_{\infty}(n)=max(T_{\infty}(n-1), T_{\infty}(n-2))+\Theta(1)=T_{\infty}(n-1)+\Theta(1)=\Theta(n)$

<br><br><br><br><br><br>
### Limits of parallelization
#### Amdahl's law
Viewing single problem
$S=\frac{T_1}{T_P}$ ... speedup
$$
S=\frac{T_1}{f*\frac{T_1}{P}+(1-f)*T_1}=\frac1{\frac fP+(1-f)}
$$
$f$ ... proportion of parallelizable code
![[Computational complexity of multithreaded algorithms-Image-3.png|400]]
#### Gustafson's law
View more/larger problems with more available processors
$T_1=a+P*b$ ;  $a$ ... sequential time, $b$ ... parallel time
$\alpha$ ... sequential share of work, $1-\alpha$ ... share of parallel work
$$
S_p=\frac{T_1}{T_P}=\frac{a+Pb}{a+b}=\frac{a}{a+b}+\frac{Pb}{a+b}=\alpha+P(1-\alpha)=P-\alpha(P-1)
$$
![[Computational complexity of multithreaded algorithms-Image-4.png|500]]