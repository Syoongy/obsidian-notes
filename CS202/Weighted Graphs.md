These graphs are not homogenous and have edges that are of differing importance. It is essentially a graph where a weight is assigned to each edge.

## Applications
- Road networks
- Supply chain networks
- Social networks
- Recommender Systems

----------------------------
# Minimum Spanning Tree
## Problem
Given a weighted undirected graph, how to build a minimum spanning tree (MST) or minimum weight spanning tree, i.e., a subset of the edges that connects all the vertices together, without any cycles and with the minimum possible total edge weight.
![[mst_example_1.png]]
### Kruskal's Algorithm
1. Sort edges by their weights in ascending order
2. Repeat until failure
	- Add the minimum edge into the spanning tree if the two endpoints are not connected
![[mst_kruskal_1.png]]
#### Complexity
![[mst_kruskal_2.png]]
#### Implementation
![[mst_kruskal_3.png]]
## Prim's Algorithm
1. Start with one vertex
2. Repeat until failure
	- Add the minimum edge that connects one vertex in the tree and one not yet in the tree
![[mst_prim_1.png]]
#### Implementation
![[mst_prim_2.png]]

They might not always generate the same trees due to the non-determinism of the algorithms
They generate the same MST if and only if they have the same ordering.
## Generic MST Algorithm
The generic algorithm: Add the minimum edge one by one.

Given a graph $G = (V, E)$, and suppose $A$ is the current set of edges selected.
Let $V_A$ be the set of coverted vertex, i.e
$$V_A = \cup \{u,v | (u,v) \in A\}$$
Let $S$ be a superset of $V_A$, i.e. $V_A \subseteq S \subseteq V$, and $e$ is the edge with minimum weight among those linking $S$ to $V-S$.
Add edge $e$ to $A$ until failure.
![[mst_generic_1.png]]
### Correctness
![[mst_generic_2.png]]![[mst_ice_1.png]]
To solve this, we can implement an algorithm `union_find`
![[mst_union_find_1.png]]
![[mst_union_find_2.png]]
![[mst_union_find_3.png]]
![[mst_ice_2.png]]

--------------------------
## Shortest Path
### Problem
Given two vertices $u, v$ in a graph, the shortest path problem is to find a path form $p$ from $u$ to $v$. When $u$ is given, it is single source shortest paths. When nethier $u$ nor $v$ are given, all-pairs shortest paths.
### Applications
- Routing
	- Driving
	- Transit
- IP/Server routing
- Social Network Recommendations

### Dijkstra's Algorithm
![[mst_dijkstra_1.png]]
![[mst_dijkstra_2.png]]
![[mst_dijkstra_3.png]]
![[mst_dijkstra_4.png]]
#### Implementation
![[mst_dijkstra_5.png]]
#### Correctness
Correct for graphs with non-negative edges
#### Complexity
$\Theta(V+E\times logV)$

### Bellman-Ford Algorithm
Single source shortest path algorithm for directed graphs where negative edge weights are allowed. It also utilises edge relaxations.
![[mst_bellman_ford_1.png]]
![[mst_bellman_ford_2.png]]
![[mst_bellman_ford_3.png]]
![[mst_ice_4.png]]
We need 3 iterations. If we do not stop when a negative cycle is detected, it can loop infinitely.

### Floyd-Warshall Algorithm
![[mst_floyd_warshall_1.png]]
#### Implementation
![[mst_floyd_warshall_2.png]]
![[mst_floyd_warshall_3.png]]
![[mst_floyd_warshall_4.png]]
![[mst_floyd_warshall_5.png]]
![[mst_floyd_warshall_6.png]]
![[mst_floyd_warshall_7.png]]
![[mst_ice_5.png]]