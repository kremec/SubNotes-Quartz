==Metaheuristics==: procedure/heuristic designed to find a heuristic that may provide a sufficiently good solution to an optimization problem, guiding search process
Not problem-specific, but domain-specific knowledge can be used as heuristics
Classification of metaheuristics:
- nature / non-nature inspired
- population based / single point search
- dynamic / static objective function
- one / various neighborhood structures
- memory / memory-less methods

Goal is to efficiently explore search space in order to find (near) optimal solutions:
- ==intensification==: search neighborhood of good solutions thoroughly
- ==diversification==: broaden the search if no good solutions found in a while

==Exploit or explore dilemma==: generally explore more at first, then exploit found (partial) solutions (eg. simulated annealing - temperature)
Often incorporate mechanisms to avoid getting trapped in confined areas (local extremes) of the search space
### Tabu search
Supress (parts of) solutions by adding them to the tabu list
- prevents moves we don't want to do - cycling back into same local extremes

Design of tabu list:
- circular list (when filled we overwrite oldest entries)
- storing complete or parital solutions (moves / attributes of moves to prevent)

Usage:
- 1 tabu list: choosing best solution from neighborhoods that is not on tabu list
- multiple tabu lists: also allow ==inspiration== - better solution found by ignoring tabu
### Guided local search
Define and penalize properties of solutions which occur often in local extremes
- prevents local search to go into local extremes

$$
h(s)=g(s) + \lambda*\sum_{feature\ i}(p_i*I_i(s))
$$
- $h(s)$ ... auxiliary fitness function
- $g(s)$ ... fitness function
- $\lambda$ ... weight of punishments
- $p_i$ ... punishment of $i$-th property
- $I_i(s)$ ... indicator function of attribute $i$ and state $s$

Utility of features: effects of feature (part of solution) on actual solution (eg. edges of a graph, number of stops in a route, ...)
$$
util_i(s^*)=I_i(s^*)*\frac{c_i}{1+p_i}
$$
- $s^*$ ... local extreme
- $c_i$ ... cost
- $p_i$ ... current punishment for property $i$

This punishes property of local extreme with largest utility (by increasing $p_i$)
- if we punish property multiple times and bad state persists, release punishments
### Variable neighborhood search
Order neighborhoods by efficiency of computation and switch when reaching local extremes