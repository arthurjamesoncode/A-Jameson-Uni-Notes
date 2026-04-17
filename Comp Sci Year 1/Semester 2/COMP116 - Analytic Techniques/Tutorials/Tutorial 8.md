## Question 1:
**Question:** Let $A$ and $B$ be $2 × 2$ square matrices on $\mathbb R$. Prove that the determinant of the product of these two square matrices is the product of the determinants.

I.e. Prove
$$
\det (AB) = \det (A) \cdot \det (B)
$$

**Answer:** Let $A$ and $B$ be given by 
$$
A=\pmatrix{a & b \\ c & d},\; B=\pmatrix{w & x \\ y & z}
$$

Observe that
$$
\begin{split}
AB &= \pmatrix{a & b \\ c & d}\cdot\pmatrix{w & x \\ y & z} \\
& = \pmatrix{aw + by & ax + bz \\ cw + dy & cx + dz}
\end{split}
$$
Now we can find the determinants of $A$, $B$, and $AB$ like so
$$
\begin{split}
\det (A) & = ad - bc \\
\\
\det (B) & = wz - xy \\
\\
\det (AB) 
& = (aw+by)(cx+dz) - (ax+bz)(cw+dy) \\
& = (acwx + bcxy + adwz + bdyz) - (acwx+bcwz+adxy+bdyz) \\
& = bcxy + adwz - bcwz - adxy
\end{split}
$$
We can now calculate $\det(A)\cdot\det(B)$ like so:
$$
\begin{split}
\det(A) \cdot \det(B) 
& = (ad-bc)(wz-xy) \\
& = adwz - bcwz - adxy + bcxy
\end{split}
$$

Observe that
$$
\det(A)\cdot\det(B) =  bcxy + adwz - bcwz - adxy  = \det(AB)
$$
And so we have proved that 
$$
\det (AB) = \det (A) \cdot \det (B)
$$
when $A$ and $B$ are $2\times 2$ matrices on $\mathbb R$.
## Question 2
Let $A$ and $B$ be $3 \times 3$ square matrices on $\mathbb{R}$. Prove the following properties of the determinant function:

**Question:** Prove that the determinant of a matrix is equal to the determinant of its transpose:
$$\det(A^{T}) = \det(A)$$
**Answer:** Let
$$
A=
\begin{pmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33} \\
\end{pmatrix}
$$
First we can must find the transpose of $A$
$$
A^T=
\begin{pmatrix}
a_{11} & a_{21} & a_{31} \\
a_{12} & a_{22} & a_{32} \\
a_{13} & a_{23} & a_{33} \\
\end{pmatrix}
$$
Now we can find the determinants of both using the expansion formula. We will start by calculating $\det A$.

The expansion formula states that
$$
\det A = \sum^3_{j=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr)
$$
For any fixed value $1\leq i \leq 3$. It also states that
$$
\det A = \sum^3_{i=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr)
$$
For any fixed value $1\leq j \leq 3$.

We can choose any fixed row or column to get this determinant and the value will always be the same.

Observe that the first row of $A$ is equal to the first column of $A^T$. Also observe that $A_{11}=A^T_{11}$, $A_{12}=A^T_{12}$, and $A_{13}=A^T_{13}$, when fixing the first row of $A$ and the first column of $A^T$.

Therefore, by the expansion formula, if we fix the first row of $A$ and fix the first column of $A^T$, we are left with an identical calculation.

Therefore, it must be the case that $\det A=\det A^T$.

**Question:**  Prove the following properties about scalar multiplication of matrices and their determinants.
1. Prove that if a single row or column of $A$ is multiplied by a scalar $s \in \mathbb{F}$ to produce a new matrix $A'$, then $\det(A') = s \cdot \det(A)$. 
2. Using the previous result, show that if the entire matrix $A$ is multiplied by $s$, the determinant satisfies: $\det(sA) = s^{3} \det(A)$.    
 3. Prove that if $A$ contains a row or column of zeros, then $\det(A) = 0$.

**Answer:** 
**1.** The expansion formula states that
$$
\det A = \sum^3_{j=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr)
$$
For any fixed value $1\leq i \leq 3$. It also states that
$$
\det A = \sum^3_{i=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr)
$$
For any fixed value $1\leq j \leq 3$.

Let $s\in\mathbb R$, and $A_s$ be the matrix obtained by multiplying an unspecified row or column. We can choose any row or column to fix for the expansion formula and we will get the same value, so lets choose the row/column multiplied by $s$.

