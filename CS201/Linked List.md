# What is a linked list?
A dynamically sized collection of nodes that collectively form a linear sequence

-----------------------------

## Nodes
A node contains an element as well as a pointer to the next node

-----------------

## Types
- [[Singly Linked List]]
- [[Doubly Linked List]]
- [[Circular Linked List]]

--------
### Suppose the Scoreboard program is implemented with DoublyLinkedList.
### a) How many node additions/removals are needed in totality as the entries are inserted in the given sequence?
5 + 2 + 2 = 9

```Java
String[] names = {"Rob", "Mike", "Rose", "Jill", "Jack", "Anna", "Paul", "Bob"};  
int[] scores = {750, 1105, 590, 740, 510, 660, 720, 400};
```
### b) How many comparisons?
where n is the number of items in the sequence and k is the capcity of our linked list
- Fewest: **n-1
- Most: **(k-1(k))/2+ k(n-k)