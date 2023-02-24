# Definition
This is an upper bound concept.
We let f(n) and g(n) be functions that map positive integers to real positive numbers.

We can say f(n) is O(g(n)) if there is a real constant c > 0 and integer constant $n_0 >= 1$
for which the following holds:
$$f(n) <= c\times g(n) for n>=n_0$$

----
## Properties
### We can drop constants
e.g.
### $$f(n) = 4n$$$$g(n) = n$$
Then for $$ c =5\space and\space n_0 = 1$$
we have
### $$f(n) <= c\times g(n)$$
### We can also drop the less dominant terms
e.g.
### $$f(n) = n^2+nlogn$$$$g(n)=n^2$$
for
### $$n>=1$$
we have
### $$n<=n$$
hence
### $$f(n)=n^2 + nlogn <=2n^2$$
### If f(n) is a polynomial of degree d, then f(n) is $$O(n^d)$$
### $$f(n) = a_0 + a_1n + a_2n^2 + a_3n^3 + ... + a_dn^d$$
for n >= 1, we have
### $$n<=n^2<=...<=n^d$$
