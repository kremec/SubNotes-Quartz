Genetic algorithms: better in discrete spaces
Differential evolution: better in numerical space (continual value problems)

Metaheuristic algorithm with no need for gradient, using crossover and mutation
Individuals represented as vectors
Distance and direction information from current population guide search process

Algorithm:
1. Generate population of agents
2. While not satisfied:
	1. Compute fitness of agents
	2. Select reproduction candidates using fitness
	3. Create new agents by combining candidates
	4. Replace old agents with new ones

New agent creation:
1. Generate ==trial vectors== with ==mutation==
   Mutation step size represented by difference between random individuals of current population:
	- differences are large in beginning $\rightarrow$ bigger step size (exploring)
	- differences are smaller towards the end $\rightarrow$ smaller step size (exploiting)
$$
u_i=x_{r1}+\beta(x_{r2}-x_{r3})
$$
2. Generate ==offspring== with ==crossover==
$$
\begin{aligned} x_{ij}^{'} = \begin{cases} u_{ij}(t)\ &...\ if\ j\in J \\ x_{ij}(t)\ &...\ otherwise \end{cases}\end{aligned}
$$
