## Equivalence Relations Continued
We covered equivalence relations pretty thoroughly in last lecture, [[Lecture 23 - Transitive Closures and Equivalence Relations]], but now we are just going to prove a few theorems regarding equivalence classes.
### First Proof
The theorem we will prove is this: Let $R$ be an equivalence relation on a non-empty set $A$. If this is true the equivalence classes of $R$, $\{E_x\;|\;x\in A\}$, form a partition of $A$.

To prove this we need the following definitions:
- **Partition of $A$ -** A group of non-empty subsets of $A$ which contain all elements of $A$ and are disjoint from each other.
- **Equivalence Relation -** An relation on a set $A$ which is reflexive, symmetric and antisymmetric.
- **Equivalence Class -** $E_x=\{y\;|\;yRx\},\;x,y\in A$

So now we need to prove that the properties of a partition hold, based on the properties of an equivalence relation and an equivalence class.

First we will show that the equivalence classes $E_x$ are non-empty subsets of $A$:
	By definition of an equivalence class $E_x=\{y\in A\;|\;yRx\},\;x\in A$.
	By definition of an equivalence relation, $R$ is reflexive.
	Since $R$ is reflexive and $E_x$ is defined as all the elements related to $x$, $E_x$ must be non-empty since $xRx$. 
	We know that $E_x\subseteq A$ since $x,y\in A$.
	Therefore each equivalence class $E_x$ must be a non empty subset of $A$.

Next we need to show that $A$ is the union of all the equivalence classes:
	We have just shown that $\forall x\in A,\;E_x\subseteq A$.
	This means that the union of the equivalence classes is a subset of $A$.
	We also know that $x\in A$ implies that $x\in E_x$. So any arbitrary $x\in A$ must be present in an equivalence class and therefore $A$ is a subset of the union of the equivalence classes.
	Therefore, as the union of all $E_x$ is a subset of $A$, and $A$ is a subset of the union of all $E_x$ we know that $A$ must be the same as the union of all $E_x$.

Next we need to show that distinct equivalence classes are disjoint. 

We do this by first showing that if $xRy$ then $E_x=E_y$:
	Suppose that $xRy$ and let $z\in E_x$.
	By definition of $E_x$ we know $zRx$.
	By definition of equivalence relation, $R$ is transitive and symmetric.
	Since $R$ is a transitive relation, $zRx$, and $xRy$ it must be that $zRy$.
	Therefore it must be that $z\in E_y$ by definition of $E_y$ and since $z$ is arbitrary this means that $E_x\subseteq E_y$.
	Since R is symmetric we know $yRx$.
	Let $z\in E_y$.
	By definition of $E_y$ we know $zRy$.
	Since $R$ is a transitive relation, $zRy$, and $yRx$ it must be that $zRx$.
	Therefore it must be that $z\in E_x$ by definition of $E_x$ and since $z$ is arbitrary this means that $E_y\subseteq E_x$.
	Since $E_y\subseteq E_x$ and $E_x\subseteq E_y$, it must be that if $xRy$ then $E_x=E_y$

Next we show that if 2 equivalence classes are not disjoint then they are identical:
	Let $z\in E_x\cap E_y$.
	By definition of $E_x$ and $E_y$ it must be that $zRx$ and $zRy$
	Since $R$ is symmetric, it must be that $xRz$.
	Since $R$ is transitive and $xRz$ and $zRy$, it must be the case that $xRy$.
	Therefore, since $xRy$, $E_x=E_y$.
	This shows us that if 2 equivalence classes are not disjoint then they are the same.

We have now proved that all of the properties of a partition hold for the equivalence classes, and thus the equivalence classes must form a partition of $A$.
### Second Theorem
The next theorem we will prove is this: "Suppose that $A_1,...,A_n$ is a partition of $A$ define a relation $R$ on $A$ by setting $xRy\iff\exists i\text{ such that }1\leq i\leq n\text{ and }x,y\in A_i$. Then $R$ is an equivalence relation."

To prove this statement we need to show that this relation $R$ holds the properties of an equivalence relation.

First we prove reflexivity:
	If $x\in A$ then $x\in A_i$ for some value $i$.
	Therefore $xRx$, meaning that $R$ must be reflexive.

