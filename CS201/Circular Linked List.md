# Definition
We only need to keep the tail, as the head is always after the tail

----------------
## General variables and functions
Mostly the same as [[Doubly Linked List]] other than

### Rotate
```Java
public void rotate() {
	// rotate the first element to the back of the list  
	if (tail != null) // if empty, do nothing  
		tail = tail.getNext(); 
		// the old head becomes the new tail  
}
```