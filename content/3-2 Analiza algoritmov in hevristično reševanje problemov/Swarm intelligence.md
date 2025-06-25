==Swarm intelligence==: collective behavior of decentralized self-organized systems, made up of simple agents following simple rules
- global control is hard to define (larger systems lead to more errors)
- robust and relatively simple to use
### Swarming - boids
Rules:
1. ==Collision avoidance==: avoid collision with neighbors
   ![[Swarm intelligence-Image-1.png|200]]
2. ==Velocity matching==: match the velocity of neighbors
   ![[Swarm intelligence-Image-2.png|200]]
3. ==Flock centering==: stay near neighbors
   ![[Swarm intelligence-Image-3.png|200]]
### Ant colony optimization (ACO)
Metaheuristic abstraction of a (probabilistic) graph construction using heuristic information of pheromone trails of ant colonies
Individual agents (ants) deposit more pheromone along shorter paths to goal (as they pass it quicker and because of that more times) than other possibly longer paths
- Agents still randomly choose one path of many (with probability based on pheromone density)
- Pheromone evaporation ensures new / frequently used paths overshadow older / less used ones
#### Generic ACO
Algorithm:
1. Initialize pheromones
2. For each ant, while stopping criteria (eg. leaderboard stagnation, max iterations, ...) not satisfied:
	1. Select route (using pheromones and path cost)
	2. Apply local optimization
	3. Update pheromones - enforcement and evaporation
3. Return best solution

Pheromone updates:
$$
\begin{aligned} \tau_{ij}&=(1-\rho)\tau_{ij}+\Delta\tau_{ij} \\ \Delta\tau_{ij}&= \begin{cases} \frac{1}{C_{ij}}\ &...\ \text{ant takes edge i-j} \\ 0\ &...\ otherwise \end{cases}\end{aligned}
$$
- $\tau_{ij}$ ... amount of pheromones on edge $i-j$
- $\Delta\tau_{ij}$ ... newly added pheromones on edge $i-j$
- $\rho$ ... speed of evaporation
- $C_{ij}$ ... cost of edge $i-j$

Pros: greedy heuristic with distributed computation $\rightarrow$ rapid discovery of good solutions, avoiding premature convergence
Cons: possible slow convergence with no outside guidance towards good solutions
<br><br>
### Particle swarm optimization (PSO)
Population-based stochastic optimization technique of optimal solution search with inspiration of swarms of insects, schools of fish, ...

Individuals strive to improve themselves by learning from actions/behaviors of themselves and neighbors
Only one operation calculation - ==velocity==: vector of position change
$$
\begin{align}\vec{v+1}&=x(t+1)-x(t) \\ x(t+1)&=x(t)+\alpha\vec v+\beta(x^*-x(t))+\gamma(x^+-x(t))+\delta(x^!-x(t)) \end{align}
$$
- $x$ ... particle's location
- $x^+$ ... best neighbor's location
- $x^*$ ... best historical location
- $x^!$ ... best global location
- $\alpha$ ... proportion of current velocity
- $\beta$ ... proportion of best historical location: too large $\rightarrow$ swarm of greedy searchers without group dynamics
- $\gamma$ ... proportion of best neighbor's location: larger $\rightarrow$ emphasise globality / smaller $\rightarrow$ emphasise local information
- $\delta$ ... proportion of best global location: too large $\rightarrow$ single greeedy search instead of several local searches

Algorithm:
1. Compute fitness for each particle, update $x^+$, $x^*$ and $x^!$
2. Update particle's representation: velocity with added random noise
3. Move particle in direction of velocity

Pros: simple implementation (no derivatives) and easy parallelization
Cons: fast premature convergence and slow convergence in refined search space - weak local search ability