## Transitive Closures
Given a binary relation $R$ on a set $A$, the transitive closure of, $R^*$, of $R$ is the relation with the following properties:
- $R^*$ is transitive
- $R\subseteq R^*$
- If $S$ is a transitive relation on $A$ and $R\subseteq S$, then $R^*\subseteq S$

What this means is that $R^*$ is the smallest transitive superset of $R$.

Since $R\subseteq R^*$ it means we can reach $R^*$ by simply adding edges to $R$. If $R$ is transitive $R^*=R$.
### Computing a Transitive Closure:
Let $A=\{1,2,3\},\; R=\{(1,1),(1,2),(1,3),(2,3),(3,1)\}$

When finding transitive closures, I find that the best strategy is to look for chains. For example, we start at (1,2), we then look at what 2 is related to, in this case only 3, and then we see if we need to add the (1,3) pair. In this case, it is already part of the relation, so we don't. 

Next we look at (1,3), continuing our chain, and we check what 3 is related to in this case only 1, and we check if we need to add (1,1). In this case, it is already part of the relation, so we don't. Now that we have reached (1,1), when we started from (1,2), we have completed a loop and we know for sure that all possible (1,x) edges are present.

Next we look at a new chain starting at (2,3), we first look at what 3 is related to, in this case only 1, and we see if we need to add (2,1). In this case, it is not part of the relation, so we do.

Now we have a new relation, $\{(1,1),(1,2),(1,3),(2,1),(2,3),(3,1)\}$, and we continue our chain by looking at (2,1). We first look at the elements 1 is related to, in this case, 1, 2, and 3, and check to see if we need to add (2,1), (2,2), or (2,3). In this case (2,1), and (2,3) are both already in the relation so we just need to add (2,2). 

Our relation is now $\{(1,1),(1,2),(1,3),(2,1),(2,2),(2,3),(3,1)\}$, and we continue our chain from (2,2). Since we have ended at (2,2) and started this chain with (2,3), we know that we have completed the chain, and can move on to a new starting point.

We now start a new chain with (3,1), and look at what 1 is related to, which is 1, 2, and 3, before seeing if we need to add any new (3,x) pairs. Since only (3,1) exists we need to add (3,2) and (3,3). 

This leaves us with the relation $\{(1,1),(1,2),(1,3),(2,1),(2,2),(2,3),(3,1),(3,2),(3,3)\}$. If we continue the chain from either (3,2), or (3,3) both complete the loop without adding any more elements to this relation, and there are no more elements from which to start a new chain so we know that this relation **must** be transitive and so we can say that $R^*=\{(1,1),(1,2),(1,3),(2,1),(2,2),(2,3),(3,1),(3,2),(3,3)\}$.

Below is the digraph of the $R$ and $R^*$.

$R$:
![[Trans_Closure_start.drawio.png]]

$R^*$:
![[trans_closure_end.drawio.png]]

When computing trans closures using a digraph, the process is the same as described when looking at a list of ordered pairs, except now you have to visually track the relations.

## Transitivity and Composition
A relation $R$ is transitive $\iff R\circ R\subseteq R$.

This means that a relation is only transitive if when composed with itself it does not add any new edges.

This is because $R\circ R=\{(a,c)\; |\; \exists b \text{ such that } aRb \text{ and } bRc\}$.

If we define $S^1=S,\; S^2=S\circ S,\;S^3=S\circ S\circ S,$ and so on up to $S^n$, we can then define this Theorem as the following:

If we denote the transitive closure of $S$ as $S^*$, then $xS^*y\iff\exists n>0 \text{ such that }xS^ny$.
### Transitive Closure in Matrix Form
We can view how this works by composing some matrices.

Let $A=\{1,2,3,4,5\}$ and $R$ be represented by the matrix $M_R$ given by$$
M_R=\begin{bmatrix}
\;1&0&0&1&0\; \\
\;0&1&0&0&1\; \\
\;0&0&1&0&0\; \\
\;1&0&1&0&0\; \\
\;0&1&0&1&0\;
\\\end{bmatrix}$$
We can compute the matrix representation of $R\circ R$ by computing $M\odot M$ as shown in [[Lecture 21 - Computer Representations of Relations]].

