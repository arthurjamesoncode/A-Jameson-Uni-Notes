The cardinality of a finite set, $A$, is the number of distinct elements in $A$, and is denoted by $|A|$. It is essentially the size of the set.
## Cardinality of the Power Set
The power set, Pow(A), of a set, A, is defined as the set of all subsets of A.

Formally, $Pow(A)=\{C\;|\;C\subseteq A\}$.

For all $n\in\mathbb{N}$ and all sets $A$: if $|A|=n$, then $|Pow(A)|=2^n$.

If we look at an example we can see the reason for this. 

Take the following set: $X=\{1,5,9\}$. We can see that:
- $|X|=3$
- $Pow(X)=\{\emptyset, \{1\},\{5\},\{9\},\{1,5\},\{1,9\},\{5,9\},\{1,5,9\}\}$
- $|Pow(X)|=8=2^3$

We can see that the property holds for the above set but it might not be clear why this holds so far, The power set contains every possible combination of elements from the original set, including the whole set and the empty set.

If we set $S=\langle1,5,9\rangle$ and represent the sets in the power set as characteristic vectors we can see why this is the case.

The characteristic vectors are as follows
- $\emptyset=[0,0,0]$
- $\{1\} = [1,0,0]$
- $\{5\} = [0,1,0]$
- $\{9\} = [0,0,1]$
- $\{1,5\} = [1,1,0]$
- $\{1,9\} = [1,0,1]$
- $\{5,9\} = [0,1,1]$
- $\{1,5,9\} = [1,1,1]$

We can see that each set in $Pow(A)$ corresponds to a different bit string of length 3, which is $|X|$, and that every possible bit string of length 3 is represented. 

This means that $|Pow(X)|$ is equal to the number of distinct bit strings of length $|X|$. Since the number of distinct bit strings of length $n$ is $2^n$ this means that $|Pow(X)|=2^{|X|}$. 

The only thing not covered by this revelation is that the $|Pow(\emptyset)|$ is 1 since $|\emptyset|=0$ and you cannot have a bit string of length 0. But since $Pow(\emptyset)=\{\emptyset\}$ we can see that the cardinality of $|Pow(\emptyset)|$ is 1. 
### Proving the number of $n$-bit vectors is $2^n$.
To prove the number of $n$-bit vectors is $2^n$ we can use induction.

So:
	Base Case, $n=1$:
		When $n=1$ there are $2$ possible bit strings, \[0] and \[1].
		Since $2^1=2$ this property holds for the base case of 1.
	 Inductive Step:
		Assume that there are $2^m$ possible bit vectors when $n=m$.
		Let $[x_1,x_2,x_3,...,x_m,x_{m+1}]$ be a bit vector of length $m+1$ and $X$ be the set of all values of $[x_1,x_2,x_3,...,x_m,x_{m+1}]$.
		From our assumption, we know that there are $2^m$ possible values for $[x_1,x_2,x_3,...,x_m]$.
		Since $x_{m+1}$ has 2 possible values, 0 and 1, we know that $X$ contains exactly $2^m$ bit vectors that end in 0, exactly $2^m$ bit vectors that end in 1, and nothing else.
		Therefore $|X|=2^m+2^m=2\cdot 2^m=2^{m+1}$.
		This shows that if the property is true for $n=m$ then it is true for $n=m+1$.
	As the property holds for both our base case and inductive step it shows that the property must be true for all $n\in\mathbb{Z^+}$.
## The Cardinality of the Union of Two Sets
We can compute the cardinality of the union of two sets, $A$ and $B$, if we know $|A|$, $|B|$, and $|A\cap B|$.

This is because $|A\cup B|=|A|+|B|-|A\cap B|$.

To show this we can look at the following diagram.
![[cardinality_a_u_b.png]]

In this diagram we can see 2 sets $A$ and $B$. $n_a$ represents the cardinality of all the elements that are only in $A$. $n_b$ represents the cardinality of all the elements that are only in $B$. $n_{ab}$ represents the cardinality of all the elements that are in $A \cap B$.

So from this we know the following:
- $|A|=n_a+n_{ab}$
- $|B|=n_b+n_{ab}$
- $|A \cap B|=n_{ab}$
- $|A\cup B|=n_a+n_b+n_{ab}$

Here we can see that: 
	$|A|+|B|=n_a+n_b+2n_{ab}$ 

And so to get $|A\cup B|$ we must do this:
	$|A|+|B|-|A\cap B|=n_a+n_b+n_{ab}$

Putting this to use we can answer the following question:
	Suppose there are 100 third-year students. 40 of them take the module “Sequential Algorithms” and 80 of them take the module “Multi-Agent Systems”. 25 of them took both modules. How many students took neither modules?

This question is essentially asking the following:
	Let $U =$ The set of all third year students.
	Let $A=$ The set of all third year students taking the "Sequential Algorithms" module.
	Let $B =$ The set of all third year students taking the "Multi-Agent Systems" module.
	Given $|U|=100,\; |A|=40,\; |B|=80,\; and\; |A\cap B|=25$, calculate $|(A\cup B)^c|$.

We can do this using the rule above:
	$|A\cup B| = |A| + |B| - |A\cap B|$
	Therefore $|A\cup B| = 40 + 80 - 25=95$
	This means that $|(A\cup B)^c|=100-95=5$

And so we know that only 5 students took neither module.