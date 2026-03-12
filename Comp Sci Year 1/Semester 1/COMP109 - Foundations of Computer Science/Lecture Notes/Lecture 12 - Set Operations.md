## Union
The union of two sets, A and B, is the set of all elements contained in either A or B.

Formally, "${A \cup B\; =\; \{x\; |\; x\in A\; or\; x\in B\}}$"

>$\cup$ is the symbol for union.

For Example take the following sets:
- ${A = \{ 1,2,3,4,5\}}$ 
- ${B = \{4,5,6,7,8\}}$
- ${C = \{8,9,10,11,12\}}$

From the definition of union we can see the following:
- ${A \cup B = \{1,2,3,4,5,6,7,8\}}$
- ${B\cup C = \{4,5,6,7,8,9,10,11,12\}}$
- ${A \cup C = \{1,2,3,4,5,8,9,10,11,12\}}$
- ${A\cup B\cup C = \{1,2,3,4,5,6,7,8,9,10,11,12\}}$

Below you can see a Venn diagram of $A\cup B$ 

![[A_U_B_Venn_Diagram.png]]

### Set Union in Python
In python we could write a function to find the union of 2 sets like so:
```
def union (A, B):
	result = set()
	for x in A:
		result.add(x)
	for x in B:
		result.add(x)
	return result
```

As you can see, the above function creates a new empty set, and then iterates through A and B and adds every element of each to this new empty set.

You might think that you could optimise this a little by doing the following:
```
def bad_union (A, B):
	for x in B:
		A.add(x)
	return A
```

However this does **NOT** work. 

While the result set **IS** the union of A and B, python passes mutable objects, like sets, to functions by reference. Understanding exactly what this means is unnecessary for this course, but this essentially means that this function would edit set A as a side effect of the function. 

A set operation like this does not edit sets, it creates a new set, and so you cannot write this program like this.

Python does have a built in operation for this, `A.union(B)`. This does the same thing our union function does. `print(union(A, B)` is exactly the same as `print(A.union(B))`.

### Set Union With Characteristic Vectors 
Let $S = \langle1,2,3,4,5 \rangle,\; A=\{1,3,5\},\; and\; B=\{3,4\}$  

From these sets we can see that $A \cup B=\{1,3,4,5\}$.

When we look at the characteristic vectors of these sets we can see:
- $A = [1,0,1,0,1]$
- $B = [0,0,1,1,0]$
- $A \cup B=[1,0,1,1,1]$

You can see that the characteristic vector of $A \cup B$ contains a 1 in any position that contained a 1 in either $A$ or $B$. 

This means that when a computer is representing sets $A$ and $B$ with characteristic vectors, it can efficiently compute $A \cup B$ using a **bitwise or** operation.
## Intersection
The intersection of 2 sets, A and B, is the set of all elements contained in both A and B.

Formally, "$A \cap B= \{x\;|\;x\in A, x\in B\}$".

>$\cap$ is the symbol for intersection. 
>
>When conditions of a predicate are separated by a comma, it is the same as them being separated by $and$.

For example take the following sets:
- $A=\{1,3,5,9,10\}$
- $B = \{1,8,9,12\}$
- $C=\{8, 10, 12, 13\}$

From the definition of intersection we can see the following:
- $A \cap B= \{1,9\}$
- $B \cap C = \{8, 12\}$ 
- $A \cap C = \{10\}$
- $A\cap B\cap C=\emptyset$

Below you can see a Venn diagram of $A\cap B$
![[A_n_B_Venn_Diagram.png]]
### Set Intersection in Python
In python we can write a function to find the intersection of 2 sets like so:
```
def intersection (A , B ) :
	result = set ()
	for x in A :
		if x in B :
			result . add ( x )
	return result
```

As you can see, the above function creates an empty set before iterating through set A and adding all the elements also in set B to this set. It then returns the new set as the result.

A minor optimisation you can make to this program is to check which set is the smaller of the 2 and always iterate through that one. This results in less checks.

Python does have a built in operation for this `A.intersection(B)` which does the same thing as our function. `print(A.intersection(B))` is exactly the same as `print(intersection(A, B)`.
### Set Intersection and Characteristic Vectors
Let $S = \langle1,2,3,4,5 \rangle,\; A=\{1,3,5\},\;and\; B=\{1,2,3,4\}$  

