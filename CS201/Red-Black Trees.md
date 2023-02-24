# Definition
Balanced binary search trees with constant number of restructuring for each structural change. It is an implementation of a [[(2, 4) Trees |(2,4) Tree]]
## Properties
- **Root**: Will be black
- **External**: All external nodes are black
- **Red**: The children of a red node are black
- **Depth**: All external nodes have the same black depth (The number of proper ancestors that are black)
![[red_black_tree.png]]
For any red-black tree, we can turn it into a [[(2, 4) Trees|(2, 4) tree]] by merging every red node with its black parent
![[red_black_into_2_4.png]]
![[2_4_red_black_comparison.png]]

## Height with $n$ nodes
Let $T$ be a red-black tree of height $h$, containing $n$ nodes
- All external nodes have a common black depth of $d$

Let $T'$ be it's corresponding [[(2, 4) Trees|(2, 4) tree]] of height $h'$
- For a (2, 4) tree, $h' <= log_2(n_1)$

Due to the correspondence between red-black tree and (2, 4) tree:
- The black depth $d$ is equal to the [[(2, 4) Trees|(2, 4) tree]] tree height $h'$
- Therefore, $d <= log_2(n+1)$

Due to the red property, the height $h$ of a red-black tree is bounded by:
### $$h <= 2d$$
### $$h <= 2log_2(n+1)$$
Because a red-black tree is a binary tree:
### $$log_2(n+1) <= h$$
Hence, $h$ is $\theta(logn)$

## Insertion
It proceeds as a regular BST
- If inserted node is the first node, colour it black
- Otherwise, colour it red

Let $x$ be the inserted node, $y$ its parent, and $z$ its grandparent
- If $y$ is black, no problem. This is like inserting a new key to an existing node in [[(2, 4) Trees|(2, 4) tree]].
- If $y$ is red, the problem is called *double red*, i.e, violation of the red property

Double red cases:
- Case #1: The sibling $s$ of $y$ is black. No overflow, just malformed, so restructure
- Case #2: The sibling of $y$ is red. Overflow, so split
![[red_black_insert_case_1.png]]
![[red_black_insert_case_2.png]]
![[red_black_insertion.png]]

## Deletion
To delete an existing key $k$:
- search for $k$ and delete it as in BST
- May require replacement by another key
- We will eventually need to remove some key $k'$ (either $k$ itself or its inorder predecessor) from an internal node
	- One child of that internal node is external, which will be removed along with $k'$
	- The other child is promoted with the removal of $k'$

If $k'$ is red, then its removal preserves all properties of red-black tree
- This is like removing a key from a 4 or 3 node, where there is another black key

If $k'$ is black, and the child node $p$ to be promoted is red, recolour $p$ to black
- This is like removing a key from a 3 node in a [[(2, 4) Trees|(2, 4) tree]], which $k'$ used to anchor

If $k'$ is black, and $p$ is black, recolour $p$ to **double black** temporarily
- This is like removing a key from a 2 node in a [[(2, 4) Trees|(2, 4) tree]]

![[red_black_deletion_case_1.png]]
![[red_black_deletion_case_2.png]]
![[red_black_deletion_case_3.png]]

## Complexity
For search, insertion and removal: $O(logn)$
Insertion required $O(logn)$ recolourings and at most 1 trinode restructuring
Deletion requires $O(logn)$ recolourings and at most 2 trinode restructurings