In this case:
$$
\begin{split}
\det A_s 
&= \sum^3_{j=1}\Bigl((-1)^{i+j}\cdot sa_{ij}\cdot\det A_{ij}\Bigr) \\
&= s\sum^3_{j=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr) \\
&= s\det A
\end{split}
$$
or 
$$
\begin{split}
\det A_s 
&= \sum^3_{i=1}\Bigl((-1)^{i+j}\cdot sa_{ij}\cdot\det A_{ij}\Bigr) \\
&= s\sum^3_{i=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr) \\
&= s\det A
\end{split}
$$

Observe that in both cases:
$$
A_s = s\det A
$$
Therefore multiplying any single row by a scalar value also multiplies the determinant by that same value.

**2.** Since multiplying a row by $s$ increases the determinant by a factor of $s$ multiplying all 3 rows by $s$ increases the determinant by a factor of $s$ three times, therefore increasing by a factor of $s^3$.

Therefore 
$$
\det(sA)=s^3\det A 
$$
**3.** Let $A$ be a $3\times 3$ matrix and $A_0$ be the matrix obtained by multiplying a single row or column by 0. This means that $A$ must have one row or column made entirely of 0s. 

By the previous theorems, we know that
$$
\det A_0 = 0\cdot \det A = 0
$$
Therefore if a matrix contains a row or column made entirely of 0s it must have a determinant of 0.

**Question:** Prove the following properties about how swapping rows/columns affects determinants
1. Prove that swapping any two rows (or two columns) of $A$ results in a determinant of opposite sign.    
 2. Show as a corollary that if $A$ has two identical rows or two identical columns, then $\det(A) = 0$.

**Answer:**
**1.** 
When swapping rows/columns of matrices there are two cases:
- The rows/columns are adjacent
- The rows/columns are not adjacent
These are square matrices, and working with rows and columns are identical, so from now on I will only consider swapping rows.

First we will consider what happens when we swap two adjacent rows.

Let $A$ and $B$ be $3\times 3$ matrices such that $B$ is the result of swapping two adjacent rows of $A$.

The expansion formula states that
$$
\det A = \sum^3_{i=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr)
$$
For any fixed value $1\leq j \leq 3$.

Observe that if
$$
A=
\begin{pmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33} \\
\end{pmatrix}
$$
then $B= B_a\; \text{OR}\; B=B_b$ where 
$$
B_a=
\begin{pmatrix}
a_{21} & a_{22} & a_{23} \\
a_{11} & a_{12} & a_{13} \\
a_{31} & a_{32} & a_{33} \\
\end{pmatrix},\; 
B_b=
\begin{pmatrix}
a_{11} & a_{12} & a_{13} \\
a_{31} & a_{32} & a_{33} \\
a_{21} & a_{22} & a_{23} \\
\end{pmatrix}
$$
$B_a$ swaps the first and second rows and $B_b$ swaps the second and third.

Observe that in either case, the submatrices obtained when removing either swapped row do not change when the rows are swapped. The submatrix obtained when removing the unchanged row does change however, to a vertical reflection of itself.

>Note that $A_1$ denotes the submatrix obtained by removing the first row of $A$ and $B_{a1}$ denotes the submatrix obtained by removing the row which was originally the first row of $A$ from $B_{a}$.

$$
\begin{split}
A_1 &= \pmatrix{\\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} } \\
A_2 &= \pmatrix{a_{11} & a_{12} & a_{13} \\\\ a_{31} & a_{32} & a_{33}  } \\
A_3 &= \pmatrix{a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\&} \\
\\
B_{a1} &= \pmatrix{a_{21} & a_{22} & a_{23} \\\\ a_{31} & a_{32} & a_{33}}\\
B_{a2} &= \pmatrix{\\a_{11} & a_{12} & a_{13} \\ a_{31} & a_{32} & a_{33}}\\
B_{a3} &= \pmatrix{a_{21} & a_{22} & a_{23} \\ a_{11} & a_{12} & a_{13} \\ &}\\
\\
B_{b1} &= \pmatrix{\\ a_{31} &  a_{32} & a_{33} \\ a_{21} & a_{22} & a_{23}} \\
B_{b2} &= \pmatrix{a_{11} & a_{12} & a_{13} \\ a_{31} & a_{32} & a_{33} \\&} \\
B_{b3} &= \pmatrix{a_{11} & a_{12} & a_{13} \\\\ a_{21} & a_{22} & a_{23} } \\
\end{split}
$$
Given a $2\times 2$ matrix $M$ given by
$$
M=\pmatrix{a & b \\ c & d}
$$
observe that the determinant of the vertical reflection of $M$ (denoted by $M_{flip}$)  is $-\det M$.
$$
\begin{split}
\det M & = ad - bc \\
\\
M_{flip} & = \pmatrix{c & d \\ a & b}
\\
\det M 
& = bc - ad \\
& = -(ad - bc)
\end{split}
$$