Next we prove transitivity:
	If $xRy$ and $yRz$ then there exists $A_i$ and $A_j$ such that $x,y\in A_i$ and $y,z\in A_j$.
	This means that $y\in A_i\cap A_j$.
	Since $A_i$ and $A_j$ form a partition of $A$, $y\in A_i\cap A_j\implies i=j$.
	Therefore $x, z\in A_i$ meaning that $xRz$.
	Therefore $R$ is transitive.

Last we prove symmetry:
	If $xRy$ then $\exists A_i\text{ such that }x,y\in A_i$
	$x,y\in A_i\implies yRx$
	Therefore $R$ must be symmetric.

As $R$ is reflexive, transitive, and symmetric, $R$ must be an equivalence relation.
## Partial Orders
Another important relation is Partial Orders.

A binary relation $R$ on a set $A$ which is **reflexive**, **transitive** and **antisymmetric** is called a partial order.

Partial orders are important in situations where we wish to characterise precedence.

Examples of Partial Orders are:
- The relation $\leq$ on the set of real numbers, $\mathbb{R}$
- The relation $\subseteq$ on Pow(A);
- The relation "is a divisor of" on the set $\mathbb{Z^+}$

If $R$ is a partial order on a set $A$ and $xRy,\;x\neq y$ then we call $x$ a predecessor of $y$.

If $x$ is a predecessor of $y$ and there is no $z\notin \{x,y\}$ for which $xRz$ and $zRy$, then we call $x$ an immediate predecessor of $y$.

The important thing to know with partial orders is that everything can be related to something in front of it, and is related to itself, but nothing is related to anything behind it.
### Hasse Diagram
The Hasse Diagram of a partial order is a digraph. The vertices of the digraph are the elements of the partial order, and the edges show the immediate predecessor relation.

Let $A=\{1,2,3\}$ or any other 3 element set, the following is an image of a Hasse Diagram representing the relation $\subseteq$ on Pow(A), with each vertex being a bit vector showing the elements it contains:
![[hasse_diagram_partial.png]]
It is common to assume the arrows point up. As you can see from here we have the empty set at the bottom, which is related to everything, and the complete set at the top which is related to nothing, except itself.

>It's important to remember that the edges on the Hasse Diagram of a partial order only show the immediate predecessors.
>
>Despite there not being an edge to show it, every element is still related to itself, and elements further down the chain of descendants.
## Total Orders
A binary relation $R$ on a set $A$ is a total order if it is a partial order such that for any $x,y\in A,\; xRy$ or $yRx$.

A total order has 1 order that everything fits into. A Hasse Diagram of a total order is a chain.

If we look back at the Hasse Diagram for $\subseteq$ on $Pow(A)$ then we can see that some elements are not related. $[0,1,0]$ is not a subset of $[1,0,1]$ for example.

This is never the case in a total order.

All total orders are also partial orders, but not all partial orders are total orders.

For examples of total orders:
- The relation $\leq$ on the set of real numbers, $\mathbb{R}$.
- The lexicographical ordering of the words in a dictionary.
## $n$-ary relations
The Cartesian product $A_1\times A_2\times ... \times A_n$ of sets $A_1,A_2,...,A_n$ is defined as $A_1\times A_2\times ... \times A_n=\{(a_1,...,a_n)\;|\;a_1\in A_1,...,a_n\in A_n\}$.

Here $(a_1,...,a_n)=(b_1,...,b_n)\iff a_i=b_i\;\forall i\text{ such that }1\leq i\leq n$.

$n$-ary relations simply connect $n$ elements from $n$ sets, instead of 2 elements like binary relations do. Because of this an $n$-ary relation is a subset of $A_1\times A_2\times ... \times A_n$.
### Database Tables
Look at the example database table below:
![[db_example.png]]
The above table is an $n$-ary relation. It is a subset of $\{\text{Student names}\}\times\{\text{ID numbers}\}\times\{\text{Majors}\}\times\{\text{Float}\}$.

## Unary Relations:
Unary relations are just subsets of a set.

For example $\{x\in \mathbb{Z^+}\;|\;x\text{ is even}\}$ is a unary relation.
