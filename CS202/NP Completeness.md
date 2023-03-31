## Decision vs Optimisation Problems
### Optimisation
Goal is to find a feasible solution with the optimal (min/max) value, e.g. what is the maximal matching. Can be easily turned into decision problems. Theory of complexity technically does not apply here.

### Decision
Goal is to determine whether some statement is true or false (i.e. "yes/no" answers) e.g. whether there is a matching with size 4. "Easier" than corresponding optimisation problems. Theory of complexity applies here.

### Algorithm Complexity
What constitutes a reasonable complexity of an algorithm?
An algorithm has reasonable complexity (tractable), if the worse case complexity is $\theta(n^k)$ where n is the input size and k is a constant (i.e. polynomial time complexity). Examples of non polynomial time complexity $\theta(2^n), \theta(n^{log(n)}, \theta(n!))$

### P (Not Pius)
P is the class of problems solvable in polynomial time. (e.g. BFS, maximal flow problem)
#### Not in P
Some problems are clearly not solvable in polynomial time. (e.g. Turing's "Halting Problem" where we have to determine if a program (written in a Turing complete language) and an input to the program, whether the program will eventually halt when run with that input)


### NP
Class of problems that can be verified (checked) by a polynomial-time algorithm. An example of this would be a hamiltonian cycle of an undirected graph (simple cycle that contains every vertex). It is NP since verifying whether a given solution is a hamiltonian cycle is easy (i.e. polynomial time).
![[hamiltonian_cycle.png]]

[[Vertex-Cover Problem]]

## Graph Colouring Problem
Given a graph $G$ and integer $k$, can $G$ be coloured with at most $k$ colours such that no two adjacent vertices are of the same colour. It is NP since verifying any given solution is in polynomial time.
![[graph_colouring.png]]

## 3-Dimensional Matching Problem
Let $X, Y, Z$ be finite sets, and let $T$ be a subset of $X \times Y \times Z$. That is $T$ consists of triples $(x, y, z)$ such that $x \in X, y \in Y, z \in Z$. $M \subseteq T$ is a 3-dimensional matching if the following holds: For any 2 distinct triples $(x1, y1, z1) \in M$ and $(x2, y2, z3) \in M$, we have $x1 \ne x2, y1 \ne y2, and z1 \ne z2$. Is there a matching of size K? Can be verified in polynomial time.
![[3_dimensional_matching.png]]
![[3_dimesional_problem_2.png]]

## Travelling Salesman Problem
Optimisation version:
Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin city.
Decision version:
Is there a route that is shorter than K?

Can be verified in polynomial time

## P vs NP
P are problems that can be solved efficiently. Np are problems whose solution can be checked efficiently.

A problem that can be solved in polynomial time can be verified in polynomial. Thus, $P \subseteq NP$. Some problems are both P and NP, e.g., the sorting problem and the shortest path problem.

Is $NP \subseteq P$ or equivalently $NP = P$?
Can problems that can be checked efficiently be solved efficiently as well?
![[p_vs_np_1.png]]

## NP-Complete
Class of problems such that solving any of them using a polynomial time algorithm would prove $P=NP$ (Or proving that there is no polynomial time algorithm to solve any of them would prove $P \ne NP$).

Let $C$ be a complexity class (e.g. polynomial, and exponential). A set of problems $L$ is hard for $C$ if every problem in $C$ is polynomially transformable to $L$; $L$ is complete for $C$ if it is in $C$ and is hard for $C$.

No polynomial-time algorithm for NP-complete problems have been found so far.
No superpolynomial lower bound has been proved for any of the NP-Complete problems.

### Examples
- Longest path
- Knapsack
- Bottleneck travelling salesman
- Boolean satisfiability problem (SAT)
- ...

A problem $L$ is NP-hard if every problem in NP is polynomially transformable to $L$, i.e. $L$ is at least as hard as the hardest problems in NP

A problem $L$ is NP-complete if $L$ is NP and is NP-hard, i.e, a solution to $L$ can be verified in polynomial time and $L$ is the hardest among all NP problems

### P = NP?
If any NP-complete problem is in P, then $P = NP$. If any NP problem is not in P, then all NP-complete problems are not in P. Hence, $P \ne NP$.

![[p_vs_np_2.png]]
