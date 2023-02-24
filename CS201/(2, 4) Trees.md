# Definition
## Size property
Every internal node has at most 4 children
- 2-node has 1 key and 2 children
- 3-node has 2 ordered keys and 3 children
- 4-node has 3 ordered keys and 4 children
## Depth property
All external nodes have the same depth

## Height with $n$ nodes
Will have $(n+1)$ nodes where each external node represents a range of values not captured by internal nodes

If a tree has height $h$
- the minimum number of external nodes is $2^h$
- the maximum number of external nodes is $4^h$

The number of external nodes is bounded by:
### $$2^h <= n+1 <= 4^h$$
When taking logarithm base-2:
### $$h <= log_2(n+1) <= 2h$$
Therefore, $h$ is $\theta(logn)$

## Insertion
To insert a new key $k$:
- We will attempt to search for $k$ until external node $z$
- $w$ (internal node) is the parent of $z$
- We insert $k$ into $w$, and add a new child (external node) to the left of $z$

If $w$ was formerly a 2 or 3 node there will be no issue as size and depth properties are fulfilled

If $w$ was formerly a 4-node, it will overflow and become a 5-node. In such cases, we need to
- Perform a split
- Suppose $w$ now has 4 keys: $k_1, k_2, k_3, k_4$ and 5 children: $c_1, c_2, c_3, c_4, c_5$
- Insert $k_3$ into $u$, which is the parent of $w$ (create a new root if necessary)
- Add two new children to $u$:
	- $w'$ with $k_1, k_2$ and $c_1, c_2, c_3$
	- $w''$ with $k_4$ and $c_4, c_5$
- $u$ may overflow, in which case we split further as necessary

![[overflow_and_split.png]]
![[2_4_cascading_split.png]]

## Deletion
To delete an existing key $k$:
- Search for $k$ and delete it as in regular binary search tree
- May require replacement by another key
- We will eventually need to remove some key $k'$ (either $k$ itself or its inorder predecessor) from an internal node $w$ whose children are external nodes
- Remove $k'$ along with one of the children of $w$ (the corresponding external node)

If $w$ was formerly a 3 or 4 node, then no issue as both size and depth properties are fulfilled

If $w$ was formerly a 2-node, it underflows and becomes an empty node
- Case #1: an immediate sibling $s$ of $w$ is a 3 or 4 node
	- Perform a **transfer**: move a key from $s$ to $u$ (parent of $s$ and $w$) and a key from $u$ to $w$
- Case #2: $w$ has 1 sibling, or both siblings are 2-nodes
	- Perform a **fusion**: merge $w$ to $s$ into $w'$ and move a key from $u$ to $w'$
![[2_4_no_underflow.png]]
![[2_4_underflow_and_transfer.png]]
![[2_4_underflow_and_fusion.png]]
![[2_4_propogating_fusion.png]]
