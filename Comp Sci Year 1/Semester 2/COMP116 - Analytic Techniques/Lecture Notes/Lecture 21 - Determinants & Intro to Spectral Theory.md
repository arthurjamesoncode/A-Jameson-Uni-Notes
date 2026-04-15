## What is Spectral Theory?
Spectral Theory is an attempt to decompose a linear operator into simpler components, the same way a prism decomposes white white into the full **spectrum** of colours.

This will be covered over the coming lectures, where we will introduce the **Eigenvalue Problem**, the defining problem of spectral theory.

Today we will return to **matrices** and have a look at what **determinants** actually mean.
## Matrices
We have dealt with matrices earlier in this module, first introduced in [[Lecture 6 - Linear Transformations]].

A matrix $A$ is an $m\times n$ tuple of elements $a_{ij}$ where $i$ represents the row and $j$ represents the column.

There are a number of simple operations on matrices, this have been covered earlier in the course so I will only give a quick reminder here.
### Matrix Addition
Matrix addition is done by adding up all corresponding elements of both matrices.

This means that matrix addition can only be done with matrices of identical dimensions. You can add two $2\times 3$ matrices, but you can't add one $2\times 3$ matrix with one $2\times 4$ matrix.

For example take the two matrices
$$
\mathbf{A}=\pmatrix{a & b \\ c & d},\;
\mathbf{B}=\pmatrix{w & x \\ y & z}
$$

We can see that the result of adding these two matrices is 
$$
\begin{split}
\mathbf{A+B}
& =
\pmatrix{a & b \\ c & d}
+
\pmatrix{w & x \\ y & z} \\
& =
\pmatrix{a+w & b+x \\ c+y & a+z}
\end{split}
$$
### Multiplication by a Scalar
Multiplying a matrix by a scalar just means that you multiply each element of the matrix by the scalar.

For example take the following matrix and scalar
$$
\mathbf{A}=\pmatrix{a & b \\ c & d},\; s\in\mathbb R
$$

