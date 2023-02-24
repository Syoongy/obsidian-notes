## Binary Tree
A tree where a node has a max of 2 children, _left_ and _right_
### Example Implementation
```Java
/** An interface for a binary tree, in which each node has at most two children. */  
public interface BinaryTree<E> extends Tree<E> {  
	Position<E> left(Position<E> p) throws IllegalArgumentException;  
	Position<E> right(Position<E> p) throws IllegalArgumentException;  
	Position<E> sibling(Position<E> p) throws IllegalArgumentException;  
}

/**An abstract base class providing some functionality of the BinaryTree interface.  
*/  
public abstract class AbstractBinaryTree<E> extends AbstractTree<E> implements BinaryTree<E> {  
	public Position<E> sibling(Position<E> p) {  
		Position<E> parent = parent(p);  
		if (parent == null) return null; // p must be the root  
		if (p == left(parent)) // p is a left child  
			return right(parent); // (right child might be null)  
		else // p is a right child  
			return left(parent); // (left child might be null)  
	}
	
	public int numChildren(Position<E> p) {  
		int count=0;  
		if (left(p) != null)  
			count++;  
		if (right(p) != null)  
			count++;  
		return count;  
	}
	
	public Iterable<Position<E>> children(Position<E> p) {  
		List<Position<E>> snapshot = new ArrayList<>(2); // max capacity of 2  
		if (left(p) != null)  
			snapshot.add(left(p));  
		if (right(p) != null)  
			snapshot.add(right(p));  
		return snapshot;  
	}
}
```

For the number of nodes in a binary tree, we can have it as $n <= 2^{h+1}-1$ where h is the height.

### Proper Binary tree
This is the case when every node has only 0 or 2 children. For a non-empty binary tree, the re will be an odd number of nodes and the external nodes will outnumber the internal nodes by 1.

### Implementation Types
#### Array-based
- Let $f(p)$ be the index of node p in the array
- if $p$ is the root, $f(p) = 0$
- if $p$ is the left child of $q$, $f(p) = 2 \times f(q)+1$
- if $p$ is the right child of $q$, $f(p) = 2 \times f(q)+2$

#### [[Linked List]] based
##### Node
```Java
public class LinkedBinaryTree<E> extends AbstractBinaryTree<E> {  
	/** Nested static class for a binary tree node. */  
	protected static class Node<E> implements Position<E> {  
		private E element; // an element stored at this node  
		private Node<E> parent; // a reference to the parent node (if any)  
		private Node<E> left; // a reference to the left child (if any)  
		private Node<E> right; // a reference to the right child (if any)  
		public Node(E e, Node<E> above, Node<E> leftChild, Node<E> rightChild) {  
			element = e;  
			parent = above;  
			left = leftChild;  
			right = rightChild;  
		}  
		public E getElement() { return element; }  
		public Node<E> getParent() { return parent; }  
		public Node<E> getLeft() { return left; }  
		public Node<E> getRight() { return right; }  
		public void setElement(E e) { element = e; }  
		public void setParent(Node<E> parentNode) { parent = parentNode; }  
		public void setLeft(Node<E> leftChild) { left = leftChild; }  
		public void setRight(Node<E> rightChild) { right = rightChild; }  
	} //----------- end of nested Node class -----------

	/** Factory function to create a new node storing element e. */  
	protected Node<E> createNode(E e, Node<E> parent, Node<E> left, Node<E> right) {  
		return new Node<E>(e, parent, left, right);  
}  
	/** Places element e at the root of an empty tree and returns its new Position. */  
	public Position<E> addRoot(E e) throws IllegalStateException {  
		if (!isEmpty()) throw new IllegalStateException("Tree is not empty");  
		root = createNode(e, null, null, null);  
		size = 1;  
		return root;  
	}

	protected Node<E> validate(Position<E> p) throws IllegalArgumentException {  
		if (!(p instanceof Node))  
			throw new IllegalArgumentException("Not valid position type");  
		Node<E> node = (Node<E>) p; // safe cast  
		if (node.getParent() == node) // our convention for defunct node  
			throw new IllegalArgumentException("p is no longer in the tree");  
		return node;  
	}
	
	/** Creates a new left child of Position p storing element e and returns its Position. */  
	public Position<E> addLeft(Position<E> p, E e) throws IllegalArgumentException {  
		Node<E> parent = validate(p);  
		if (parent.getLeft() != null)  
			throw new IllegalArgumentException("p already has a left child");  
		Node<E> child = createNode(e, parent, null, null);  
		parent.setLeft(child);  
		size++;  
		return child;  
	}
	
	/** Creates a new right child of Position p storing element e and returns its Position. */  
	public Position<E> addRight(Position<E> p, E e) throws IllegalArgumentException {  
		Node<E> parent = validate(p);  
		if (parent.getRight() != null)  
			throw new IllegalArgumentException("p already has a right child");  
		Node<E> child = createNode(e, parent, null, null);  
		parent.setRight(child);  
		size++;  
		return child; 
	}

	/** Replaces the element at Position p with element e and returns the replaced  
element. */  
	public E set(Position<E> p, E e) throws IllegalArgumentException {  
		Node<E> node = validate(p);  
		E temp = node.getElement();  
		node.setElement(e);  
		return temp;  
	}

	/** Removes the node at Position p and replaces it with its child, if any. */  
	public E remove(Position<E> p) throws IllegalArgumentException {  
		Node<E> node = validate(p);  
		if (numChildren(p) == 2) throw new IllegalArgumentException("p has two children");  
		Node<E> child = (node.getLeft() != null ? node.getLeft() : node.getRight() );  
		if (child != null)  
			child.setParent(node.getParent()); // child's grandparent becomes its parent  
		if (node == root)  
			root = child; // child becomes root  
		else {  
			Node<E> parent = node.getParent();  
			if (node == parent.getLeft())  
				parent.setLeft(child);  
			else  
				parent.setRight(child);  
		}  
		size--;  
		E temp = node.getElement();  
		node.setElement(null); // help garbage collection  
		node.setLeft(null);  
		node.setRight(null);  
		node.setParent(node); // our convention for defunct node  
		return temp;  
	}

	/**  
	* Attaches trees t1 and t2, respectively, as the left and right subtree of the  
	* leaf Position p. As a side effect, t1 and t2 are set to empty trees.  
	*/  
	public void attach(Position<E> p, LinkedBinaryTree<E> t1, LinkedBinaryTree<E> t2) throws IllegalArgumentException {  
		Node<E> node = validate(p);  
		if (isInternal(p)) throw new IllegalArgumentException("p must be a leaf");  
			size += t1.size() + t2.size();  
		if (!t1.isEmpty()) { // attach t1 as left subtree of node  
			t1.root.setParent(node);  
			node.setLeft(t1.root);  
			t1.root = null;  
			t1.size = 0;  
		}  
		if (!t2.isEmpty()) { // attach t2 as right subtree of node  
			t2.root.setParent(node);  
			node.setRight(t2.root);  
			t2.root = null;  
			t2.size = 0;  
		}  
	}

}
```

----