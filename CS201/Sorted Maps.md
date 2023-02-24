# What is it?
Regular [[Maps]] are meant for exact search while sorted maps are used for range search

----
## Abstract Data Type
```Java
public interface SortedMap<K,V> extends Map<K,V>{  
	Entry<K,V> firstEntry(); /** Returns the entry having the least key (or null). */  
	Entry<K,V> lastEntry(); /** Returns the entry having the greatest key (or null). */  
	/** Returns the entry with least key greater than or equal to given key */  
	Entry<K,V> ceilingEntry(K key) throws IllegalArgumentException;  
	/** Returns the entry with greatest key less than or equal to given key */  
	Entry<K,V> floorEntry(K key) throws IllegalArgumentException;  
	/** Returns the entry with greatest key strictly less than given key */  
	Entry<K,V> lowerEntry(K key) throws IllegalArgumentException;  
	/** Returns the entry with least key strictly greater than given key */  
	Entry<K,V> higherEntry(K key) throws IllegalArgumentException;  
	/** Returns all keys in the range from fromKey (inclusive) to toKey (exclusive). */  
	Iterable<Entry<K,V>> subMap(K fromKey, K toKey) throws IllegalArgumentException;  
}
```

----
## TreeMap
```Java
public class TreeMap<K,V> extends AbstractSortedMap<K,V> {  
	/** Returns the value associated with the specified key*/  
	public V get(K key) throws IllegalArgumentException {  
		checkKey(key); // may throw IllegalArgumentException  
		Position<Entry<K,V>> p = treeSearch(root(), key);  
		if (isExternal(p)) return null; // unsuccessful search  
		return p.getElement().getValue(); // match found  
	}  
	/** Returns the position in p's subtree having the given key */  
	private Position<Entry<K,V>> treeSearch(Position<Entry<K,V>> p, K key) {  
		if (isExternal(p))  
			return p; // key not found; return the final leaf  
		int comp = compare(key, p.getElement());  
		if (comp == 0)  
			return p; // key found; return its position  
		else if (comp < 0)  
			return treeSearch(left(p), key); // search left subtree  
		else  
			return treeSearch(right(p), key); // search right subtree  
	}
```

### Complexity
![[bst_complexity.png]]
The worst case scenario would be a completely linear tree with all items on either the left or right exclusively

----
## Balanced Search Tree
A binary tree is balanced if:
- for every internal position $p$, the heights of $p$'s children differ by at most 1
Worst case search, insert, remove will be O($logn$)
The primary operation to rebalance is rotation (A child is rotated above its parent)
![[balanced_search_tree_rotation.png]]

----
## AVL Trees
Named after inventors Adelson-Velsky and Landis and performs rebalancing after each insertion or removal

### Insertion
- Assume that a binary tree $T$ is balanced (e.g. an AVL tree) before insertion
- After inserting a node $p$, the new tree $T'$ is now unbalanced
- Upon tacing the ancestors of $p$, we find $z$ as the earliest unbalanced node
- This implies that $z$ has two children
	- Previously with height difference 1, but now with height difference 2
	- Let $y$ be the "taller" of $z$'s two children, which is also the one that is an ancestor of $p$
	- let $x$ be the "taller" child of $y$, which may be an ancestor $p$ , or $p$ itself
- Upon restructuring at $x$
	- $z$ will add to the height of $y$'s shorter sibling
	- $x$ and $y$ were both balanced before, so will remain balanced after
	- $y$ or $x$ will take the former place of $z$, thereby the height of local subtree remains
		- the rest of the tree outside of the local subtree is not affected by the restructuring, yet any ancestor of $z$ that became unbalanced is now balanced again
![[avl_insertion.png]]
![[avl_insertion_example.png]]