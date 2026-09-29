We consider there to be a "relation" between two things if there is some connection between them.

For Example:
- Peter is a **friend of** John
- a **is less than** b
- m **divides** n

Relations are used in many branches of mathematics and many ways in computer science.

>For an example of relations in computer science think of the tables in a relational database.
## Ordered Pairs & Cartesian Product
Ordered pairs are a 2 element tuple in which order matters, i.e. $(1,3) \neq (3,1)$.

The Cartesian Product, $A\times B$, of sets, A and B, is the set consisting of all pairs $(a ,b)$ where $a\in A$ and $b\in B$.

Formally: $A\times B=\{(a,b)\;|\;a\in A\; and\; b\in B\}$.

>Note that $(a,b)=(c,d)\iff a=c\;and\; b=d$. Unlike sets, order does matter.

For Example:
	Let $A=\{1,2\},\; B=\{a,b,c\}$. This means that
	$A\times B=\{(1,a),\;(1,b),\;(1,c),\;(2,a),\;(2,b),\;(2,c)\}$
	$B\times A=\{(a,1),\;(b,1),\;(c,1),\;(a,2),\;(b,2),\;(c,2)\}$

>Note that the order of $A$ and $B$ matter. $A\times B\neq B\times A$. 
>
>$\times$ is not a commutative operation.

## Binary Relations
A binary relation between two sets, $A$ and $B$, is a subset, $R$, of $A\times B$. If $A=B$ then $R$ is called a binary relation on $A$.

Essentially a binary relation relates a number of elements from $A$ to a number of elements from $B$ using ordered pairs. 
### Example 1:
Take this family tree:
![[Family Tree.png]]
If we call the set of all these people in this tree $T$ we can define a number of binary relations on $T$.
 $$R=\{(x,y)\in T \times T\; |\; x\; is\; a\; grandfather\; of\; y\} = \{(Fred,\; Jane), (Fred,\;Fiona), (Fred,\; Mavis)\}$$
 $$S=\{(x,y)\in T\times T\; |\; x\; is\; a\; sister\; of\; y\} = \{(Alice,\; Ken), (Sue,\; Mike), (Sue,\; Penny), (Penny,\; Sue),(Penny,\; Mike),(Jane,\;Fiona),(Jane,\;Alan),(Fiona,\;Jane),(Fiona\;Alan)\}$$

>Notice how these pairs relate 2 elements but in 1 direction. In the second example, both $(Sue, Penny)$ and $(Penny, Sue)$ need to exist since both "Sue is a sister of Penny" and "Penny is a sister of Sue" are true.
### Example 2:
Let $A = \{1,3,5,7\}, B = \{2,4,6\}$, $U= \{(x,y)\in A\times B\;|\;x+y=9\}$, $V=\{(x,y)\in A\times B\;|\;x<y\}$.

We can also represent $U$ and $V$ as the following sets of ordered pairs:
- $U=\{(3,6),(5,4),(7,2)\}$
- $V=\{(1,2),(1,4),(1,6),(3,4),3,6),(5,6)\}$
### Example 3:
Let $A=\{1,2,3,4,5,6\}$, $R=\{(x,y)\in A\times A\; |\;x\; is\; a\; divisor\; of \;y\}$.

We can also represent $R$ as the following set of ordered pairs:
$$R=\{(1,1),(1,2),(1,3),(1,4),(1,5),(1,5),(2,2),(2,4),(2,6),(3,3),(3,6),(4,4),(5,5),(6,6)\}$$
## Directed Graphs
Let $A$ and $B$ be two finite sets and $R\subseteq A\times B$, (i.e., $R$ is a binary relation between these two sets).

We can represent the elements of these two sets as vertices on a graph, with arrows linking the related elements.

This is called a directed graph, or digraph, of $R$.
### Example 1:
Let $A = \{1,3,5,7\}, B = \{2,4,6\}$
Consider the relation $V$ between $A$ and $B$ such that $V=\{(x,y)\in A\times B\;|\;x<y\}$.

We can represent $V$ with the following digraph:
![[digraph_example_1.png]]
As you can see above, the elements of $A$ and $B$ are shown in the left and right columns respectively. The related elements are connected with an arrow drawn between them.

