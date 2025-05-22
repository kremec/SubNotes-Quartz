NP-complete (NPC) problems: no polynomial algorithms $\rightarrow$ approximate solution in polinomial time
==k-approimation algorithm==: the approximation is at most $k$-times worse than optimal solution
### Performance ratio
==Approximation ratio==: ratio between cost of approximate ($C$) and optimal ($C^*$) solution
$$
\rho=max(\frac{C}{C^*}, \frac{C^*}{C})
$$
Approximate algorithm returns a solution no more than $\rho$ times worse than the optimal solution
### Vertex cover
==Vertex cover==: smallest set of vertices that cover all edges of the graph
Approximation algorithm: while the condition is not satisfied, choose a random edge and put it's vertices in the solution set $\rightarrow$ $|C|\leq 2*|C^*|$
### Travelling salesman problem (TSP) & Hamiltonian graph problem
There is no $\rho$-approximation algorithm for any constant $\rho$ for general TSP, unless P=NP
If we assume triangular inequality between costs, 2-approximation algorithm exists
### Satisfiability problems
All following prolems are NP-hard ($\in NPC$):
- CSAT: digital circuit with gates, find input that produces output of all logical ones
- FSAT: logical formula, find assignment of logical variables so that result is logical one
- 3CNF-SAT: conjunctive normal form formula with 3 dejunctions, each of 3 conjunctions, find assignment of logical variables so that result is logical one
  Approximation algorithm: randomly, independently assign each variable with equal chance of it being a $0$ or a $1$ $\rightarrow$ $\frac87$-approximation algorithm