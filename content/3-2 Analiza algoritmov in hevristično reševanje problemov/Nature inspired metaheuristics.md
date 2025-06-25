Population-based algorithms: randomly selected search agents explore different candidate solutions
- interaction among individuals $\rightarrow$ wider knowledge about solution space
- diversity of population $\rightarrow$ efficiently explore search space, overcome local optima

General schema:
- starting population of solutions
- iteratively update current population by modifying some of its properties and perform selection
### Evolution-based methods
#### Evolution strategies (ES)
Two parents: modification of each dimension separately, select whichever is better among parent and child
Several parents: each dimension chosen randomly from one of parents and then mutated
#### Genetic algorithms (GA)
Genome encoding with fixed-length representation, modifications with crossover and mutation
#### Genetic programming (GP)
Variable-length representation of evolution of programs:
- initial population of computer programs as templates
- execute each program to assign a fitness value and run selection
- generate new population of computer programs by copying best / mutation / crossover over existing programs
#### Differential evolution
### Swarm-based methods
Simulate collective behavior of animal groups
#### Particle swarm optimization (PSO)
#### Ant colony optimization (ACO)
#### Artificial bee colony (ABC)
Mimicking finding optimal food sources in search space, amount of food representing fitness function
3 types of bees:
- ==Employed bees==: explore surroundings of known food sources, share information with rest of colony
- ==Onlooker bees==: randomly choose existing location with probability corresponding to its fitness
- ==Scout bees==: explore whole terrain for new food sources randomly if current food sources abandoned
#### Firefly algorithm
Mimicking fireflies attracting each other by light
Initially fireflies positioned randomly, each iteration each firefly jumps towards every other firefly based on attractiveness $\beta$:
$$
\beta_{ij}=\begin{cases} \beta_{0j}*e^{-\gamma* r_{ij}^2} &;\ f(x_i)>f(x_j) \\ 0 &;\ otherwise \end{cases}
$$
- $\gamma$ ... light absorption coefficient - pull diminishes with distance to not explore the same best position

Bad fireflies get pulled in all directions $\rightarrow$ explore
Good fireflies get pulled much less $\rightarrow$ exploit
#### Cuckoo search
Mimicking cuckoos secretly laying eggs in host nests of other birds, which may toss out these eggs or let new cuckoos hatch
Solutions as host nests, new candidate solutions are generated around randomly selected host nests by applying a random walk with Levi's noise
In each iteration, a fraction of worst nests are abandoned and replaced with newly generated ones
<br>
#### Crow search algorithm
Mimicking crows hiding excess food at different locations, and following other crows to their hiding places to steal
Initial population of crows with memories of best positions so far
2 movement possibilities:
- following a randomly chosen crow to its hiding place
- being tricked into moving into a random position
#### Grey wolf optimizer
Mimicking hunting and hierarchical behaviors of a pack of wolves, lower ranked wolves obeying higher ranked wolves during hunting, encircling its pray
Lower ranked wolves of population move towards higher ranked ones, based on hierarchy of their solution valuations
### Physics-based methods
Emulating laws of physics
#### Simulated annealing
#### Gravitational search
#### Electromagnetism-like mechanism
#### States of matter search
### Human-based methods
Inspiration from humans' behavior
#### Firework algorithm
Intensification of search in promising directions (of sparks from fireworks set of at best previous locations)
#### Artificial immune systems
Mimick methods of separation of self and non-self
Generate set of strings that represent self, and detectors that recognise complement of self and classify new data
#### Harmony search
#### Imperialistic competitive search