Differs from divide and conquer as it reuses answers from common sub-sub problems. The answers are stored in a table for future reference.

## Optimisation Problem
- Many solutions, each having an objective value
- Goal is to find a solution with the optimal value
- Minimisation problem (e.g. Shortest path, Scheduling)
- Maximisation problem (e.g. Tour planning)
Given a problem $P$, obtain a sequence of problems $Q_0, Q_1, ..., Q_m$ where:
- we have a solution to $Q_0$
- The solution to problem $Q_{J'} \space J > 0$, can be obtained from solutions to problems $Q_k \space where \space k < j$ 

## Rod-Cutting problem
![[rod_cutting_1.png]]
![[rod_cutting_2.png]]
![[rod_cutting_3.png]]

### Recursive Approach
```Python
def rod_cutting_recur(n):

    if n == 0:

        return 0

    q = 0

    for i in range(1, n+1):

        q = max(q, rod_price[i] +

            rod_cutting_recur(n-i))

    return q
```
This is $\Theta(2^n)$
### Bottom-up Approach
```Python
def rod_cutting_iterative():
	for i in range(1, n):
		for j in range(1, min(i+1, len(rod_price))):
			new_price = rod_price[j] + max_price[i-j]
			if new_price > max_price[i]:
				max_price[i] = new_price
				first_cut[i] = j
```
This is $\Theta(n^2)$

## Elements of Dynamic Programming
Dynamic programming is used to solve optimisation problems with these 2 characteristics
### Optimal Sub-structure
This is known as the principle of Optimality. Any optimal solution to the problem should contain optimal solutions to sub-problems. (e.g. An optimal solution for 9 contains an optimal solution for 6)
### Overlapping Sub-problems
We may need to solve the sub-problem more than once in cases such as the optimal solution for 8 and 9. Thus, we would need to solve for the optimal solution for 6 more than once.

### Steps to design a DP algorithm
![[designing_dp_algo.png]]

## Matrix Chain Multiplication
Order matters as it changes the cost of multiplications
An example of this:
- $A_1$: 10 x 100
- $A_2$: 100 x 5
- $A_3$: 5 x 50
To multiply these matrices,
$((A_1A_2)A_3)$, the cost of multiplications = $10 \times 100 \times 5 + 10 \times 5 \times 50 = 7500$
$(A_1(A_2A_3))$, the cost of multiplications = $100 \times 5 \times 50 + 10 \times 100 \times 50 = 75000$
![[matrix_chain_multiplication_1.png]]
![[matrix_chain_multiplication_2.png]]
![[memoization.png]]
## Coin Change With Limited Supply
![[coin_change_w_limited_supply.png]]
## Knapsack
![[knapsack.png]]
## Longest Common Subsequence
![[longest_common_subsequence.png]]
### Exercise
![[longest_common_subsequence_exercise.png]]
```
lcs(X, Y, m, n) = 
	case 1: 0 if m == 0 or n == 0
	case 2: 1 + lcs(X, Y, m-1, n-1) if m*n > 0 and X[m-1] == y[n-1]
	case 3: max(lcs(X, Y, m-1, n-1) if m*n > 0 and X[m-1] != y[n-1])
```
## Edit Distance
![[edit_distance_1.png]]
