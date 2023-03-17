![[reducibility_summary.png]]
How do we prove that a problem is [[NP complete  | NP Completeness]]?
Informally, a problem X can be reduced to another problem Y if any instance of X can be easily modelled as an instance of Y, and the solution to the latter provides a solution to the former and vice versa.

Intuitively, if X reduces to Y, X is "no harder" than Y or Y is at least as hard as X.

The maximum flow problem can be encoded as a linear programming problem. Thus, the maximum flow problem is no harder than the linear programming problem.
$ax + b = 0$ can be encoded as $0 \cdot x^2 + ax + b = 0$, and this solving a linear equation is no harder than solving a quadratic equation.

![[reducibility_1.png]]
![[reducibility_2.png]]
![[reducibility_ice_1.png]]
a) false
b) true
c) 

## NP-Completeness
Given one NP-complete problem X, we can prove many interesting problems are NP-Complete using reduction, i.e., by showing a reduction from X to the problem.

### Example
All of the following problems are proven to be NP-complete through reduction based on one NP-complete problem, i.e., the SAT problem.
- 3 Colouring
- Subset Sum
- Knapsack
- Vertex Cover
- Clique
- Travelling Salesman

## SAT
Given a Boolean formula with n Boolean variables, determine whether there is an assignment such that the formula is TRUE.

One of the first problems to be proven NP-Complete. Cook's Theorem: SAT is NP-Complete.
Proven by the first principle (i.e., showing that it is as hard as any NP problem); very difficult.
![[sat_problem.png]]

## 3SAT
### Conjunctive Normal Form (CNF)
A Boolean formula is in CNF, if it is an AND of clauses, each of which is an OR of literals (i.e., a Boolean variable or its negation).

A Boolean formula is in 3-CNF if each of its clauses has exactly 3 distinct literals.
### The problem
Given a 3-CNF formula, is it satisfiable?
![[3sat_1.png]]
![[3sat_2.png]]
## Clique Problem
Is it NP?
Can you check whether it is a clique in polynomial time? Yes
Is it NP-hard?
Show that 3SAT $\leq_p$ Clique, i.e., transform 3SAT formula into a graph, for which a clique of size k exist if the 3SAT formula is satisfiable.
![[clique_problem_1.png]]
![[clique_problem_2.png]]
![[clique_problem_3.png]]
## Exercise
Can you show that the 3SAT problem is NP-complete based on the fact that the SAT problem is NP-complete.

## Vertex-Cover problem
is it NP? Yes
Is it NP-hard?
![[vertex_cover_proof_1.png]]
![[vertex_cover_proof_2.png]]
![[vertex_cover_proof_3.png]]
![[vertex_cover_proof_4.png]]
## NP-Complete Family
![[np_complete_family.png]]
![[karp_np_complete.png]]
![[np_complete_real_life.png]]

## Coping with NP-Completeness
![[solving_np_complete_1.png]]
![[solving_np_complete_2.png]]
![[CS202/images/solving_np_complete_3.png]]
![[solving_np_complete_3 1.png]]
![[solving_np_complete_4.png]]
### Vertex-Cover Example
![[vertex_cover_solving.png]]
![[vertex_cover_solving_heuristics.png]]
## Exercise
Prove that the travelling salesman problem (whether there exists a solution shorter than K) is NP-complete

In order to prove the Travelling Salesman Problem is NP-Hard, we will have to reduce a known NP-Hard problem to this problem. We will carry out a reduction from the Hamiltonian Cycle problem to the Travelling Salesman problem.  
Every instance of the Hamiltonian Cycle problem consists of a graph $G =(V, E)$ as the input can be converted to a Travelling Salesman problem consisting of graph $G’ = (V’, E’)$ and the maximum cost, $K$. We will construct the graph $G’$ in the following way:  
For all the edges e belonging to $E$, add the cost of edge $c(e)=1$. Connect the remaining edges, $e’$ belonging to $E’$, that are not present in the original graph $G$, each with a cost $c(e’)= 2$.  
And, set $K = N$.  
The new graph $G’$ can be constructed in polynomial time by just converting $G$ to a complete graph $G’$ and adding corresponding costs. This reduction can be proved by the following two claims:

-   Let us assume that the graph $G$ contains a Hamiltonian Cycle, traversing all the vertices $V$ of the graph. Now, these vertices form a TSP with $cost = N$ Since it uses all the edges of the original graph having cost $c(e)=1$. And, since it is a cycle, therefore, it returns back to the original vertex.
-   We assume that the graph $G’$ contains a TSP with cost, $K = N$. The TSP traverses all the vertices of the graph returning to the original vertex. Now since none of the vertices are excluded from the graph and the cost sums to n, therefore, necessarily it uses all the edges of the graph present in $E$, with cost 1, hence forming a [hamiltonian cycle](https://www.geeksforgeeks.org/hamiltonian-cycle-backtracking-6/) with the graph $G$.
Thus we can say that the graph $G’$ contains a TSP if graph $G$ contains Hamiltonian Cycle. Therefore, any instance of the Travelling salesman problem can be reduced to an instance of the hamiltonian cycle problem. Thus, the TSP is NP-Hard.