We can see that
$$
\begin{split}
sA
& =
\pmatrix{sa & sb \\ sc & sd}
\end{split}
$$
### Matrix Multiplication
We have covered matrix multiplication both when covering [[Lecture 21 - Computer Representations of Relations#Boolean Matrix Multiplication|boolean matrix multiplication]], and when covering [[Lecture 6 - Linear Transformations#Matrix Multiplication By a Vector|matrix vector multiplication]]. I recommend reviewing the latter for detailed explanation, but I will cover the key points again here.

Matrix multiplication works by summing the product of corresponding values from the rows of the first (left hand) matrix and the columns of the second (right hand) matrix. The result is a single number, whose row and column in the new matrix is decided by which row and column were multiplied together.

This means that the first matrix must have the same number of columns as the second matrix has rows, and that the order of matrix multiplication matters.

If you have two matrices $A$ and $B$ where $A$ is a $x\times y$ matrix and $B$ is a $y\times z$ then $AB$ will be $x \times z$ matrix.

>A good way to remember some of this information is to think about the inner and outer dimensions.
>
>If you write the dimensions of the matrices in the order you want to multiply them you can tell both if you **can multiply them** and what the **dimensions of the resulting matrix** will be. To be able to multiply them the **inner-dimensions** must be the same. The **outer-dimensions** tell you the size of the resulting matrix.

You can see an example multiplication of two $2\times 2$ matrices below
$$
\begin{split}
AB & =
\pmatrix{a & b \\ c & d}\cdot\pmatrix{w & x \\ y & z} \\
& =
\pmatrix{aw + by & ax + bz \\ ax + bz & cx + dz} 
\end{split}
$$
### Matrix Inverse
The inverse of a matrix has not been covered before on this module, but is related to the **identity matrix** which was covered [[Lecture 6 - Linear Transformations|here]].

The identity matrix $I$ is any **square** matrix where the top-right to bottom left diagonal is filled with 1s and every other cell is filled with 0s. The inverse of a matrix $A$ is defined as the matrix which when multiplied by $A$ gives $I$.

We denote the inverse of a matrix $A$ by adding a superscript of $-1$, so formally
$$
A\cdot A^{-1} = A^{-1} \cdot A = I
$$

Not every matrix has an inverse. We call a matrix with no inverse a **singular matrix**. Only square matrices will ever be invertible but not all square matrices are invertible.

Let's consider two matrices
$$
A = \pmatrix{a & b \\ c & d},\; B=\pmatrix{d & -b \\ -c & a}
$$

If we multiply these matrices we can see that
$$
\begin{split}
A \cdot B & =
\pmatrix{a & b \\ c & d}\cdot\pmatrix{d & -b \\ -c & a} \\
& =
\pmatrix{ad - bc & -ab + ab \\ cd - cd & -bc+ad} \\
& = 
\pmatrix{ad-bc & 0 \\ 0 & ad-bc}
\end{split}
$$

Observe that 
$$
AB = \pmatrix{ad-bc & 0 \\ 0 & ad-bc} = (ad-bc)\cdot I
$$

Since $A\cdot A'=I$ we know that
$$
\begin{split}
A^{-1} 
& = \frac{1}{ad-bc}B \\
& = \frac{1}{ad-bc}\pmatrix{d & -b \\ -c & a}
\end{split}
$$

$ad-bc$ is the **determinant** of a $2\times 2$ matrix, this has been touched on before, and will be gone into in detail later in this note.

From all of this, you can see that the inverse of a $2\times 2$ matrix is gotten by swapping the elements of the top-left diagonal and negating the elements of the top-right diagonal before dividing the whole thing by the determinant.

Because of that last step, the inverse of a matrix is only defined if the determinant of the matrix isn't 0.

>The process of inverting a matrix is a bit more complicated than this when we reach into 3 or more dimensions. I don't think this will be covered or required in this module, but if curious you can look at [this video](https://www.youtube.com/watch?v=srnaDoIKA-E).
## Determinant of a Matrix
We have seen before how every $n\times n$ matrix can act as a linear map for vectors from $\mathbb R^n$. 

The **determinant** of a matrix is a single number that indicates how much the linear map **scales** the vector or group of vectors. For groups of vectors from $\mathbb R^2$, this measures how much the total **area** increases. For groups of vectors from $\mathbb R^3$ however, this measures how much the total **volume** increases.

>There is more interesting stuff to do with determinants that won't be fully covered here. I recommend checking out [this video](https://www.3blue1brown.com/?v=determinant), from 3blue1brown if you are curious.

For a $2\times 2$ matrix $A$ given by
$$
A=\pmatrix{a & b \\ c & d}
$$
The determinant $D$ is 
$$
D=ad-bc
$$
Which described in plain English is the difference of the product of the top-left diagonal and the product of the top-right diagonal.

This gets a bit more complicated when we look to matrices with higher dimensions, but has a similar logic.

>Using $a$, $b$, $c$, and $d$ to represent the elements of a matrix works well for $2\times 2$ matrices, where there aren't many elements to keep track of. 
>
>For matrices from more than 2 dimensions, however, it is better to use the notation $a_{ij}$ for all elements of the matrix, where $i$ is the row of the element and $j$ is the column, since this makes it clear what row and column it is. 
>
>For example $a_{11}$ represents the top left element of the matrix and $a_{32}$ represents the element from the third row and second column.

You can see the determinant for a $3\times 3$ matrix below.

![[3x3determinant.png]]

This looks awful, but actually fits a similar pattern to that we saw with the $2\times 2$ matrices.

If you notice the colours of the elements are related to the positive and negative products below:
- The positive products are made of the highlighted colour groups,
- The negative products are made of the vertical reflections of the highlighted colour groups.

This is actually the same top-left diagonal minus top-right diagonal logic as the $2\times 2$ matrix, except that there are more diagonals. 

Each of the highlighted colours represents a left diagonal that starts at the top row. Following the diagonals, if an element is in the last column but not in the bottom row, it wraps around and the next element is chosen from the first column of the next row down.

The negative products follow the same rule but instead are the right diagonals starting from the top row.

This process actually generalises to any dimension $n$, and we have a recursive algorithm to compute it for matrices of arbitrary size.
### The Expansion Formula
The expansion formula is a recursive algorithm that allows us to find the determinant of any square matrix.

For any $m\times m$ matrix $A$ and $i,j\in\{1,...,m\}$, let $A_{ij}$ be the $(m-1)\times(m-1)$ matrix obtained by removing row $i$ and column $j$.

The expansion formula states that
$$
\det A = \sum^m_{j=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr)
$$
for any fixed $i$ (any fixed row).

It doesn't matter whether you fix a row and iterate through columns, or fix a column and iterate through rows. 

This means that the expansion formula also states that
$$
\det A = \sum^m_{i=1}\Bigl((-1)^{i+j}\cdot a_{ij}\cdot\det A_{ij}\Bigr)
$$
for any fixed $j$ (any fixed column).

Lets run through this with a general $3\times3$ matrix
$$
A=
\begin{pmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33} \\
\end{pmatrix}
$$
To find our determinant we need to choose any fixed row or column. It does not matter which one at all so for simplicity I will choose the top row.

Now we need to go element by element over the top row and find $(-1)^{i+j}$, as well as $A_{ij}$ and therefore $\det A_{ij}$.

Lets start by finding the values $(-1)^{i+j}$ for all the elements in the first row
$$
\begin{split}
a_{11}: 
(-1)^{1+1} 
& = (-1)^2 \\
& = 1 \\
\\
a_{12}: 
(-1)^{1+2} 
& = (-1)^3 \\
& = -1 \\
\\
a_{13}: 
(-1)^{1+3} 
& = (-1)^4 \\
& = 1 \\
\end{split}
$$
Which tells us that 
$$
\det A = a_{11}\cdot\det A_{11} - a_{12}\cdot\det A_{12} + a_{13}\cdot\det A_{13}
$$

Now all we need to do is find each submatrix and it's determinant.
$$
\begin{split}
A_{11} & = \pmatrix{\\ & a_{22} & a_{23} \\ & a_{32} & a_{33}} \\
\det A_{11} & = a_{22}a_{33}-a_{23}a_{32} \\
\\
A_{12} & = \pmatrix{\\ a_{21} && a_{23} \\ a_{31} && a_{33}} \\
\det A_{11} & = a_{21}a_{33}-a_{23}a_{31} \\
\\
A_{13} & = \pmatrix{\\ a_{21} & a_{22} & \\ a_{31} & a_{32}} & \\
\det A_{11} & = a_{21}a_{32}-a_{22}a_{31}
\end{split}
$$

Now we can plug this back in to get
$$
\begin{split}
\det A 
& = a_{11}\bigl(a_{22}a_{33}-a_{23}a_{32}\bigr) - a_{12}\bigl(a_{21}a_{33}-a_{23}a_{31}\bigr) + a_{13}\bigl(a_{21}a_{32}-a_{22}a_{31}\bigr) \\
& = a_{11}a_{22}a_{33} + a_{12}a_{23}a_{31} + a_{13}a_{21}a_{32} - a_{11}a_{23}a_{32} - a_{12}a_{21}a_{33} - a_{13}a_{22}a_{31}
\end{split}
$$
which we can see matches the determinant we saw before.
## Determinant Properties
There are a number of useful properties to know when it comes to determinants. We will go over some of these now.

I will be explaining these rules in plain English first, but I think the maths notation definitions are more succinct and less confusing.
## The Determinant Transpose Rule
The determinant transpose rule states that the determinant of a matrix is the same as the determinant of the transpose of the same matrix.

The transpose operation was covered briefly during [[Lecture 15 - Representation Techniques#Conjugate|representation techniques of complex numbers]], but, in case you need a reminder, the transpose of a matrix is the same matrix reflected in the top-left diagonal.

>We use $A^T$ to denote the transpose of $A$.

So formally:
$$
\det (A^T) = \det A
$$
### The Determinant Multiplication Rule
The determinant multiplication rule states that if a matrix $A$ is multiplied by a matrix $B$ the determinant of $AB$ will be the product of $\det A$ and $\det B$.

So formally
$$
\det AB = \det A\cdot\det B 
$$
A direct consequence of this is that
$$
\det A^n = (\det A)^n
$$
for any square matrix $A$ with $n\in\mathbb N$
### Scalar Multiplication Rule
The scalar multiplication rule states that if one row or column of $A$ is multiplied by a scalar $s$, then the value of $\det A$ is also multiplied by $s$. 

A consequence of this is that for an $m\times m$ matrix $A$ with $s\in\mathbb R$
$$
\det sA = s^m\det A
$$

Another consequence of this is that if any single row of column of $A$ is entirely filled with zeros, then $\det A$ will be 0.
### Row/Column Swap Rule
The row/column rule states that if you form a new matrix $B$ by swapping 2 rows (or columns) of a matrix $A$, then $\det B = -\det A$.

If we recall the expansion formula, and the alternating signs we were working with there, you can start to understand why this happens.

One big consequence of this is that if any two rows of a matrix $A$ are identical, or if any 2 columns of $A$ are identical, then $\det A=0$.