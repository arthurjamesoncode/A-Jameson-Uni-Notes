### Introduction and Notation
A set is a collection of objects. These objects are called the *elements* of the set. 

For example:
- {7, 5, 3}
- {Liverpool, Manchester, Leeds}

You can see from these examples that when we write down a set we write down the elements of the set, separated by commas and surrounded by curly braces.

We write ${a \in A}$ to denote that $a$ is an element of the set $A$. $\in$ means "is an element of".

So:
- 7 $\in$ {7, 5, 3}
- 4 $\notin$ (7, 5, 3)

In a set, the order of an element does not matter, and there are no repetitions.

So, {7, 5, 3} is the same as {3, 5, 7} or {3, 7, 3, 5, 7, 7, 7}.

For large, or infinite sets, we cannot write down sets in this way and instead use a predicate *P(x)*. So we write sets like: "*A = { ${x \in S\;|\;P(x)}$ }"

For example "{...,-2,-1, 1, 3, 5, 7,...}" would be "*A = {${x \in \mathbb{Z}}$ | $x$ is odd}*" or more formally "*A = {${x\in \mathbb{Z}\; |\;x=2n+1,\; n\in\mathbb{Z}}$}".

Some more examples:
- A = {${x\in\mathbb{Z}\; |\; x^2+4x=12}$} = {-6, 2}
- B = {${n^2\; |\; n\in \mathbb{Z}}$} = {0, 1, 4, 9, 16,...}
- C = {${x\; |\; x}$ is an English day of the week not containing "u"} = {Monday, Wednesday, Friday}
### Important Sets
Here are some important sets and their notation. You have seen many of these before.

- $\emptyset$  means the empty set, this set contains no elements.
- $\mathbb{N}$ means the natural numbers, {0, 1, 2, 3, ...}.
- $\mathbb{Z}$ means the integers, {..., -2, -1, 0, 1, 2, ...}.
- $\mathbb{Z^+}$ means the positive integers. The + superscript can be applied to any of these sets to mean only the positive elements.
- $\mathbb{Q}$ means the rationals, {${\frac{x}{y}\; |\; x\in\mathbb{Z},\; y\in\mathbb{Z},\; y\neq 0}$}.
- $\mathbb{R}$ means the reals. 
- \[a, b] means the set of real numbers between a and b inclusive, {${x\in\mathbb{R}\; |\; a \leq x \leq b}$}.

### Computer Representation of Sets
Sets are the most elementary data structures, although they don't always map well onto hardware. Some modern programming languages include sets by default.

In computer representation of sets, only finite sets can be represented. Some modern representations of sets, in languages such as Python and JavaScript, use hash-tables in order to implement them. This is because sets in this languages are not limited to a certain type, and can contain any hashable element such as strings, integers, or tuples.

Older representations of sets, which are limited to a single data type, use characteristic vectors. This may also be done because these vectors are more efficient to perform computations with, although that is only necessary for demanding algorithms.

When not represented with a hash table, all the elements of A are drawn from some ordered sequence, S, where S = ⟨${s_1,\; ... ,\; s_n}$⟩. The characteristic vector of A is the sequence \[${b_1,...,b_n}$] where ${b_i}$ is 1 if ${s_i\in}$ A and ${b_i}$ is 0 if ${s_i\notin}$ A.

We refer to sequences of 1s and 0s as bit strings, bit vectors, or bit arrays.

For example, let S = ⟨1, 2, 3, 4, 5⟩, A = {1, 3, 5} and B = {3, 4}.  
- The characteristic vector of A is \[1, 0, 1, 0, 1].  
- The characteristic vector of B is \[0, 0, 1, 1, 0].  
- The set characterised by \[1, 1, 1, 0, 1] is {1, 2, 3, 5}.  
- The set characterised by \[1, 1, 1, 1, 1] is {1, 2, 3, 4, 5}.  
- The set characterised by \[0, 0, 0, 0, 0] is $\emptyset$.

## Relations Between Sets
### Subsets
A set, $A$,  is called a subset of a set, $B$, if every element of $A$ is an element of $B$. This is shown by $A\subseteq{B}$ 

For Example:
- {3, 4, 5} ⊆ {1, 5, 4, 2, 1, 3}
- {3, 3, 5} ⊆ {3, 5}
- {5, 3} ⊆ {3, 5}.

In python we could check if a set is a subset of another set by doing the following:
```
def isSubset (A , B ) :  
	for x in A :  
		if x not in B :  
			return False  
	return True  
```

As you can see above we loop through all the elements of A and return False if any of them are not in B.

There is an inbuilt operation in python `A < B` which is identical. `print(isSubset(a, b)` is the same as `print(a < b)` when a and b are both sets.

### Equality
A set A is called equal to a set B if A ⊆ B and B ⊆ A. This is denoted by A = B.

For Example:
	{1} = {1, 1, 1},  
	{1, 2} = {2, 1},  
	{5, 4, 4, 3, 5} = {3, 4, 5}.

If 2 sets are equal it means they are the same set.