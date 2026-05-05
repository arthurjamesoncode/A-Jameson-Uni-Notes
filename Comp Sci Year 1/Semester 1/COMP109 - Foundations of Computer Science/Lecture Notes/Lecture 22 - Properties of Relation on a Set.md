There are a number of useful properties we can use to describe relations on a set. 

It's important to recognise that these properties are only possible when a relation is on a set and not between sets. So these properties are only valid for $R\subseteq A\times A$ and not $R\subseteq A\times B$.
## Properties
### Reflexive Relations
A binary relation $R$ on a set $A$ is reflexive when $\forall x\in A,\;xRx$.

This means there cannot be an element in $A$ that is not related to itself by $R$. 

It is important to note that even if $R$ only contains elements $x$ for which $xRx$ is true, it still may not be reflexive if there is an element of $A$ that is not related to anything in $R$.
### Symmetric Relations
A binary relation $R$ on a set $A$ is symmetric when $\forall x,y\in A,\;xRy\implies yRx$.

This means if a $(x,y)\in R$ then also $(y,x)\in R$.

### Antisymmetric Relations
A binary relation $R$ on a set $A$ is antisymmetric when $\forall x, y\in A,\;xRy\;\land\;yRx\implies x=y$.

This means that if an element $x$ is related to a different distinct element $y$, that $y$ is not related to $x$.

It is important to note that a relation can be both reflexive and antisymmetric as elements being related to themself means nothing in terms of being antisymmetric.
### Transitive Relations
A binary relation $R$ on a set $A$ is transitive when $\forall x, y, z\in A,\;xRy\;\land\;yRz\implies xRz$.

This means that if an element $x$ is related to an element $y$, and $y$ is related to an element $z$, that $x$ is also related to $z$.

It is important to note that $x=z$ can be true. So if $xRx\land yRx$ is true then $xRx$ must also be true.  
## Classifying Relations
Lets look at some relations on sets and see which properties hold for them.
### $R=\{(x,y)\in \mathbb{Z^+}\times\mathbb{Z^+}\;|\;x \text{ divides } y\}$ 
This is the **"divides by"** relation on the set of positive integers.

We know the following about this relation:
- This relation is **reflexive** as every integer divided by itself is 1.
- This relation is not **symmetric** as $4R2$ is true but $2R4$ is not.
- This relation is **antisymmetric** as smaller numbers can never divide by larger numbers, and unless 2 numbers are the same one must be larger and one must be smaller.
- This relation is **transitive** as any number that divides by another, will also divide by factors of that number.

>Note how we can show that this relation is not symmetric by just providing a counter example. We can do the same thing for all of these, since they are all universal (or "for all") statements.
### $R=\{(x,y)\in \mathbb{Z}\times\mathbb{Z}\;|\;x\neq y\}$
This is the **not equal too** relation on the set of integers.

We know the following about this relation:
- This relation is not **reflexive** as $1\neq 1$ is false.
- This relation is **symmetric** as if any number $x$, is not equal to another number $y$, it will also be true that $y\neq x$.
- This relation is not **antisymmetric** as $1\neq 2$ and $2\neq 1$ are both true.
- This relation is not **transitive** as $1\neq 2$ and $2\neq 1$ are true but $1\neq 1$ is false.

>Notice how we used examples to show that these properties weren't true. 
>
>Also notice that the example to show this relation isn't transitive uses an example where $xRy\land yRx$ is true but $xRx$ is false.

### $R=\{(x,y)\in People\times People\;|\;x\text{ is the same age as } y\}$
This is the **is the same age as** relation on the set of people.

We know the following about this relation:
- This relation is **reflexive** as everyone is the same age as themselves.
- This relation is **symmetric** as if any person $x$ is the same age as another person $y$, it will also be true that $y$ is the same age as $x$.
- This relation is not **antisymmetric** as if any person $x$ is the same age as another person $y$, it will also be true that $y$ is the same age as $x$, even when $x\neq y$.
- This relation is **transitive** as if any person $x$ is the same age as another person $y$, and $y$ is the same age as another person $z$, then $x$ must be the same age as $z$.

>Notice how, in this case, I didn't give a specific example to show it is not antisymmetric, but instead mirrored the reasoning for symmetry with the added case of $x\neq y$. 
>
>It is possible for a relation to be both symmetric and antisymmetric, but only in cases when distinct elements are not related to each other.

## Digraph Representations
In the directed graph representation, $R$ is:
- *Reflexive* if there is always an arrow from every vertex to itself
- *Symmetric* if whenever there is an arrow from x to y there is also an arrow from y to x
- *Antisymmetric* if whenever there is an arrow from x to y and x , y, then there is no arrow from y to x
- *Transitive* if whenever there is an arrow from x to y and from y to z there is also an arrow from x to z.
### Classifying Digraph Relations
#### Example 1:
Let $A=\{1,2,3\},\;R=\{(1,1),(2,2),(3,3),(2,3),(3,2)\}$

This is represented by the following digraph:
![[property_digraph1.png]]
This graph holds the following properties:
- It is **reflexive**
- It is **symmetric**
- It is not **antisymmetric**
- It is **transitive**
### Example 2:
Let $A=\{1,2,3\},\;R=\{(2,2),(3,3),(2,3),(3,2)\}$

This is represented by the following digraph:
![[property_digraph2.png]]

This graph holds the following properties:
- It is not **reflexive**
- It is **symmetric**
- It is not **antisymmetric**
- It is **transitive**
### Example 3:
Let $A=\{1,2,3\},\;R=\{(1,1),(2,2),(3,3),(1,3)\}$

This is represented by the following digraph:
![[property_digraph3.png]]

This graph holds the following properties:
- It is **reflexive**
- It is not **symmetric**
- It is **antisymmetric**
- It is **transitive**
### Example 4
Let $A=\{1,2,3\},\;R=\{(1,3),(3,2),(2,3)\}$

This is represented by the following digraph:
![[property_digraph4.png]]

This graph holds the following properties:
- It is not **reflexive**
- It is not **symmetric**
- It is not **antisymmetric**
- It is not **transitive**

## Reachability Relation
The reachability relation, $R$, is a relation on a set $A$ that requires a different relation, $S$, on a set $A$. An element, $x$, can reach another element $z$, if $xSz$ or if there exists an element $y$ such that $xSy\land yRz$. 

Essentially if, $x$ can reach $z$ if $x$ is related to $z$, or if $x$ is related to an element that can reach $z$. This relation is recursive, meaning it mentions itself in its definition, so it might be a bit more difficult to understand without a graph.

Take the following graph to represent $S$:
![[reachable_digraph.png]]

Using this graph we can define the reachability relation $R$ as:$$
R=\{(1,1),(1,2),(1,4),(1,5),(1,6),(2,1),(2,2),(2,4),(2,5),(2,6),(3,3),(4,1),(4,2),(4,4),(4,5),(4,6),(5,5),(6,1),(6,2),(6,4),(6,5),(6,6)\}
$$