When we do this we see that $M_{R\circ R}$ is given by $$
M_{R\circ R}=\begin{bmatrix}
\;1&0&1&1&0\; \\
\;0&1&0&1&1\; \\
\;0&0&1&0&0\; \\
\;1&0&1&1&0\; \\
\;1&1&1&0&1\;
\end{bmatrix}
$$
We can see from this that $R$ is not transitive as we can see that there are edges in $M_{R\circ R}$ that do not exist in $M_R$ such as in the 1st row third column. 

Note that it is possible to lose edges when computing $R\circ R$ on some relations, because of this we can find the transitive closure through an iterative process of:
- Composing the matrix with itself; 
- Checking if the matrix is transitive; 
- If it is we end with that matrix, otherwise we perform a **logical OR** operation on the matrix and its composition and restart from step 1 with that matrix.

If we continued with the example above, we know that the $M_R$ is not transitive so we compute a **logical OR** operation between $M_R$ and $M_{R\circ R}$. Since no edges were lost when composing $R$ with itself, this is just $M_{R\circ R}$ which we take as our new $M_{R_1}$ and repeat.

So now:$$
M_{R_1}=
\begin{bmatrix}
\;1&0&1&1&0\; \\
\;0&1&0&1&1\; \\
\;0&0&1&0&0\; \\
\;1&0&1&1&0\; \\
\;1&1&1&0&1\;
\end{bmatrix},\;
M_{R_1\circ R_1}=
\begin{bmatrix}
\;1&0&1&1&0\; \\
\;1&1&1&1&1\; \\
\;0&0&1&0&0\; \\
\;1&0&1&1&0\; \\
\;1&1&1&1&1\;
\end{bmatrix}
$$
We can see that $M_R$ is still not transitive as there are new edges in $M_{R1\circ R1}$ such as the edge in the 1st column and 2nd row. So we now perform a **logical OR** between $M_{R_1}$ and $M_{R_1\circ R_1}$, which as $M_{R_1\circ R_1}$ lost no edges we just take  $M_{R_2}=M_{R_1\circ R_1}$.

