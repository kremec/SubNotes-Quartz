==Genetic algorithms== sample solution space and guide search where probability of better solutions is larger using competition of agents
- Population size: large $\rightarrow$ slow computation, small $\rightarrow$ not enough agents (normally 20 - few thousand agents)
- Selection method - probability of performing crossover (normally ~$0.9$) / mutation (normally ~$0.1$)
- Stopping criteria (eg. number of generations, target fitness, availability of computational resources, ...)

Pros:
- faster searching of large search spaces with many local extremes, parallelization of population simulations
- easy algorithm after defining representation and fitness function
- no specialized methods (for given problem) / having just fitness information (cannot compute gradients)

Cons:
- randomized $\rightarrow$ not optimal, can still get stuck on local maxima with possible (over)specialization for local extremes
- non-accurate abstraction of real environment
#### Evolutionary program template
1. Generate population of agents
2. Loop while condition is not satisfied (eg. leaderboard updated for some time / ...)
	1. Compute fitness (quality) of agents (fitness must be fast-computable)
	2. Select candidates for reproduction using calculated fitness (with probability distribution)
	3. Create new agents by combining the candidates
	4. Replace old agents with new ones

![[Genetic algorithms and hybrids-Image-1.png|350]]
#### Gene representation
Define:
- ==data structure==: bit vector / numeric vector / string / tree
- ==crossover operation==: single point / multipoint
- ==mutuation operation==: single point / multipoint
- ==fitness function== determining agents to reproduce - keeping the good, but preventing premature convergence
![[Genetic algorithms and hybrids-Image-2.png|400]]

>[!example] Bit vector representation
>Crossover operation:
>- Exchange representations over random splitting point
>  Parents: [1 1 | 0 1], [1 0 | 1 0]
>  Children: [1 1 | 1 0], [1 0 | 0 1]
>
>Mutation operation:
>- Flip bits with random probability $p_m<0.1$ (larger $p_m$ leads to random search)
>  Parent: 0110
>  Child: 0010
>- ==Lamarckian mutation==: searching for locally best mutation
><br>

>[!example] Numeric vector representation
>Crossover operation:
>- Exchange representations over random splitting point
>  Parents: [1.2 | 3.4], [5.6 | 7.8]
>  Children: [1.2 | 7.8], [5.6 | 3.4]
>
>Linear crossover operation: $c=\alpha x+(1-\alpha)y$, $\alpha\in(0,1)$
>Example: $\alpha=0.75$, parents [5  1  2  10] and [2  8  4  5]
>Result of crossover: [3.75+0.5  0.75+2  1.5+1  7.5+1.25]
>Vartiation for $\alpha=$[0.5  0.25  0.75  0.5]: [2.5+1  0.25+6  ...]
>
>Mutation operation:
>- Replace random dimension with random number
>- Gaussian mutation: $c=x_i+N(0, \sigma)$
>- Differential evolution
><br>

>[!example] Tree representation
>Crossover operation:
>- Ordered crossover: choose random path slice, keep it as is and fill with other parent (replace duplicates with missing)
>  Parents: [1 9 2 | 4 6 5 7 | 8 3], [4 5 9 | 1 8 7 6 | 2 3]
>  Children: [2 3 9 | 4 6 5 7 | 1 8], [3 9 2 | 1 8 7 6 | 4 5]
>
>Mutation operation:
>- Switch $k$ nodes in path
><br>

==Neural networks==: Evolving neurons, weights and topology of neural network
#### Selection
==Multiobjective optimization problems==: fitness function with several parameters
- ==Pareto optimal solution==: no possible improvement of one criteria without getting worse on others
##### Proportional selection
Each agent has a probability of being selected based on fitness: $p_i=\frac{f_i}{\sum f_i}$
Choose slot with random generated number $\in(0,1)$
##### Rank proportional selection
Each agent is given a rank based on fitness and then a probability of being selected based on the rank: $p_i^r=\frac{r_i}{\sum r_i}$
##### Tournament selection
Randomly select $g$ ... size of tournament agents:
- the best among them wins tournament with probability $p$
- else the second best wins with probability $(1-p)p$
- else the third best wins with probability $(1-p)^2p$
##### Single tournament selection
Split the population into groups of size $g$
The best two win and reproduce, the children replace the worst two in a group
#### Replacement
Replacement of:
- all agents
- only worst ones
- ==elitism==: keeping the top agents of population - prevent losing good genes
- local elitism: children replace parents if they are better