From these sets we can see that $A\cap B=\{1,3\}$

When we look at the characteristic vectors of these sets we can see:
- $A=[1,0,1,0,1]$
- $B=[1,1,1,1,0]$
- $A\cap B=[1,0,1,0,0]$

We can see that the characteristic vector of $A\cap B$ contains a 1 in all the locations that there is a 1 in the characteristic vectors of both $A$ and $B$. 

This means that when a computer is representing sets $A$ and $B$ with characteristic vectors, it can efficiently compute $A \cap B$ using a **bitwise and** operation.

## Relative Complement or Set Difference/Set-Minus
The relative complement, or set-difference/set-minus, of set A relative to B is the set of all elements that are in A but not in B.

Formally, "$A - B=\{x\; |\; x\in A, x\notin B\}$".

>$-$ is the symbol for set-difference. It is obviously the same symbol used for normal subtractions.

For example take the following sets:
- $A=\{1,3,5,9,10\}$
- $B = \{1,8,9,12\}$
- $C=\{8, 10, 12, 13\}$

From the definition of set-minus we can see:
- $A-B=\{3,5,10\}$
- $B-A=\{8,12\}$
- $B-C=\{1,9\}$
- $C-B=\{10,13\}$
- $A-C=\{1,3,5,9\}$
- $C-A=\{8,12,13\}$
- $A-B-C=\{3,5\}$
- $A-(B-C)=\{3,5,10\}$

>It is important to notice that set difference is not an associative operation. This means that the order matters when performing set difference operations.
>
>In the second to last example, we see $A-B-C$. When there are no parentheses we go from left to right, so $A-B-C=(A-B)-C$.

Below you can see a Venn diagram of $A-B$.
![[A-B_Venn_Diagram.png]]

### Set-Minus in Python
In python we can write a function to find the difference of 2 sets like so:
```
def setMinus (A, B) :
	result = set()
	for x in A:
		if x not in B:
			result.add (x)
	return result
```

As you can see the above program creates an empty set and then iterates through set A adding all the elements not in B to this set before returning this new set.

Python does have a built in method for set minus `A - B`. In python, `print(A - B)` and `print(setMinus(A, B)` are exactly the same.
### Set-Minus with Characteristic Vectors.
Let $S = \langle1,2,3,4,5 \rangle,\; A=\{1,3,5\},\;and\; B=\{3,4\}$ 

From these sets we can see that $A \cup B=\{1,3,4,5\}$.

When we look at the characteristic vectors of these sets we can see:
- $A = [1,0,1,0,1]$
- $B = [0,0,1,1,0]$
- $A - B=[1,0,0,0,1]$
- $B - A=[0,0,0,1,0]$

From this we can see that to find the set difference using characteristic vectors we remove the 1s at any position in the first vector that also contains a 1 in the second vector.

This means that $A - B$ = **bitwise $A$ xor ($A$ and $B$)**. 
## Set Complement
Set complement is similar to relative complement but is used when we are dealing with subsets of some large set, $U$. We call $U$ the universal set or just the "Universe" for the problem in question.

It is formally defined as "$A^c =\{x\;|\;\notin A\}=U-A$"

>The superscript $c$ in $A^c$ is the symbol for complement of. 

U would usually be defined as some infinite set such as $\mathbb{Z}$ or $\mathbb{R}$ as such providing specific examples of complement, in a way that is different to relative complement, is not really possible.

Below you can see a Venn diagram of what $A^c$ looks like, where the highlighted region is $A^c$ and the rectangle is $U$
![[A^c_venn_diagram.png]]
### Set Complement in Python
Similarly to above, where we recognise that providing specific examples is not really possible, it is not possible to program this in python, or rather, that programming this in python requires a defined and finite $U$ and therefore is exactly the same as set minus.
### Set Complement with Characteristic Vectors
Let $S = \langle1,2,3,4,5 \rangle,\; A=\{1,3,5\},\;and\; B=\{3,4\}$

When representing sets as characteristic vectors, $U = S$, and therefore when we look at the characteristic vectors of these sets we can see:
- $A = [1,0,1,0,1]$
- $B = [0,0,1,1,0]$
- $A^c=[0,1,0,1,0]$
- $B^c=[1,1,0,0,1]$