So now:$$
M_{R_2}=
\begin{bmatrix}
\;1&0&1&1&0\; \\
\;1&1&1&1&1\; \\
\;0&0&1&0&0\; \\
\;1&0&1&1&0\; \\
\;1&1&1&1&1\;
\end{bmatrix},\;
M_{R_2\circ R_2}=
\begin{bmatrix}
\;1&0&1&1&0\; \\
\;1&1&1&1&1\; \\
\;0&0&1&0&0\; \\
\;1&0&1&1&0\; \\
\;1&1&1&1&1\;
\end{bmatrix}
$$
Now we see that $M_{R_2\circ R_2}$ adds no new edges so we know that $M_{R_2}$ is transitive. This means that we can take $R^*=M_{R_2}$ (or more specifically the relation represented by $M_{R_2}$ and we know we've found our transitive closure. 

### Warshall's Algorithm
Below we can see an implementation of Warshall's algorithm in python:
```
def warshall(a):
	n = len(a)
	for k in range (n):
		for i in range (n):
			for j in range (n):
				a [i][j] = (a[i][j] or (a[i][k] and a[k][j]))
	return a
```

Warshall's algorithm is similar to the algorithm we described above but, instead of multiplying the whole matrix each time, it iterates through each node `k`, (would be the values 1-5, represented by positions 0-4, in the above example) and, if `i` and `j` aren't connected already, checks if each value of `k` connects `i` and `j`.

This isn't really necessary for the course, but understanding this algorithm can help you understand the logic behind computing transitive closures.
## Equivalence Relations
An equivalence relation is any relation that is reflexive, transitive, and symmetric.

For example lets take the relation $R=\{(a,b)\in (\mathbb{Z}-\{0\})\times(\mathbb{Z}-\{0\})\; |\; ab> 0\}$;

This is a relation on the non-zero integers given by $aRb$ if $ab > 0$.

We can recognise the following about this relation:
- We can see that this relation is **reflexive** as any integer squared is always positive. 
- We can see that this relation is **symmetric** as $ab > 0\implies ba > 0$.
- We can see that this relation is **transitive** as any if $ab > 0$ and $bc> 0$ then $a$, $b$, and $c$ must be either all positive or all negative. In either case the relation holds.
- We can see that this relation is not **antisymmetric** $(2,3)\in R$ and $(3,2)\in R$.

Because the relation is **reflexive**, **antisymmetric**, and **transitive**, it means that the relation is an equivalence relation.

An interesting consequence of equivalence relations is that they partition the set they exist on into multiple distinct classes.

Take the example above, $R=\{(a,b)\in (\mathbb{Z}-\{0\})\times(\mathbb{Z}-\{0\})\; |\; ab> 0\}$. This relation splits the set $\mathbb{Z}-\{0\}$ into 2 sets. $A=\{x\in Z\;|\;x<0\},\;B=\{x\in Z\;|\;x>0\}$. If you look at set $A$ you will see that every element in $A$ is related to every other element of $A$, and the same is true for $B$.

In fact $R=(A\times A)\cup(B\times B)$.

Lets look at another example, and try and figure out the distinct classes.

Let $R=\{(x,y)\in \mathbb{N}\times \mathbb{N}\;|\;x\text{ and }y\text{ leave the same remainder when divided by }3\}$.

We can recognise the following about this relation:
- We can see that this relation is **reflexive** as any integer leaves the same remainder as itself when divided by 3. 
- We can see that this relation is **symmetric** as $aRb\implies bRa$.
- We can see that this relation is **transitive** as any if $a$, $b$ both leave the same remainder when divided by 3 and $b$ and $c$ both leave the same remainder when divided by 3, then $a$ and $c$ must also both have the same remainder when divided by 3.
- We can see that this relation is not **antisymmetric** $(2,5)\in R$ and $(5,2)\in R$.

We can see from these properties that this an equivalence relation, so what are the distinct classes. In this case it is simple, the split is based on what the remainder is when divided by $3$. It can only be $1$, $2$, or $0$, so every element in $\mathbb{N}$ can be grouped into one of those three classes.

Other examples could be same length on the set of strings, or same tax band on the set of salaries. There is something about these relations that determine them to be the same in some way, hence the title of *equivalence* relation.

### Functions and Equivalence Relations
Every equivalence relation $R$ on a set $A$ can be defined by using a function.

Let $f:A\to B$ be a function. We can define $R$ like so: $R=\{(a,b)\in A\times A\;|\;f(a)=f(b)\}$.

For example, if $A$ is the set of cars and $B$ is $\mathbb{R}$, and $f$ assigns any car in $A$ to its length, then $aRb\iff$ $a$ and $b$ are of the same length.

The number of distinct classes is the same as the size of the range of $f$, (or $f(A)$).

Again, it should be clear why these are called *equivalence* relations now.
## Partitions on a Set
Sets can be partitioned into multiple blocks. We call this collection of blocks the partition.

A partition of a set $A$ is a collection of non-empty subsets $A_1,...,A_n$ of $A$ for which the following properties hold:
- $A=A_1\cup A_2\cup...\cup A_n$
- $A_i\cap A_j=\emptyset$ for $i\neq j$.

Essentially, the partition must contain every element of the se, and no element can be in more than one block of the partition.

For example:
![[partitions.png]]
## Equivalence Classes
Equivalence classes are the blocks of the partition that equivalence classes create. I already gave some examples for this before.

The equivalence class $E_x$ of any $x\in A$ is defined by $E_x=\{y\;|\;yRx\}$.