# Definition
Expressing a problem as a smaller version of itself. It consists of a recursive step (to get smaller) and a base case (the smallest version).

----
## Factorial
The number of permutations of $n$ distinct items
![[factorial_function.png]]
![[factorial_implementation.png]]

----
## Linear Recursion
```Java
public static int linearSum(int[] data, int n) {
	if (n == 0)
		return 0;
	else
		return linearSum(data, n-1) + data[n-1];
}
```
This has a time complexity of O(n)

## Binary Recursion
```Java
public static int binarySum(int[] data, int low, int high) {
	if (low > high) // zero elements in subarray
		return 0;
	else if (low == high) // one element in subarray
		return data[low];
	else {
		int mid = (low + high) / 2;
		return binarySum(data, low, mid) + binarySum(data, mid+1, high);
	}
}
```
![[binary_recursion.png]]
The left side will have to complete all recursions before proceeding to the right

## Multiple Recursion
```Java
/**
* Calculates the total disk usage (in bytes) of the portion of the file system
rooted at the given path, while printing a summary
*/
public static long diskUsage(File root) {
	long total = root.length(); // start with direct disk usage
	if (root.isDirectory()) { // and if this is a directory,
		for (String childname : root.list()) { // then for each child
			File child = new File(root, childname); // compose full path to child
			total += diskUsage(child); // add child's usage to total
		}
	}
	System.out.println(total + "\t" + root); // descriptive output
	return total; // return the grand total
}
```
![[disk_usage.png]]

----
## Inefficient vs Efficient Recursion
### Fibonacci Numbers
![[fibonacci_number.png]]
#### Inefficient recursive
```Java
/** Returns the nth Fibonacci number (inefficiently). */
public static long fibonacciBad(int n) {
	if (n <= 1)
		return n;
	else
		return fibonacciBad(n-2) + fibonacciBad(n-1);
}
```
