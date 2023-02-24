## Graph Representations
### Adjacency Matrices
For simple graphs with no self loops nor multi-edges between the same pair of nodes. The adjacency matrix is a (0,1) matrix with zeroes on its diagonal. Entry(i, j) is 1 if there is an edge from vertex i to vertex j, 0 otherwise.
![[adjacency_matrix.png]]
### Adjacency Lists
Each vertex is represented by a linked list, which are its neighbours
![[adjacency_list.png]]
## Depth-First Search (DFS)
- Explore deeper whenever possible
- Given a starting vertex $s$, explore all unexplored neighbours of the most recently discovered vertex
- Build one depth-first tree at a time, an edge $u$ -> $v$ represents $v$ is explored in the neighbourhood of $u$
- Build depth-first trees from other unexplored vertices to form a depth-first forest
![[dfs_1.png]]![[dfs_2.png]]
### Graph Searching
![[dfs_graph_searching.png]]
![[dfs_directed_tree.png]]
### Time Complexity
![[dfs_time_complexity.png]]
![[dfs_time_complexity_2.png]]
### Applications
1. Connected Components
2. Cycle Detection
3. Topological Sort
4. Strongly Connected Components

## Breadth-First Search(BFS)
- Explore the breadth of the frontier to discover every vertex reachable from $s$
- Build a single breadth-first tree rooted at $s$, an edge $u$ -> $v$ represents $v$ is enqueued into a list of candidates to be explored when searching the neighbourhood of $u$
- Build breadth-first trees from other unexplored vertices to form a breadth-first forest
![[bfs_example_1.png]]![[bfs_example_2.png]]
### Graph Searching
![[bfs_graph_searching.png]]
### Time Complexity
![[bfs_time_complexity_1.png]]![[bfs_time_comlexity_2.png]]

-------------------------
## Connected Components
![[connected_components.png]]
![[w6_exercise_3.png]]
1. Add a count everytime a new DFS is started on a "white" node. Same as DFS
2. Same as DFS

### In Directed Graphs
![[connected_components_directed_graphs.png]]

------------------------
## Cycle Detection
![[cycle_detection_1.png]]
An undirected graph is acyclic if a DFS has no back edges.
Proof:
If and undirected graph is acyclic, the graph is a forest, therefore all edges are tree edges. DFS is an undirected graph, classifies edges into either tree edges or back edges. If there is no back edge, all edges are tree edges and the graph is acyclic. This also applies to a directed graph.

-------------------------------
## Directed Acyclic Grapg (DAG) and Topological Ordering
![[dag_topological_ordering.png]]

-----------------------
## Strongly Connected Components
![[strongly_connected_components.png]]

--------
## Graph Transpose
![[graph_transpose.png]]

------------------
## Kosaraju's Algorithm
![[kosaraju_algorithm_1.png]]![[kosaraju_algorithm_2.png]]
![[kosaraju_algorithm_3.png]]
![[kosaraju_algorithm_4.png]]