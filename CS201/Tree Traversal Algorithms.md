## Tree Traversal Algorithms
### Preorder Traversal
```Java
public Iterable<Position<E>> preorder() {  
	List<Position<E>> snapshot = new ArrayList<>();  
	if (!isEmpty())  
		preorderSubtree(root(), snapshot);  
	return snapshot;  
}

private void preorderSubtree(Position<E> p, List<Position<E>> snapshot){  
	snapshot.add(p);  
	for (Position<E> c : children(p))  
		preorderSubtree(c, snapshot);  
}
```

### Postorder Traversal
```Java
public Iterable<Position<E>> postorder() {  
	List<Position<E>> snapshot = new ArrayList<>();  
	if (!isEmpty())  
		postorderSubtree(root(), snapshot);  
	return snapshot;  
}

private void postorderSubtree(Position<E> p, List<Position<E>> snapshot) {  
	for (Position<E> c : children(p))  
		postorderSubtree(c, snapshot);  
	snapshot.add(p);  
}
```

### Inorder Traversal of a Binary tree
```Java
public Iterable<Position<E>> inorder() {  
	List<Position<E>> snapshot = new ArrayList<>();  
	if (!isEmpty())  
		inorderSubtree(root(), snapshot);  
	return snapshot;  
}

private void inorderSubtree(Position<E> p, List<Position<E>> snapshot) {  
	if (left(p) != null)  
		inorderSubtree(left(p), snapshot);  
	snapshot.add(p);  
	if (right(p) != null)  
		inorderSubtree(right(p), snapshot);  
}
```

### Euler Tour Traversal
![[Euler Tour Traversal.png]]

----