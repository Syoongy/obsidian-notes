----
# Definition
A binary tree with these two properties
### Heap-Order Property
- For every position $p$ (except the root), the key at $p$ is greater than at its parent
### Complete Binary Tree Property
- Every level of the tree (except the last) have the maximal number of nodes possible
- The remaining nodes at the last level reside in the leftmost possible positions

## Adding Entry to Heap
- To preserve the complete binary tree property
	- Insert the new entry just after the rightmost entry at the last level
- To preserve the heap-order property
	- Interatively swap a position with its parent if the former's key is smaller than the latter's
### Up-Heap Bubbling After Insertion
![[up_heap_bubbling_insertion.png]]
![[up_heap_bubbling_insertion_cont.png]]
```Java
/** Inserts a key-value pair and return the entry created.*/  
public Entry<K,V> insert(K key, V value) throws IllegalArgumentException {  
	checkKey(key); // auxiliary key-checking method (could throw exception)  
	Entry<K,V> newest = new PQEntry<>(key, value);  
	heap.add(newest); // add to the end of the list  
	upheap(heap.size() - 1); // upheap newly added entry  
	return newest;  
}  
/** Moves the entry at index j higher, if necessary, to restore heap property. */  
protected void upheap(int j) {  
	while (j > 0) { // continue until reaching root (or break statement)  
		int p = parent(j);  
		if (compare(heap.get(j), heap.get(p)) >= 0) break;//heap property verified  
		swap(j, p);  
		j = p; // continue from the parent's location  
	}  
}
```
## Removing Entry with Minimum Key from Heap
- Minimum key is at the root
- To preserve the complete binary tree property
	- Replace the root with the rightmost entry at the last level
- To preserve the heap-order property
	- Iteratively swap the newly relocated position with its child with the lower key
### Down-Heap Bubbling After Removal
![[down_heap_bubbling_removal.png]]
![[down_heap_bubbling_removal_cont.png]]
```Java
public Entry<K,V> removeMin() {  
	if (heap.isEmpty()) return null;  
	Entry<K,V> answer = heap.get(0);  
	swap(0, heap.size() - 1); // put minimum item at the end  
	heap.remove(heap.size() - 1); // and remove it from the list;  
	downheap(0); // then fix new root  
	return answer;  
}  
protected void downheap(int j) {  
	while (hasLeft(j)) { // continue to bottom (or break statement)  
		int leftIndex = left(j);  
		int smallChildIndex = leftIndex; // although right may be smaller  
		if (hasRight(j)) {  
			int rightIndex = right(j);  
			if (compare(heap.get(leftIndex), heap.get(rightIndex)) > 0)  
				smallChildIndex = rightIndex; // right child is smaller  
		}  
		if (compare(heap.get(smallChildIndex), heap.get(j)) >= 0)  
			break; // heap property has been restored  
		swap(j, smallChildIndex);  
		j = smallChildIndex; // continue at position of the child  
	}  
}
```
## Complexity of Heap-Based Priority Queue
![[heap_priority_queue_complexity.png]]
## Heapify
A bottom up construction of a heap.
If the elements to be inserted into a heap are known in advance, the heap  
construction can be done in $O(n)$ time.
Pseudocode:
- Input array of size $n$. Interpret this as the initial complete binary tree
- Starting from the parent of the last element, iteratively perform down-heap
Heapify will create many sub-heaps at the deeper levels
- Majority of the nodes in a binary tree are at the deepest levels
- Many down-heaps encompass shorter heights
```Java
	/** Creates a priority queue initialized with the respective key-value pairs. The two arrays given will be paired */  
	public HeapPriorityQueue(K[] keys, V[] values) {  
		super();  
		for (int j=0; j < Math.min(keys.length, values.length); j++)  
			heap.add(new PQEntry<>(keys[j], values[j]));  
		heapify();  
	}  
	/** Performs a bottom-up construction of the heap in linear time. */  
	protected void heapify() {  
		int startIndex = parent(size()-1); // start at PARENT of last entry  
		for (int j=startIndex; j >= 0; j--) // loop until processing the root  
			downheap(j);  
	}
```
![[heapify.png]]
![[heapify_cont.png]]
### Complexity
- For a given key, the number of swaps is proportional to the distance between the key and its ‘inorder successor’ (smallest key on its right sub-tree)
	- May not be the actual path of down-heap, but the distance is similar
- Every key has a unique 'inorder successor' and the path is distinct
- The number of swaps is bounded by the number of edges in the tree, $O(n)$
	- A tree of $n$ nodes has ($n$ - 1) edges, as each node has an edge to its parent (except root)

----
## Priority Queue
```Java
public interface PriorityQueue<K,V> {  
	/** Returns the number of items in the priority queue. */  
	int size();  
	/** Tests whether the priority queue is empty. */  
	boolean isEmpty();  
	/** Inserts a key-value pair and returns the entry created. */  
	Entry<K,V> insert(K key, V value) throws IllegalArgumentException;  
	/** Returns (but does not remove) an entry with minimal key. */  
	Entry<K,V> min();  
	/** Removes and returns an entry with minimal key. */  
	Entry<K,V> removeMin();  
}
```
### Total Ordering of Keys
![[priority_queue_keys.png]]
### Comparing keys
It can be based on lexicographic order or length for Strings. As long as there is a comparator, we can compare any object.

### List-based Implementation
#### Unsorted Priority Queue
```Java
public class UnsortedPriorityQueue<K,V> extends AbstractPriorityQueue<K,V> {  
...  
	/** Inserts a key-value pair and returns the entry created. */  
	public Entry<K,V> insert(K key, V value) throws IllegalArgumentException {  
		checkKey(key); // auxiliary key-checking method (could throw exception)  
		Entry<K,V> newest = new PQEntry<>(key, value);  
		list.addLast(newest);  
		return newest;  
	}  
	/** Removes and returns an entry with minimal key. */  
	public Entry<K,V> removeMin() {  
		if (list.isEmpty()) return null;  
		return list.remove(findMin());  
	}  
	/** Returns the Position of an entry having minimal key. */  
	private Position<Entry<K,V>> findMin() { // only called when nonempty  
		Position<Entry<K,V>> small = list.first();  
		for (Position<Entry<K,V>> walk : list.positions())  
			if (compare(walk.getElement(), small.getElement()) < 0)  
				small = walk; // found an even smaller key  
		return small;  
	}
...
```
#### Sorted Priority Queue
```Java
public class SortedPriorityQueue<K,V> extends AbstractPriorityQueue<K,V> {  
...  
	/** Inserts a key-value pair and returns the entry created. */  
	public Entry<K,V> insert(K key, V value) throws IllegalArgumentException {  
		checkKey(key); // auxiliary key-checking method (could throw exception)  
		Entry<K,V> newest = new PQEntry<>(key, value);  
		Position<Entry<K,V>> walk = list.last();  
		// walk backward, looking for smaller key  
		while (walk != null && compare(newest, walk.getElement()) < 0)  
			walk = list.before(walk);  
			if (walk == null)  
				list.addFirst(newest); // new key is smallest  
			else  
				list.addAfter(walk, newest); // newest goes after walk  
			return newest;  
	}  
	/** Removes and returns an entry with minimal key. */  
	public Entry<K,V> removeMin() {  
		if (list.isEmpty()) return null;  
		return list.remove(list.first());  
	}
...
```
