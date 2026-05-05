## Matrix Representation
Computers can represent relations using matrices. 

Let $A=\{a_1,...,a_n\}$, $B=\{b_1,...,b_n\}$, and $R\subseteq A\times B$. 

We can represent $R$ as an array $M$ of $n$ rows and $m$ columns. We call this an $n$ by $m$ matrix. The entry in row $i$ and column $j$ of this matrix is given by $M(i,j)$ where $$M(i,j)=\begin{cases} 1 \;\text{if}\;(a_i,b_j)\in R \\ 0\; \text{if}\; (a_1,b_j)\notin R\end{cases}$$
### Examples
#### Example 1:
Let $A=\{1,3,5,7\}$, $B=\{2,4,6\}$ and $U=\{(x,y)\in A\times B\;|\;x+y=9\}$.

Assuming an enumeration, ($a_1=1,a_2=3,$ etc.), then $M$ represents $U$, where $$M=\begin{bmatrix}\;0 & 0 & 0\;\\\;0 & 0 & 1\;\\\;0 & 1 & 0\;\\\;1 & 0 & 0\;\end{bmatrix}$$
#### Example 2:
Let $A=\{a,b,c,d\}$ and suppose that $R\subseteq A\times A$ has the following matrix representation:$$M=\begin{bmatrix}\;0 & 1 & 1 & 0\;\\\;0 & 0 & 1 & 1\;\\\;0 & 1 & 0 & 0\;\\\;1 & 1 & 0 & 1\;\end{bmatrix}$$
From this matrix, we can see that $R=\{(a,b),(a,c),(b,c),(b,d),(c,b),(d,a),(d,b),(d,d)\}$.

>Note that, within a matrix representation of a relation, the row of the cell represents the left element of the ordered pair, and the column represents the right element of the ordered pair. 
>
>For example note how $(a,b)\in R$ since a one exists in the 2nd column of the 1st row, but $(b,a)\notin R$ since a zero exists in the 1st column of the 2nd row.
#### Example 3:
Let $A=\{1,2,3,4\}$

The binary relation $R$ on $A$ has the following digraph representation:
![[R_digraph.png]]
From the above digraph we can see that $R=\{(4,3),(3,2),(2,1)\}$ or $R=\{(x,y)\in A\times A\;|\;y=x-1\}$.

We can see that the matrix representation of $R$, $M$, can be given by $$M=\begin{bmatrix}\;0&0&0&0\\\;1&0&0&0\;\\\;0&1&0&0\;\\\;0&0&1&0\end{bmatrix}$$
## Composition with Matrices
Let's revisit the digraph showing composition of relations from [[Lecture 20 - Relations]].
![[composition_digraph.png]]
The above digraph represents 3 relations, that span 3 different sets. We will call the sets $A$, $B$, and $C$ where $A=\{a,b\}$, $B=\{1,2,3\}$, and $C=\{x,y\}$.

We can see that $R\subseteq A\times B$, $S\subseteq B\times C$, and $S\circ R\subseteq A\times C$.

We can also write out their matrix representations like so:
$$
M_R=\begin{bmatrix} \;1&1&1\; \\ \;0&1&0\; \end{bmatrix},\;
M_S=\begin{bmatrix} \;0&1\; \\ \;1&0\; \\ \;1&0\; \end{bmatrix},\;
M_{S\circ R}=\begin{bmatrix} \;1&1\; \\ \;1&0\; \end{bmatrix}
$$

If you are familiar with Boolean matrix multiplication you may realise that $M_{S\circ R}$ is the same as the Boolean matrix product of $M_R$ and $M_S$. 

You can get the matrix representing the composition of 2 relations by finding the Boolean matrix product of the matrices representing those relations.

### Boolean Matrix Multiplication
If you are familiar with standard matrix multiplication, you can understand Boolean matrix multiplication just by exchanging **multiplication** with **logical AND** and **addition** with **logical OR**.

If you are unfamiliar with any type of matrix multiplication, don't worry you can understand it from below.

When performing logical multiplying 2 matrices, $A$ and $B$, to form a third matrix $C$, the number of columns in $A$, must be the same as the number of rows in $B$. If $A$ is an $n$ by $x$ matrix, then $B$ must be an $x$ by $m$ matrix. 

