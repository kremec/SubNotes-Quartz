Problem representation:
- different ==problem states==: $S_0$ ... starting state, $S_F$ ... set of final states
- ==search space==: graph of states, reachable in a final number of steps - $S=\{S;\ S_0\rightarrow^* S\}$

==Neighbourhood function==: step transition between neighbouring states, can be infinite possible connections - $N(S)=\{S';\ S\rightarrow S'\}$
==Quality function==: quality of a state as an optimization parameter $q(S)$ ... $q:S\rightarrow\mathbb{R}$
- Global optimum: $S_{best}=arg\ min_{s\in S}\ q(S)$ / $S_{best}=arg\ max_{s\in S}\ q(S)$ ... returns argument, not value
- Local optimum: no better neighbour - $S_{local}=\{S;\ \forall S\rightarrow S'\ : \ q(S)\leq q(S')\}$
### Local search
Algorithm:
- random starting state/solution $\rightarrow$ optimize by choosing best neighbour $\rightarrow$ (repeat)
- repeat algorithm with different starting solutions and return the overall best solution

Complexity of specific algorithm is determined by complexity of transformation (getting neighbours)
Problem: low probability of finding global extreme (optimum)
#### Gradient descent
Efficient algorithm for derivative functions: maximization / minimization: move in the direction $\nabla f(x)$ / $-\nabla f(x)$
$$
\nabla f(x)=(\frac{\partial f}{\partial x_1},\ ...,\ \frac{\partial f}{\partial x_n})
$$
Step size: parameter of how fast we move (problem: find better optimums or overstep into some local optimum)
#### Metropolis algorithm
Generalization of greedy LS:
- better neighbour exists $\rightarrow$ move to it
- otherwise $\rightarrow$ choose random neighbours and move (better neighbours with larger probability)

==Simulated annealing==: lower temperature/acceptance over time: $T'=\lambda T$ (typically $\lambda=0,95$)
- Over time $T$ comes close to $0$ $\rightarrow$ stochastic search turns into deterministic LS

Larger temperature $\rightarrow$ larger probability for acceptance of worse neighbour
Slower decreasing: searching larger portion of search space $\rightarrow$ better probability of finding global optimum, but takes more time
### Neighbourhood selection
Until now: 1-flip neighbourhood
Considering neighbourhood selection ways:
- large enough not to stop too fast in a local extreme
- small enough not to be too computationally expensive

==K-L heuristics/neighbourhood==: getting neighbourhood partitions - $(A,B)$ such that $A\cap B=\emptyset$ and $A\cup B=V$:
- Start with solution $(A,B)$
- Phase 1: Flip the single best node (that maximizes new solution $(A_1, B_1)$, even if solution is lower than current one) and mark it
- Phase k: We have partitions $(A_{k-1}, B_{k-1})$ and $k-1$ marked nodes, repeating as above
- Phase n: All nodes are marked, final solution is $(A_n, B_n)=(B,A)=(A,B)$

K-L neighborhoods are all the partitions from all phases - $(A_1,B_1),\ (A_2,B_2),\ ...,\ (A_{n-1},B_{n-1})$
### Best response dynamic
Each agent searches for best solution for himself
==Nash equilibrium==: no agent has initiative to change its configuration (stable state)
- There can be multiple possible Nash equilibriums

==Social choice==: configuration that minimizes the total cost of agents
- Social choice can be unstable, so it's not always achieved

Total possible cost of Nash equilibrium selfishness compared to social choice is at max $ln(k)$ instead of $1+\epsilon$