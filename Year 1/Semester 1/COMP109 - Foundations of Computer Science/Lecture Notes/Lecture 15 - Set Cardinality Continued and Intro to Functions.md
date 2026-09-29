## Set Cardinality Continued
### Computing the Cardinality of the Union of 3 Sets
When computing the cardinality of three sets, we can use the following formula:

$|A\cup B\cup C|=|A|+|B|+|C|-|A\cap B|-|A\cap C| - |B\cap C| + |A\cap B\cap C|$

We can show this, but first we need to label all of these regions like so:
![[cardinality_a_u_b_u_c.png]]

From the above diagram we can see:
- $|A| = n_a+n_{ab}+n_{ac}+n_{abc}$
- $|B| = n_b+n_{ab}+n_{bc}+n_{abc}$
- $|C| = n_c+n_{ac}+n_{bc}+n_{abc}$
- $|A\cap B| = n_{ab}+n_{abc}$
- $|A\cap C| = n_{ac}+n_{abc}$
- $|B\cap C| = n_{bc}+n_{abc}$
- $|A\cap B\cap C|=n_{abc}$
- $|A\cup B\cup C| = n_a+n_b+n_c+n_{ab}+n_{ac}+n_{bc}+n_{abc}$

Using $x,y,z$ as arbitrary labels we can see:
- $x = |A|+|B|+|C|=n_a+2n_{ab}+2n_{ac}+2n_{bc}+3n_{abc}$
- $y=|A\cap B| + |A\cap C| + |B\cap C| = n_{ab} + n_{ac} + n_{bc} + 3n_{abc}$
- $z = |A\cap B\cap C| = n_{abc}$

We can see that $x$ contains too many copies of $n_{ab},n_{ac},n_{bc},\; and\; n_{abc}.$ To try and fix this we can subtract $y$. However $x-y=$ $n_a+n_b+n_c+n_{ab}+n_{ac}+n_{bc}.$ and is now missing $n_{abc}$. To fix this we need to add $z$.

So $|A\cup B\cup C|=x-y+z=|A|+|B|+|C|-|A\cap B|-|A\cap C| - |B\cap C| + |A\cap B\cap C|$.

This is a special case of the principle of inclusion and exclusion.

### The Principle of Inclusion and Exclusion
The principle of inclusion and exclusion states that the cardinality of the union of $n$ sets is the same as the sum of the cardinality of all the individual sets, minus the sum of the cardinality of all of the 2 way intersections, plus the sum of the cardinality of all the 3 way intersections and so on.

Essentially, for all intersections between an odd number of sets, you add the cardinality. On the other hand, for all intersections between an even number of sets you subtract the cardinality.

Formally, it is defined below
	Let $A_1, A_2,...,A_n$ be sets.
	Then $|A_1\cup\;...\cup A_n|=$
	$\sum_{1\leq i\leq n} |A_i|$ 
	$-\sum_{1\leq i<j\leq n} |A_i\cap A_j|$
	$+\sum_{1\leq i<j<k\leq n} |A_i\cap A_j\cap A_k|$
	$-...$
	$+(-1)^{n-1}|A_1\cap ... \cap A_n|$.
### Russell's Paradox
This set theory is called "Naïve Set Theory". Why is it naïve?

It is naïve because it contains paradoxes.

Russell's Paradox, discovered by Bertrand Russell in 1901, shows that the "object" $\{x\; |\; P(x)\}$ is not always meaningful, or possible.

Take for example the set $A = \{B\; |\; B \notin B\}$. So $A$ is defined as the set of all sets which don't contain themselves.

Now we simply ask, do we have $A\in A$?

If we define $P(C)$ as $C \notin C$, we can see that $A = \{B\; |\; P(B)\}$.

Well lets look at 2 cases, $A\in A\; and\; A \notin A$.
	Case 1, $A\in A$:
		In this case it is true that $A\in A$. 
		However since $A\in A$, it means $P(A)$ is false and therefore it must be that $A\notin A$.
		This is a paradox.
	Case 2, $A\notin A$:
		In this case, since $A\notin A$, $P(A)$ is true.
		Therefore it must be the case that $A\in A$.
		This is a paradox.
	As we can see this paradox proves that this notation is not rigorous enough, as paradoxes can exist when the predicate of a set references itself.
## Functions
Functions in maths connect 2 sets, A and B. 

A function from a set A to a set B is an assignment of exactly one element of B to each element of A.

We can write $f(a)=b$ if $b$ is the chosen element of B assigned by the function to the element $a$.

if $f$ is a function from $A$ to $B$ we write $f: A \to B$.

For example if we take the following sets:
- $A=\{1,2,3\}$
- $B = \{4,5,6\}$

We can define a function from $A$ to $B$ like so:
- $f(1)=4$
- $f(2)=5$
- $f(3)=4$

>Notice that the above function has multiple values that map to 4. This is still a function as each value on the left, maps to exactly 1 value on the right. Though values on the right can be mapped to by multiple values on the left.

Functions are a type of relation. For a relationship from $A\to B$ to be functional 2 properties must hold:
- Each value of $A$ must map to a value from $B$.
- Each value of $A$ must only map to one value from $B$.

So if we instead defined sets $A$ and $B$ like so:
- $A=\{1,3,5,7\}$
- $B=\{2,4,6\}$

If we define a function $g: A \to B$ like so:
- $g(1)=2$
- $g(3)=4$
- $g(5)=6$

We have **NOT** defined a valid function as there is no mapping from $7$ to an element of $B$.

Similarly if we define a function $g: A \to B$ like so:
- $g(1) = 2$
- $g(1) = 6$ 
- $g(3) = 4$
- $g(5)=6$
- $g(7)=6$

Again we have **NOT** defined a valid function as there are multiple mappings from $1$ to different elements of $B$.
### Domain, Codomain, and Range
If we have a function, $f: A \to B$. We call $A$ the domain, and $B$ the codomain.

We also define the range of $f$ as $f(A)=\{f(x)\; |\; x\in A\}$.

Essentially the range is a subset of $B$ and is the set of all the actual outputs of the function.

You may wonder why we work with a codomain at all and not just the range. This is simply because the range of a function may not always be easy to determine, but we can guarantee that a function will only ever map to values within the codomain.
### Composition of Functions
If $f: X\to Y\;$and $g: Y\to Z$ then we can compose $f$ and $g$.

The composition of these functions, $g \circ f$, is a function from $X \to Z$ given by $(g\circ f)(x) = g(f(x))$

Take the following functions:
- $f: \mathbb{R} \to \mathbb{R}$ given by $f(x) = x^2$
- $g: \mathbb{R} \to \mathbb{R}$ given by $g(x) = 4x+3$

These functions can be composed as follows:
- $g\circ f(x)=g(x^2)=4x^2+3$
- $f\circ g(x)=f(4x+3)=16x^2+24x+9$
- $f\circ f(x)= f(x^2) = x^4$
- $g\circ g=g(4x+3)=4(4x+3)+3=16x+15$


