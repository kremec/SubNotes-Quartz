Watching the function growth based on selected parameter
Omitting multiplicative and additive constants
#### Asymptotical upper bound $O$
$g(n)$ is asymptotical upper bound for $f(n)$ (at most $n$ instructions)
$$
O(g(n))=\{f(n);\ \exists c,n_0>0,\ \forall n>n_0:\ 0\leq f(n)\leq c*g(n)\}
$$
$$
f(n)=O(g(n)) \iff \lim_{n\to\infty}\frac{|f(n)|}{g(n)}<\infty
$$
#### Asymptotical lower bound $\Omega$
$g(n)$ is asymptotical lower bound for $f(n)$ (at least $n$ instructions)
$$
\Omega(g(n))=\{f(n);\ \exists c,n_0>0,\ \forall n>n_0:\ 0\leq c*g(n)\leq f(n)\}
$$
#### Asymptotically tight bound $\Theta$
$g(n)$ is asymptotical tight bound for $f(n)$ (approximately $n$ instructions)
$$
\Theta(g(n))=\{f(n);\ \exists c_1,c_2,n_0>0,\ \forall n>n_0:\ 0\leq c_1*g(n)\leq f(n)\leq c_2*g(n)\}
$$
$$
f(n)=\Theta(g(n))\iff f(n)=O(g(n))\ \land\ f(n)= \Omega(g(n))
$$
#### Imprecise bounds $o$ and $\omega$
$o(g(n))$ is an imprecise upper bound for $f(n)$
$$
o(g(n))=\{f(n);\ \exists c,n_0>0,\ \forall n>n_0:\ 0\leq f(n)\lt c*g(n)\}
$$
$$
f(n)=o(g(n)) \iff \lim_{n\to\infty}\frac{f(n)}{g(n)}=0
$$

$\omega(g(n))$ is an imprecise lower bound for $f(n)$
$$
o(g(n))=\{f(n);\ \exists c,n_0>0,\ \forall n>n_0:\ 0\leq c*g(n)<f(n)\}
$$
$$
f(n)=o(g(n)) \iff \lim_{n\to\infty}\frac{f(n)}{g(n)}=\infty
$$
### Properties of asymptotic bounds
Transitivity:
$$
\begin{aligned}
f(n)=\Theta(g(n))\ \land\ g(n)=\Theta(h(n)) &\implies f(n)=\Theta(h(n)) \\
f(n)=O(g(n))\ \land\ g(n)=O(h(n)) &\implies f(n)=O(h(n)) \\
f(n)=\Omega(g(n))\ \land\ g(n)=\Omega(h(n)) &\implies f(n)=\Omega(h(n)) \\
f(n)=o(g(n))\ \land\ g(n)=o(h(n)) &\implies f(n)=o(h(n)) \\
f(n)=\omega(g(n))\ \land\ g(n)=\omega(h(n)) &\implies f(n)=\omega(h(n))
\end{aligned}
$$
Reflexivity:
$$
\begin{aligned}
f(n)&=\Theta(f(n))\\
f(n)&=O(f(n))\\
f(n)&=\Omega(f(n))
\end{aligned}
$$
Symmetry:
$$
f(n)=\Theta(g(n))\iff g(n)=\Theta(f(n))
$$
Transpose symmetry:
$$
\begin{aligned}
f(n)=O(g(n))&\iff g(n)=\Omega(f(n))\\
f(n)=o(g(n))&\iff g(n)=\omega(f(n))
\end{aligned}
$$
$f(n)$ and $g(n)$ are not always in relation - either with $\Theta$/$O$/$\Omega$
<br><br><br>
### Analysis of algorithms
Watching algorithm's complexity through resource requirements:
- number of operations - time
- memory consumption
- network accesses

Random-Access Machine: abstract machine for approximating hardware
- uniprocessor, random access to memory locations
- constant time for most operations, numbers take limited amount of memory
- no parallelism, memory hierarchies (caches)

In most cases:
- only worst and average cases are important
- only the fastest growing (asymptotically important) terms are important
  ![[Computational complexity-Image-1.png|400]]