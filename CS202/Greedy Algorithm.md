## Applications
### Scheduling
- Activity Selection
- Scheduling on a single processor
### Graph Algorithms
- Minimum Spanning Trees
- Djikstra's Algorithm
### Combinatorial Optimisation Problems
- Fractional Knapsack
- Travelling Salesman Approximation
- Self-covering Approximation

## Activity Selection Problem
![[activity_selection_1.png]]
### Real-world
- #### Tourism
	- Theme park itinerary planning
		- pass lets you go on rides
		- all rides start at different times
		- maximise "happiness"
	- Multi-day tour itinerary planning
	- Berth allocation
		- Allocation of berths to vessels
	- Event scheduling
		- Allocation of rooms to events
	- Workforce Scheduling
		- Allocation of employees to tasks
### Algorithms
![[activity_selection_2.png]]![[greedy_activity_selection.png]]
## When Does Greedy Work?
Two key points:
1) Problem exhibits **optimal substructure**
	An optimal solution to the entire problem contains optimal solutions to sub problems
2) Algorithm exhibits **greedy choice property**
	Locally optimal solution => globally optimal solution (i.e., greedy choice is always safe)
Optimal substructure + greedy choice establishes the **correctness and optimality** of the greedy algorithm

### Greedy choice property:
- Make the best choice at the moment
- Greedy choice: From a locally optimal solution $S_j$ to sub problem $Q_j$, a globally optimal solution $S_i$ to problem $Q_i$ can be constructed
- Proofs often use exchange argument
	- If there were a “better” solution for Qi that does not contain the greedy choice
	- We could exchange the greedy choice into the “better” solution to get an equally optimal solution, leads to a contradiction that the “better” solution is better.
![[greedy_choice_proof.png]]
## Exercise 3
![[greedy_exercise_22.png]]
### Can you use exchange argument to prove why it is always optimal to process customers with the shortest service time?

## Fractional Knapsack Problem
### Original Problem
- There are n items, where the $i^{th}$ item worth $v_i$ dollars and weighs $w_i$ kg
- Knapsack carries at most W kg
- Question: What items should you take to maximise the profit?
### 0-1 Knapsack problem:
- "0-1" since each item must be take or left in entirety
### Fractional
- Can take fractions of items
- Can be solved by a greedy algorithm
### Why can't we apply the greedy algorithm to solve the first 2 knapsack problems?
For 0-1 knapsack problem consider the following example.
	```
```
C = 4, W = [1,2,2,3]
```
## Exercise 4
![[greedy_exercise_25.png]]

## Data Compression Problem
In the past, data storage space was small, and communication speed was low. Thus, data compression was needed.
Nowadays, data storage space is large, and data transfer rate is high. However, data compression is still needed as bigger files are stored or transferred.
![[data_compression_1.png]]
### Code Tree
![[data_compression_code_tree.png]]
#### Prefix Code
![[data_compression_prefix_code.png]]
#### Optimal Coding
![[data_compression_optimal_coding.png]]
### Huffman Codes
![[huffman_code_1.png]]
```Python
n = len(heap)
heapq.heapify(heap)
for _ in range(n-1):
    lval, lnode = heapq.heappop(heap)
    rval, rnode = heapq.heappop(heap)
    nnode = Node(lnode.value + rnode.value,
                 lval + rval, lnode, rnode)
    lnode.parent, rnode.parent = nnode, nnode
    heapq.heappush(heap, (lval + rval, nnode))
_, root = heapq.heappop(heap)
root.traverse('')
```
![[huffman_code_2.png]]
#### Analysis
##### Efficiency
Using heap, the time complexity is $O(nlogn)$
##### Correctness
1. Optimal substructure
	![[huffman_code_optimal_substructure.png]]
2. Greedy choice property
	- Cost of tree is cost of all mergers
	- Greedy choice is merger of least cost i.e., lowest frequency character at the time
	![[huffman_code_greedy_choice.png]]