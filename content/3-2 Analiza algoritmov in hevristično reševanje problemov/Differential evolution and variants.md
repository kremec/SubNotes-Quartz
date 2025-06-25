Genetic algorithms: better in discrete spaces
Differential evolution: better in continual (eg. numerical) space, for discrete problems with rounding / limits / penalization of values

Metaheuristic algorithm with individuals represented as vectors, distributed over search space, over time they converge to the same solution

Algorithm:
1. Generate population of agents
2. While not satisfied:
	1. Compute fitness of agents
	2. Select reproduction candidates using fitness
	3. Create new agents by combining candidates
	4. Replace old agents with new ones
#### 1. Mutation
Generate ==trial vectors== - mutation step size represented by difference between individuals
Distance and direction information from current population guide search process:
- differences are large in beginning $\rightarrow$ bigger step size (exploring)
- differences are smaller towards the end $\rightarrow$ smaller step size (exploiting)
$$
u_i=x_{r1}+F(x_{r2}-x_{r3})
$$
#### 2. Crossover
Generate ==offspring==, the better one (parent or child) survives, $J$ ... crossover scheme
   $$
   \begin{aligned} x_{ij}^{'} = \begin{cases} u_{ij}(t)\ &...\ if\ j\in J \\ x_{ij}(t)\ &...\ otherwise \end{cases}\end{aligned}
   $$
### Control parameters
==Scaling vector F==: smaller $F$ $\rightarrow$ smaller step size (exploit / maintain diverstiy)
==Recombination/crossover probability CR==: higher $CR$ $\rightarrow$ more variation in new populations (faster convergence / search robustness)
==Population size==: based on number of dimensions
### Notation DE/x/y/z
==x ... vector to be mutated==:
- ==rand==: randomly chosen from population
- ==best==: best from current population
- ==current-to-best==: linear combination of current and best
- ==pbest==: randomly chosen from the best

==y ... number of difference vectors used==
==z ... crossover scheme==:
- ==bin==: change each dimension independently from others
- ==exp==: change connected sequence of dimensions
- ==arithmetic recombination==
### (L-)SHADE
Idea: record history of successful parameters and sample from it for future generations
==SHADE== ... DE/current-to-best/1/bin with archive and adaptive parameters $F$ and $CR$
- archive includes points which were replaced by trial points, maximum size adjusted each generation
$$
u_i=x_i+F(x_{pbest}-x_i)+F(x_{r1}-x_{r2})
$$
- $x_{pbest}$ ... randomly chosen from $p*100\%$ of best points of population
- $x_{r1},x_{r2}$ ... randomly chosen from population and archive

==L-SHADE== ... SHADE with linear reduction of population size over generations $\rightarrow$ limit maximal allowed number of fitness calls