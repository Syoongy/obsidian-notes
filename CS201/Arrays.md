# What is an array?
A fixed-size sequenced collection of elements of the same type

----------------------------------------

## Adding/Removing an element in the middle
- Requires us to shift all elements to the right of the element within the array
- This shift can be left or right

--------------------------------------

### a) How many elements need to shift (change position) in totality as the entries are inserted in the given sequence of capacity 5?
1 + 1 + 1 + 1 = 4
```Java
String[] names = {"Rob", "Mike", "Rose", "Jill", "Jack", "Anna", "Paul", "Bob"};  
int[] scores = {750, 1105, 590, 740, 510, 660, 720, 400};
```
### b) What are the sequences that will produce the fewest and the most shifts?
- If the sequences are in descending order, there will be the least number of shifts, **O(0).
- If the sequences are in ascending order, there will be the greatest number of shifts, 
1 + 2 + 3 + 4 + 4 + 4 +4 + 4 = 22 **O((c-1)! + (c-1)(n-c)) = O(4n - 10) when c = 5

### c) How is the number of shifts affected by the length of the sequence?
It can increase the number of shifts required.
$$k/2(k-1) + (n-k)(k-1)$$

[How do we reduce the complexity?](Linked%20List.md)