The formula for a single element of $C$ at row $i$ and column $j$ is the following:
$$c_{ij} = (a_{i1} \land b_{1j}) \lor (a_{i2} \land b_{2j}) \lor \dots \lor (a_{in} \land b_{nj})$$
>$\land$ means **logical AND**, and $\lor$ means **logical OR**.

Essentially, to arrive at the value of $c_{ij}$ we first apply a **logical AND** operation between the corresponding values of the $i$th row of $A$ and the $j$th column of $B$. If any of those operations are a 1, the value of $c_{ij}$ is 1.

This is why the number of columns in the first matrix must match the number of rows in the second matrix, otherwise there will not be corresponding elements from the $i$th row and $j$th column, as the rows and columns will have a different number of elements.

We also know what the size of the resulting matrix will be. If $A$ is an $n\times x$ matrix and $B$ is an $x\times m$ matrix we know that the resulting matrix will be an $n\times m$ matrix.

A good way to remember all of this is by thinking of the inner and outer numbers. If you place the sizes of $A$ and $B$ next to each other, $n\times x,\;x\times m$, you can see that the **inner** numbers must match for it to be possible, while the outer numbers show the dimensions of the resulting matrix.

If we look back at example now we can work through it step by step.

Recall our Matrices:
$$M_R=\begin{bmatrix} \;1&1&1\; \\ \;0&1&0\; \end{bmatrix},\;
M_S=\begin{bmatrix} \;0&1\; \\ \;1&0\; \\ \;1&0\; \end{bmatrix},\;$$

We want to find $M_{S\circ R}$ and to do this we can find $M_R \odot M_S$.

>$\odot$ is the symbol for logical (Boolean) matrix multiplication. While this is the preferred notation, you may see $C=A\odot B$ written as $C=AB$ or $C=A\cdot B$. These are usually used to show standard matrix multiplication, but if $A$ and $B$ are defined as **logical matrices**, meaning they can only contain 0s and 1s, then they can be used for logical multiplication as well.

To find $M_R\odot M_S$, we do the following:
- Take the 1st row of $M_R$, $[1,1,1]$, and the 1st column of $M_S$, $[0,1,1]$.
- Complete a **logical AND** operation on all corresponding elements to get the bit vector $[0,1,1]$
- Complete a **logical OR** operation on this bit vector to get $1$. We now know the element that will be going in the 1st row and 1st column of $M_{S\circ R}$.
- Take the 1st row of $M_R$, $[1,1,1]$, and the 2nd column of $M_S$, $[1,0,0]$.
- Complete a **logical AND** operation on all corresponding elements to get the bit vector $[1,0,0]$
- Complete a **logical OR** operation on this bit vector to get $1$. We now know the element that will be going in the 1st row and 2nd column of $M_{S\circ R}$.
- Take the 2nd row of $M_R$, $[0,1,0]$, and the 1st column of $M_S$, $[0,1,1]$.
- Complete a **logical AND** operation on all corresponding elements to get the bit vector $[0,1,0]$
- Complete a **logical OR** operation on this bit vector to get $1$. We now know the element that will be going in the 2nd row and 1st column of $M_{S\circ R}$.
- Take the 2nd row of $M_R$, $[0,1,0]$, and the 2nd column of $M_S$, $[1,0,0]$.
- Complete a **logical AND** operation on all corresponding elements to get the bit vector $[0,0,0]$
- Complete a **logical OR** operation on this bit vector to get $0$. We now know the element that will be going in the 2nd row and 2nd column of $M_{S\circ R}$.

The resulting matrix from performing these steps is:$$
M_{S\circ R}=\begin{bmatrix} \;1&1\; \\ \;1&0\; \end{bmatrix}
$$
We can see that this is the same as the when we just wrote the matrix by looking at the digraph.

>Notice that to get $M_{S\circ R}$ we compute $M_R\odot M_S$. The order is swapped. Remember this, as it can cause confusion.

I recommend that you practice performing logical matrix multiplication a fair bit, as it is easy to make small mistakes as you go through the steps.

