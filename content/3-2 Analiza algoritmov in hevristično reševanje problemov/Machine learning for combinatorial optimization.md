Inputs $\rightarrow$ $ML(problem,parameters)$ $\rightarrow$ outputs
Collect all data from all generations to predict the next best move
Variants:
- Supervized learning: training data from disired result examples
- Reinforcement learning: training data from penalties/rewards exploration (random moves to explore, then exploit)

### Embedding
Graph representation $\rightarrow$ numerical space vector (for each node/edge)
#### PageRank
Node (page) is important if many nodes (pages) point to it
Random walker walks along the graph, fitness on nodes based on number of visits
#### DeepWalk
Predicting neighboring words for randomly seelcted words - what is important for this word