>The columns are not strictly necessary, they just make reading this specific digraph easier. If you swapped the locations of 1 and 4, as long as the arrows were adjusted correctly the graph would still be valid.
### Example 2:
Let $A=\{1,2,3,4,5\}$.
Now consider the binary relation $V\subseteq A\times A$ where $V=\{(1,2),(3,3),(5,5),(1,4),(4,1),(4,5)\}$.

We can represent $V$ with the following digraph:
![[digraph_example_2.png]]
Unlike the previous example, this is a relation over a single set. There is no separation of the vertices like the columns in the last example.

>Recall that any relation, $R$, such that $R\subseteq A\times A$ is called a binary relation on $A$. 

## Functional Relations
We know that a function $f$ from a set $A$ to a set $B$, assigns exactly one element of $B$ to each element of $A$. This gives rise to the relation $R_f=\{(a,b)\in A\times B\;|\;b=f(a)\}$. We call $R_f$ a functional relation.

An functional relation $S\subseteq A\times B$, where $A$ and $B$ are arbitrary sets, is a relation, that has at most one $b\in B$ for each $a\in A$ where $(a,b)\in S$. 

For example:
Let $A=\{i\in\mathbb{N}\;|\;i<10\},\; B=\{i\in\mathbb{N}\;|\;5<i<15\}$.

If we take the function $f(x)=2x$, we can define $R_f$ as $R_f=\{(x,y)\in A\times B\;|\;y=2x\}$.

We can also see that $R_f=\{(3,6),(4,8),(5,10),(6,12),(7,14)\}$ and can be represented by the following digraph:
![[digraph_example_3.png]]
>Notice that this, while a functional relation, is not actually a function. A function must map every element of A to a single element of B, but a functional relation can skip elements of A. This can also be called a partial function.

## Building New Relations From Given Ones 
### Inverse Relations
Inverse relations are the opposite of a given relation.

Formally: Given a relation $R\subseteq A\times B$, the inverse relation $R^{-1}\subset B\times A$ is given by $R^{-1}=\{(b,a)\;|\;(a,b)\in R\}$.

For example the inverse of **"is a child of"** relation of a set of people is **is a parent of**.

As another example, take the set $A=\{1,2,3,4\}$ and the relation $R=\{(x,y)\;|\;x\leq y\}$.

From this we can see $R = \{(1,1),(1,2),(1,3),(1,4),(2,2),(2,3),(2,4),(3,3),(3,4),(4,4)\}$.

We can get $R^{-1}$ either by reversing each of the ordered pairs in $R$ or we can recognise that the inverse of $\leq$ is $\geq$ and so we know that $R^{-1}=\{(x,y)\;|\;x\geq y\}$.

And so $R^{-1}=\{(4,4),(4,3),(4,2),(4,1),(3,3),(3,2),(3,1),(2,2),(2,1),(1,1)\}$.
### Composition of Relations
Let $A$, $B$, and $C$ be arbitrary sets. Let $R\subseteq A\times B$ and $S\subseteq B\times C$. The composition of $R$ and $S$, denoted by $S \circ R$, is the binary relation between $A$ and $C$ given by $S\circ R=\{(a,c)\in A\times C\;|\;\exists\; b\in B,$ such that $aRb$ and$\;bSc\}$.

>$aRb$ is shorthand for $(a,b)\in R$. $bSc$ is the same, just for $(b, c)\in S$.

For example take following family tree:
![[Family Tree.png]]
If we define the following relations:
- $S:$ is a sister of
- $P:$ is a parent of

Then we can also define the relation $P\circ S:$ is an aunt of.

Since we can see that Alice $S$ Ken and Ken $P$ Alan, we know that Alice $P\circ S$ Alan.

>It might be tempting to read the $P\circ S$ as **parent of sister of** due to the $\circ$ and the order. However the correct way to read it is **sister of parent of**. 
>
>This can be confusing, but you can understand it by just reading the compositions backwards. Alice is Alan's aunt, so Alice is a **sister of a parent of** Alan. 

We can also compose relations with themselves.

For example $P\circ P:$ is a grandparent of.

Since Fred $P$ Ken and Ken $P$ Fiona, we know that Fred $P\circ P$ Fiona.

Below you can see a an example of how you can create a digraph of a composition of relations.
![[composition_digraph.png]]