Imagine we fix the first column. 
- When the row we are removing is one of the swapped rows, the determinant of the submatrix stays the same but the coefficient we multiply becomes it's negation (due to the expansion formula)
- When the row we are removing is not one of the swapped rows, the determinant of the submatrix becomes its negation, while the coefficient we multiply stays the same.
This means that every term of the determinant of our new matrix $B$ becomes it's negation meaning that 
$$
\det B = -\det A
$$

And so we have proved that if you swap adjacent rows or columns of a $3\times 3$ square matrix then the determinant becomes it's negation.

Now let's consider the case of us swapping non-adjacent rows.

We can view swapping of non-adjacent rows as multiple sequential adjacent swaps.

In a $3\times 3$ matrix $A$, swapping non-adjacent rows can only mean swapping the top and bottom row.

To do this we can make two adjacent swaps, swapping the first row with the second row, and then the new second row with the first row, and then 1 more adjacent swap to move the top row back to the middle row. We will call this resulting matrix $B$.

Since we make 3 swaps and the sign flips each swap, it must be the case that
$$
\det B  = (-1)^3\det A = -\det A
$$

And so we have proved that swapping any two rows of a $3\times 3$ matrix results in the determinant becoming its negation.

**2.** Let $A$ be a $3\times 3$ matrix containing two identical rows or two identical columns. If we swap two identical rows or columns of this matrix, we are left with an identical matrix (still $A$).

By the previous theorem we know that 
$$
\begin{split}
\det A & = -\det A \\
2\det A & = 0 \\
\det A &= 0
\end{split}
$$
Therefore the determinant of a matrix with identical rows or columns must be $0$.
## Question 3
Let $A$ and $B$ be matrices defined as follows:

$$A = \begin{pmatrix} 2 & k \\ 1 & 4 \end{pmatrix}, \quad B = \begin{pmatrix} 1 & 0 & 2 \\ 0 & 3 & 1 \\ 2 & 1 & 0 \end{pmatrix}$$

**Question:** If the value of $k$ is chosen such that $\det(A) = \det(B)$, find the value of the determinant of the product matrix, $\det(AB)$.

**Answer:** First we find $\det A$ in terms of $k$.
$$
\begin{split}
\det A 
&= 2\cdot4 - 1\cdot k \\
&= 8 - k
\end{split}
$$
Then we find the determinant of $B$
$$
\begin{split}
\det B 
& = 1\cdot3\cdot0 + 0\cdot1\cdot2 + 2\cdot0\cdot 1 - 2\cdot3\cdot2 - 0\cdot0\cdot0 - 1\cdot 1\cdot 1 \\
& = 0 + 0 + 0 - 12 -1 \\
& = -13
\end{split}
$$
We can now solve for $k$
$$
\begin{split}
\det A &= \det B \\
8 - k &= -13 \\
k &= 21
\end{split}
$$
Oops I didn't read the whole question properly and wasted my time. $AB$ does not exist because the matrices have incompatible dimensions for multiplication.
## Question 4
Consider the function $f: \mathbb{C} \to \mathbb{C}$ defined as $f(z) = 1 + z - z^{2}$. The function is to be integrated between the points $p = 0$ and $q = 1 + i$ in the Complex Plane.

**Question:** Classify the following parameterizations, $t: \mathbb{R} \to \mathbb{C}$:
1. $t(x) = x^{2} - ix$
2. $t(x) = (2 - i) \cdot x$
3. $t(x) = x + 1 - i \cdot x$
4. $t(x) = \cos^{2}(\pi x) + \sin(\pi \cdot \frac{1}{2}) + i \sin(1.5\pi x)$

**Into the following categories:**
- (A) ONLY maps $Re(p)$ correctly
- (B) ONLY maps $Re(q)$ correctly
- (C) Maps BOTH $Re(p)$ and $Re(q)$ correctly
- (D) Maps NEITHER $Re(p)$ nor $Re(q)$ correctly

**Answer:**
1. (C)
2. (A)
3. (A)
4. (D)