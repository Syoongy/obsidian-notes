## Problem
$$max_{x\in S}f(x)$$
Where $S$ is the feasible solution space.
A heuristics or metaheuristics algorithm explores the feasible solution space partially guided by certain heuristics.

## The Intuitive Idea
Heuristics and metaheuristics algorithms do not guarantee to find an optimal solution (as opposed to exact algorithms) or to find solutions within certain worst-case approximation ratio (as opposed to approximation algorithms). 

However, they are usually designed to find a “reasonably good” solution quickly.

There are many heuristics/metaheuristics algorithms.

## Heuristics
Is often problem dependent (i.e. works for one problem only)

### Categories
#### Single solution metaheuristics
These methods are algorithms in which the search for the optimum is achieved by manipulating a single solution throughout the progression of the algorithm. (i.e. Hill climbing, simulated annealing)

#### Population-based heuristics
These methods maintain and improve multiple candidate solutions, often using population characteristics to guide the search. (i.e. Genetic algorithms, particle swarm optimisation)

## Metaheuristics
High-level problem-independent algorithmic framework that provides a set of guidelines and strategies to develop heuristic optimisation algorithms

---------------------------------
## Local Search (Hill Climbing)
![[local_search_1.png]]
![[local_search_2.png]]
![[local_search_3.png]]
![[local_search_4.png]]
![[local_search_5.png]]
![[local_search_6.png]]
![[local_search_7.png]]
![[local_search_8.png]]
![[local_search_9.png]]
### Vehicle Routing Problem
![[vehicle_routing_1.png]]

#### Using local search
![[local_search_10.png]]
![[local_search_11.png]]
![[local_search_12.png]]

---------------------
## Simulated Annealing
A stochastic variation of hill climbing in which inferior moves are allowed.

The probability of making an inferior move decreases with time.

Model after the physical process of annealing metals (cooling molten metal to solid minimal-energy state).

![[simulated_annealing_1.png]]
![[simulated_annealing_2.png]]
![[simulated_annealing_3.png]]