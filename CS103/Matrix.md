# Definition
For [[Linear Algebra]], a matrix is a table of numbers.

## General matrix
$$A∈ℝ^{m×n}$$
Where rows = m and columns = n

-----
## Multiplication
We are only able to multiple matrices when matrix a's row is equal to matrix b's column or vice versa.
$$\begin{bmatrix}1 & 2 \\3 & 5 \\ \end{bmatrix}\begin{bmatrix}7 \\11 \\ \end{bmatrix} = \begin{bmatrix}29 \\ 76 \end{bmatrix} $$
This multiplication is not commutative
## Blockwise multiplication
We can simplify blocks to make it easier to multiply before expanding out for the final result.
$$\begin{bmatrix}a_{11} & a_{12} \\a_{21} & a_{22} \\ \end{bmatrix}\begin{bmatrix}x_1 \\x_2 \\ \end{bmatrix} = \begin{bmatrix}a_{11}x_1 + a_{12}x_2 \\ a_{21}x_1 + a_{22}x_2 \end{bmatrix} $$
$$\bar{a} \cdot \bar{b} = \bar{a} ^t \bar{b}$$