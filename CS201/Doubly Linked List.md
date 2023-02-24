# Definition
A single linked list with the ability to know the previous node

-------

## General variables and functions
Mostly the same as Singly Linked List with some exceptions
```Java
public class DoublyLinkedList<E> {  
	private static class Node<E> {... //nested Node class  
	private Node<E> header; // header sentinel  
	private Node<E> trailer; // trailer sentinel  
	private int size = 0; // number of elements in the list  
	public DoublyLinkedList() {  
		header = new Node<>(null, null, null); // create header  
		trailer = new Node<>(null, header, null); // trailer is preceded by header  
		header.setNext(trailer); // header is followed by trailer  
	}
	...
}
```

### Add to the end
```Java
public void addLast(E e) {  
	Node<E> newest = new Node<>(e, tail, null);  
	if (isEmpty())  
		head = newest;  
	else  
		tail.setNext(newest);  
	tail = newest;  
	size++;  
}
```

### Remove from the end
```Java
public E removeLast() {  
	if (isEmpty()) return null;  
	E answer = tail.getElement();  
	tail = tail.getPrev();  
	size--;  
	if (size == 0)  
		head = null; // list is now empty  
	else  
		tail.setNext(null); // if not empty  
	return answer;  
}
```

### Add between
```Java
private void addBetween(E e, Node<E> predecessor, Node<E> successor) {  
	// create and link a new node  
	Node<E> newest = new Node<>(e, predecessor, successor);  
	predecessor.setNext(newest);  
	successor.setPrev(newest);  
	size++;  
}
```
