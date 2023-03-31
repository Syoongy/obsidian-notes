## Performance Measurement
What do we expect from a "good" approximation algorithm or heuristics?

It should be efficient, i.e., its complexity should be reasonable (e.g., polynomial). 
It should find a solution of good quality, i.e., the solution should not be far from the optimal solution.

### Performance Ratio
P: an NP-hard minimisation problem
A: A polynomial time algorithm to solve P
I: an instance I of P
A(I): The solution returned by A on instance I
OPT(I): The optimal solution on instance I
The performance ratio is defined as:
$$R_A(I)=A(I)/OPT(I)$$
An example would be the travelling salesman problem
A: nearest neighbour heuristics (i.e., travel to the nearest unvisited city next)

If the solution returned by A is 200, whereas the optimal solution is 100, the performance ratio is 2

### Worst case approximation ratio
This is defined by:
$$R_A=\max_IR_A(i)$$
i.e., the worst performance of A among all problem instances

### Performance guarantee for approximation algorithms
Algorithm A for P is an approximation algorithm if, for all instances, A returns a solution whose value is at most a give factor away from the value of the optimal solution

When looking at the [[Vertex-Cover Problem]],
![[vertex_cover_approximation.png]]
#### Theorem
$$R_{AVC}\leq2$$
Where AVC = approx-vertex-cover

#### Proof
```
Let C be the set returned by AVC. 

Let C* be the optimal vertex cover.

Let A be the set of edges selected. 

|A|≤ |C*| since C* covers all the edges in A and no two edges in A share a vertice. 

2|A|=|C| since every vertice is covered exactly once. 

Ergo: |C|≤ 2|C*|, implies |C|/|C*|≤ 2.
```

When looking at the travelling salesman algorithm, an approximation algorithm would look something like this:

```
The salesman starts at a random city and repeatedly visits the nearest city until all have been visited.

How do we quantify the performance of RNN?

The conclusion: RNN≤ ½(1+log2n) where n is the number of cities. 

Example: when n=10, RNN≤ 2.16; when n=1000, RNN≤ 5.48.
```

Can we find an approximate algorithm with a constant worst-case approximate rate?
Yes, if we assume triangle inequality, i.e., c(a,b) + c (b,c) ≥ c(a,c). Intuitively, it is always cheaper to go directly to city c (than transiting through b). However, the travel salesman problem with triangle inequality is still NP-hard.

To do this, we first have to understand the MST algorithm
1.  Select a root r; 
    
2.  Compute a minimum spanning tree T for G from root r;
    
3.  Let L be list of vertices visited in a pre-order walk of T;
    
4.  Return tour that visits the vertices in the order L;

![[tsp_mst_1.png]]
![[tsp_mst_2.png]]
![[CS202/images/tsp_mst_3.png]]
![[tsp_mst_3 1.png]]
#### Performance Guarantee
#### Theorem
$$R_{MST}\leq2$$
#### Proof
```
Let H* be the optimal tour.

Let w(MST) be the weight of the MST. 

w(MST) ≤ c(H*) (since deleting one edge from H* makes a spanning tree).

Given an MST, we can always have a tour of all the vertices with a full walk F, which visits every edge exactly twice. 

c(F) = 2*w(MST) ≤ 2*c(H*)

Delete those repeated vertices from F to obtain F’. 

Due to triangle inequality, we have c(F’) ≤ c(F) ≤ 2*c(H*).
```
#### The Good
Since we have $RMST\leq2$, we know for sure that if we apply the MST algorithm to solve the travel salesman problem (with triangle inequality), we won’t be more than 2 times worse off
#### The Bad
In practice, the MST algorithm usually does not produce the best practical choice for this problem

## Bin Packing Problem
Suppose that we are given a set of n objects, where the size si of the i-th object satisfies 0 < si < 1. We wish to pack all the objects into the minimum number of unit-size bins. 

Each bin can hold any subset of the objects whose total size does not exceed 1.
![[bin_packing_1.png]]

### Next fit packing algorithm
It keeps a current bin, which is initially empty.

When an item arrives, it checks whether the item fits into the current bin. 

If it fits, it is placed inside it.

Otherwise, the current bin is closed, a new bin is opened and the coming item is placed inside this new bin.
![[bin_packing_2.png]]
![[bin_packing_3.png]]
![[bin_packing_4.png]]

## Branch and Bound
Optimisation problem with an objective function min $f(x)$.
A divide and conquer algorithm, where a problem is branched into smaller and smaller subproblems. Each subproblem is solved separately, and hopefully used to bound the solution of other subproblems.
![[branch_bound_1.png]]
-   The most popular approach for solving combinatorial optimization problems.
    
-   Enumerate the entire solution space but only implicitly; hence they are called implicit enumeration algorithms.
    
-   A general-purpose solution framework which must be specialized for individual problems.
    
-   Running time grows exponentially with the problem size, but small to moderate size problems can be solved in reasonable time.

![[branch_bound_2.png]]
![[branch_bound_3.png]]
![[branch_bound_4.png]]
![[branch_bound_5.png]]
![[branch_bound_6.png]]
![[branch_bound_7.png]]
![[branch_bound_8.png]]
![[branch_bound_9.png]]
![[branch_bound_10.png]]
![[branch_bound_11.png]]
### Complexity Analysis
Worst case is still NP-complete. Average case complexity is likely much better dependent on problem instance distribution.
Effectiveness of this depends on:
- Branching rule
- Bounding function
- Search Strategy
Advanced decomposition methods:
- Langrangian Relaxation
- Dantzig-Wolfe Decomposition
- Bender's Decomposition

