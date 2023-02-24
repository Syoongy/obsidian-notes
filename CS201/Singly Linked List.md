# Definition
A singly linked list begins with a head node and ends with a tail node

--------------
## General variables and functions
```Java
public class SinglyLinkedList<E> implements Cloneable {  
	private static class Node<E> {...} // nested Node class  
	private Node<E> head = null; // head node of the list (or null if empty)  
	private Node<E> tail = null; // last node of the list (or null if empty)  
	private int size = 0; // number of nodes in the list  
	public SinglyLinkedList() { } // constructs an initially empty list  
	public int size() {...  
	public E first() {... // returns (but does not remove) the first element  
	public E last() {... // returns (but does not remove) the last element  
	public void addFirst(E e) {... // adds element e to the front of the list  
	public void addLast(E e) {... // adds element e to the end of the list  
	public E removeFirst() {... // removes and returns the first element
	...
}
```

-------
### Adding to the front
We want to call the addFirst() function
```Java
public void addFirst(E e) {  
	head = new Node<>(e, head);  
	// create and link a new node  
	if (size == 0) //special case  
		tail = head; //new node becomes tail  
	size++;  
}
```

### Adding to the back
```Java
public void addLast(E e) {
	Node<E> newest = new Node<>(e, null);
	// node will eventually be the tail
	if (isEmpty())
		head = newest;
	// special case: previously empty list
	else
		tail.setNext(newest);
	// new node after existing tail
	tail = newest;
	// new node becomes the tail
	size++;
}
```

### Removing from the front
```Java
public E removeFirst() {  
	if (isEmpty()) return null;  
	// nothing to remove
	
	E answer = head.getElement();  
	head = head.getNext();  
	// null if list had only one node
	
	size--;  
	if (size == 0)  
		tail = null;  
	// special case as list is now empty  
	return answer;  
}
```

### Removing from the back
```Java
public E removeLast() {  
	if (isEmpty()) return null; // nothing to remove  
	E answer = tail.getElement();  
	if (head == tail) { // if there is only one node  
		head = null;  
		tail = null;  
	}  
	else { 
		// if more than one node, find second last node  
		Node walk = head;  
		while(walk.getNext() != tail)  
		walk = walk.getNext();  
		walk.setNext(null);  
		tail = walk;  
	}  
	size--;  
	return answer;  
}
```
^ This is inefficient
