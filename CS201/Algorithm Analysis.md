# How to determine a good algorithm
## Is it correct?
- Tests
- Proofs
## Is it efficient?
- Experiments
- Analyses

## Measuring Performance
### Empirically
- Implementation must be available
- Hardware and software environments must be controlled
- Experiments can only be done over limited set of inputs

### Analytically
- Avoid having to implement first
- Independent of hardware and software
- Accounts for all inputs

## What do we count?
### Primitive operations
Assigning values to variables, performing operations, comparisons, accessing arrays, etc…
The cost of this depends on the operation. Can range from n(1) for assigning to larger costs for methods like `.contains()

## Counting
Usage of product and sum rule or permutations and combinations.

----

## Growth Rate of Functions
[[Constant Function]]
[[Logarithm Function]]
[[Linear Function]]
[[Linearithmic Function]]
[[Polynomial Function]]
[[Exponential Function]]

----
## Asymptotic Analysis
Used to measure performance "in the limit"
[[Big O Notation]]
[[Big Omega Notation]]
[[Big Theta Notation]]