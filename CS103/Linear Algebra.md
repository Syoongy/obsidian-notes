# Expressions
- Any combination of variables is a mathematical expression
- An expression is linear if the LHS and RHS functions are both linear
- Expression with a name is a function
	- $$f(x)=ax, g(x)=lnx, f(x)=e^x$$
	- As long as it is **single-valued**
	- f(x)=|x^1⁄2| ⟶ Function
	- f(x)=x^1⁄2⟶ Not a function
- Notation: f:ℝ↦ℝ, x∈ℝ
	- f transforms a real number to another real number

# Equations
expression or function = another one is an equation
- In linear algebra,
	- Equation ⇒ Expression = Constant
		$$ax^2+bx+c=0$$
		$$−mx+y=c$$
- Equal sign and Equality
	- f(x)=Expression ⇒ Label assignment
	- Expression = constant ⇒ Statement of truth

# Transformations
Takes in **1** mathematical entity and returns another
- Example: A function: y=f(x), x and y are real numbers.
- Notation: $$f:ℝ ⟼ℝ  with x,y∈ℝ$$
	$$x→ f(x)→y$$
- Even roots are not functions while odd roots are functions
	 $$f(x)=x^−1/2$$⟶ not a function

------------

# How to tell if an expression/function is linear?

## Homogeneity
Scaling the input variable scales the output of the expression (or function) by the same factor
f(sx)=sf(x)   ∀ s, x∈ℝ

## Additivity
The output of the expression (or function) for the sum of two inputs is the same as the sum of the corresponding outputs.
f(x+x^′)=f(x)+f(x^′)   ∀ x, x′∈ℝ

------------------
# Testing for linearity
- 0 should transform to 0
- Negative input --> Output changes sign
- Scale input --> output scales
- Sum of inputs --> sum of outputs

------
# Is y = mx + c linear?
Both x and y need to scale to satisfy Homogeneity.
$$f(sx, sy)=−msx+sy
=s(−mx+y)
=sf(x,y)$$
Both x and y need to satisfy additivity
$$f(x+x^′, y+y′) =−m(x+x^′)+y+y^′
=(−mx+y)+(−mx^′+y^′)
=f(x,y)+f(x^′,y^′)$$

But f(x)=mx+c is not linear, as a function of one variable
The only linear expression is in one var
$$ax    a,x∈ℝ$$
The only linear equation in one var is
$$ax=b      a,x,b∈ℝ$$

## Generalising Linearity
We need to generalise further
We want to define a new entity, **vector**, to keep and ordered list of numbers.
$$x=\begin{bmatrix}x \\y \\ \end{bmatrix}$$


## System of Linear Equations
$$Ax=b$$

-------------

# Vectors and Matrices
- The numbers are of the same type
	- Integer, Rational, Real, Complex etc.
	- ℂ, ℝ, ℚ, ℤ (SageMath, CC, RR, QQ, ZZ)
	- Not a big deal, because
		 $$ℤ⊂ℚ⊂ℝ⊂ℂ$$
- The numbers need not represent the same physical quantity

------
# Our first Matrix Equation
## $$Ax=b$$
## $$A∈ℝ^{m×n}, x∈ℝ^n , b∈ℝ^m$$
## $$A:ℝ^n ↦ℝ^m$$
