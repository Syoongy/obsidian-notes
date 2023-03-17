![[dynamic_partitioning_1.png]]
- Compaction - OS needs to periodically shift the processes so that they are contiguous (time-consuming)
#### Process
Loaded into a partition of exactly the same size as the process
#### Fragmentation
External (Creation of "small holes")

## Placement Algorithms
### Best-fit
Chooses the block that is closest in size to the request
### First-fit
Begins to scan memory from the beginning and chooses the first available block that is large enough
### Next-fit
Begins to scan memory from the location of the last placement and chooses the next available block that is large enough
![[dynamic_partitioning_2.png]]
To implement the various placement algorithms discussed for dynamic partitioning, a list of the free blocks of memory must be kept. For each of the three methods (best-fit, first-fit, next-fit), what is the average length of the search? In other words, what is the average running time if there are N free blocks?
Best-fit: $\theta(N)$
First-fit: Probability of first free block is 1/2. Probability of second free block is 1/4
Probability of the i-th free block is $1/2^i$. Thus, the average length of search = $1/2 + 2/2^2 + 3/2^3 + \cdots + N/2^N + N-1$
On average is between 1 and 2
Next-fit

## Buddy System
Comprised of fixed and dynamic partitioning schemes
1. Space available for allocation is treated as a single block of size $2^u$
2. If a request of size $s$ such that $2^{u-1} < s \leq 2^u$ is made, the entire block is allocated
3. Otherwise, the block is split into two equal buddies of size $2^{u-1}$
4. Repeat steps 1-3 until the smallest size block is found
![[buddy_system_1.png]]
![[buddy_system_2.png]]
![[buddy_system_3.png]]
![[buddy_system_4.png]]