From this we can see that $A^c$  can be computed by using a **bitwise not** operation on $A$.
## Symmetric Difference
The symmetric difference of 2 sets, A and B, is the set of all elements that is in either A or B, but not both.

It is formally defined as "$A \triangle B=\{x\;|\;(x\in{A}\; and\; x\notin{B})\; or\; (x\notin{A}\; and\; x\in{B})\}$"

For example take the following sets:
- $A=\{1,3,5,9,10\}$
- $B = \{1,8,9,12\}$
- $C=\{8, 10, 12, 13\}$

From the definition of Symmetric Difference we can see:
- $A\triangle B=\{3,5,8,10,12\}$
- $B\triangle C=\{1,9,10,13\}$
- $A\triangle C=\{1,3,5,8,9,12,13\}$
- $A\triangle B\triangle C=\{3,5,13\}$

>Note that, unlike set-minus, symmetric difference is an associative operation. This means that $(A\triangle B)\triangle C=A\triangle(B\triangle C)$.
### Symmetric Difference in Python
In python we can write a function that can find the symmetric difference of 2 sets like so.
```
def symmetricDifference(A, B):
	result = set()
	for x in A:
		if not x in B:
			result.add(x)
	for x in B:
		if not x in A:
			result.add(x)
	return result
```

As you can see this function iterates through both sets and adds any elements not contained in the other set to the resulting set.

This can also be done with the following:
```
def symmetricDifference(A, B):
	return A.union(B) - A.intersection(B)
```
This uses pythons union and intersection methods and the set minus operator. It works because symmetric difference is the set of all elements in either set but not in both.

Python does have a built in method for symmetric difference which is `A.symmetric_difference(B)`. This means that `print(A.symmetric_difference(B))` is exactly the same as `print(symmetricDifference(A, B))` using either definition of our `symmetricDifference` function. 
### Symmetric Difference with Characteristic Vectors
Let $S = \langle1,2,3,4,5 \rangle,\; A=\{1,3,5\},\;and\; B=\{3,4\}$

When we look at the characteristic vectors of these sets we can see:
- $A = [1,0,1,0,1]$
- $B = [0,0,1,1,0]$
- $A\triangle B=[1,0,0,1,1]$

From this we can see that when a computer is using bit vectors to represent sets it can compute it efficiently using a **bitwise xor** operation.
### Proving $A\triangle B = (A\cup B) -(A\cap B)$
Earlier we used the identity that $A\triangle B = (A\cup B) -(A\cap B)$. While this may be intuitively true it makes a good case study for how to prove identities with sets.

To prove 2 sets are equal to each other, we need to prove that both sets are subsets of each other.

So first let us prove that $A\triangle B \subseteq (A\cup B) -(A\cap B)$:
	$Let\; x \in A\triangle B$
	This means either that $x\in A\; and\; x \notin B$ or $x\in B\; and\; x \notin A$
	Case 1, $x\in A\; and\; x \notin B$:
		Since $x\in A$ then we know that $x\in A \cup B$
		Since $x \notin B$ then we know that $x\notin A \cap B$
		This means that $x\in (A\cup B) -(A\cap B)$
	Case 2, $x\in B\; and\; x \notin A$:
		Since $x\in B$ then we know that $x\in A \cup B$
		Since $x \notin A$ then we know that $x\notin A \cap B$
		This means that $x\in (A\cup B) -(A\cap B)$
	As both cases show an arbitrary $x \in A\triangle B$ to be in $(A\cup B) -(A\cap B)$ so therefore $A\triangle B \subseteq (A\cup B) -(A\cap B)$

We then must prove that $(A\cup B) -(A\cap B) \subseteq A\triangle B$:
	$Let\; x \in (A\cup B) -(A\cap B)$
	By definition of "$-$" $x\in A\cup B\; and\; x\notin A\cap B$
	By definition of "$\cup$" $x\in A\; or\; x\in B$
	As $(x\in A\; or\; x\in B)\; and\; x\notin A\cap B,\; x$ is in exactly one of $A\; or\; B$.
	This means either that $x\in A\; and\; x \notin B$ or $x\in B\; and\; x \notin A$
	As an arbitrary $x\in (A\cup B) -(A\cap B)$, also exists in $A\triangle B$, this shows that $(A\cup B) -(A\cap B) \subseteq A\triangle B$.

As both sets are subsets of each other, they must be equivalent.
