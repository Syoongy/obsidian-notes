We break a problem of larger size into smaller sub problems. This allows us to solve these smaller problems to form a solution for the larger problem
There are 3 steps:
1) Divide
2) Conquer: solve the sub-problems
3) Combine: combine solutions of the sub-problems
An example of this would be merge sort:
```Python
def merge_sort(A):

    if len(A) > 1:

        mid = len(A) // 2

        Lhalf, Rhalf = A[:mid], A[mid:]

        merge_sort(Lhalf)

        merge_sort(Rhalf)

        merge Lhalf and Rhalf into A
```
##### Merge sort divides the main problem into 2 sub-problems
1) Is it possible to divide into > 2 sub-problems? (e.g. Strassen Algorithm)
2) Is it possible to divide into just one sub-problem? (e.g. Binary search)

##### Merge sort spends more effort in “combine” than “divide”, is there any divide and conquer algorithm that spends more effort in “divide” than “combine”?
Quick sort

# Binary Search

# Quick Sort
![[quick_sort.png]]
![[quick_sort_2.png]]
Unlike merge sort, we have no combine step. The 2 subarrays already form a sorted array (in-place sort)
## Divide
`A[p..r]` is partitioned into 2 subarrays `A[p..q-1]` and `A[q+1..r]`
- All elements in `A[p..q-1] <= A[q]`
- All elements in `A[q+1..r] >= A[q]`
We first want to partition all elements in A, according to `A[q]`
![[Pasted image 20230125101029.png]]
## Conquer
The subarrays are recursively sorted

## In-place sort
```Python
pick k = A[r]  
initialize list B, C = [], []  
for i in range(p, r):  
    if A[i] <= k:  
        B.append(A[i])  
    else:  
        C.append(A[i])  
A = B + [k] + C
```
We always create two new lists that are only used once. This can lead to many mallocs for large lists.
To solve this, we try to implement in-place quick sort

## Complexity
In the worst case scenario for quick sort, the partition would always be unbalanced (e.g. one side of the pivot is empty). We would partition a list of size n into a list of size n-1 and a pivot
We would then get $T(n) = T(n-1) + \theta(n) =\theta(n^2)$ where in general,![[Pasted image 20230125101516.png]]
The best case scenario would give us, $T(n) = 2 . T(n/2) + \theta(n) = \theta(nlogn)$
For the average case, we would have a mix of "bad" and "good" splits where:
- They are randomly distributed in the recursion tree
- Pretend that they alternate between best-case $(\frac{n}{2} : \frac{n}{2})$ and worse-case $(n-1: 0)$
- What happens if there is a bad split at the root node then a good split of the size n-1 partition?
- We will end up with 3 subarrays of size $0, \frac{n-1}{2} - 1, \frac{n-1}{2}$
- Of which, the cost would be $\theta(n) + \theta(n-1) = \theta(n)$
- This is no different that having a good split for the original list
- We can assume that the O(n) cost of a bad split can be absorbed by a good split
- Running time of alternating bad/good split is still O($nlogn$), with slightly higher constants

# Selection
We have an input list A which might not be sorted and an index $i$. We want the $i^{th}$ smallest/largest elemtn in A.
We have 2 algorithms:
- A randomised algorithm with O(n) expected time
- A cool algorithm with O(n) worst-case time
## Randomised Selection
```Python
def randomized_select(A, p, r, i):

    if p == r:

        return A[p]

    q = randomized_partition(A, p, r)

    k = q - p + 1

    if i == k:

        return A[q] 

    if i < k:

        return randomized_select(A, p, q-1, i)

    else:

        return randomized_select(A, q+1, r, i-k)
```
The idea here is to use `partition` from Quicksort where we only need to examine 1 partition(Decrease and Conquer). This results in O(n) time.
![[randomised_selection.png]]
### Worst case
The partition always gives a $0 : n-1$ split
$$T(n) = T(n-1) + O(n) = O(n^2)$$
### Best case
Suppose a (9:1) split
$$T(n) = T(\frac{9n}{10}) + O(n) = O(n)$$
### Average Case
For upper bound, assume $i^{th}$ element always falls in larger side of partition![[randomised_selection_avg.png]]![[randomised_selection_avg_2.png]]

--------------------------------------
# Strassen Algorithm
A divide and conquer algorithm that reduces the time complexity of matrix multiplication from $O(n^3)$ to $O(n^{log_2{7}}) \approx O(n^{2.8})$
![[strassen_algorithm.png]]
## Subdividing Matrices
Would subdividing matrices be better?
Subdivision would give us $$T(n) = 8 . T(\frac{n}{2} + \theta(n^2))$$
Therefore, it is not more efficient
