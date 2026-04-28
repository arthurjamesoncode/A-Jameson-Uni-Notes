## The Eigenvalue Problem
The Eigenvalue Problem is the defining problem of spectral theory. The problem is as follows.

Given an $n\times n$ matrix $A\in\mathbb R^{n\times n}$, find all scalar values $\lambda\in\mathbb R$ for which there is an $n$-vector $\vec v_\lambda\neq0$ satisfying the equation
$$
A\cdot\vec v_\lambda = \lambda\cdot \vec v_\lambda
$$
The scalar values $\lambda$ are called the **eigenvalues** of $A$.

The $n$-vectors $\vec v_\lambda$ are called the **eigenvectors** of $A$.

If $\vec v_\lambda$ is an eigenvector of $A$, then so is $c\vec v_\lambda$ for all $c\in\mathbb R$.

Geometrically, this means that matrix $A$, when applied as a linear map, scales all vectors in the direction of $\vec v_\lambda$ by the factor $\lambda$.
### Solving the Eigenvalue Problem
To find the eigenvalues of $A$, we find solutions to the **characteristic equation**
$$
\det(A-\lambda I)=0
$$
>Recall that $I$ is the $n\times n$ identity matrix. You can look back to [[Lecture 6 - Linear Transformations#Linear Transformation|this note]] for a refresher.

We use $\chi(A)$ as a shorthand to denote $\det(A-\lambda I)$.

$\chi(A)$ is a polynomial of degree $n$. Any polynomial has $n$ complex roots, which are not necessarily distinct. As a result $A$ has $n$ eigenvalues $\lambda_i\in\mathbb C$ which are also not necessarily distinct.

If you recall that if $\lambda_i$ is a root of a polynomial then $(\lambda_i -\lambda)$ is a factor of that polynomial, then you know that we can write
$$
\chi(A) = (\lambda_1-\lambda)\times\cdots\times(\lambda_n-\lambda)
$$

>Recall that $\mathbb R\subset\mathbb C$, so this statement does not mean that every eigenvalue has an imaginary part. If you are confused about the idea of "non-distinct roots" I recommend you go back to [[Lecture 14 - Complex Numbers]] since **multiplicity** is discussed in the beginning.

If you're struggling to understand how $\chi(A)$ is a polynomial, don't worry. It will become more clear in the example below.

The list of all eigenvalues $\lambda_1$ is called the spectrum of $A$ and is denoted like so
$$
\sigma(A)=(\lambda_1, \lambda_2, \lambda_3,...,\lambda_n)
$$
By convention, the eigenvalues are ordered from largest absolute value $|\lambda_1|$ to smallest absolute value $|\lambda_n|$ .
 
$\lambda_1$ is called the **dominant eigenvalue** of $A$. If $\lambda_1$ appears multiple times, then $A$ is said to have **multiple dominant eigenvalues**.

>This is the consensus I am finding online, however the lecture slides state that $\lambda_1$ is only called the dominant eigenvalue if unique. I doubt this will be relevant, but it's probably useful to know there is some variation in how people use it.

The maximum of the absolute values of all eigenvalues is called the spectral radius and is denoted with $\rho(A)$.  

For **complex values** if $\lambda$ is an eigenvalue $\bar\lambda$ is also an eigenvalue. You can understand this is you recall that all eigenvalues of $A$ are roots of $n$ degree polynomial.

**Importantly:** If $A$ is symmetric, then all eigenvalues $\lambda_k$ of $A$ are real.
## Example
Consider the matrix $A$ given by 
$$
A=\pmatrix{3 & 1\\0 & 2}
$$
From this we can derive the characteristic polynomial $\chi(A)$
$$
\begin{split}
\chi(A)
&= \det(A-\lambda I) \\
&= \det\Big(\pmatrix{3 & 1 \\ 0 & 2}-\pmatrix{\lambda & 0 \\ 0 & \lambda}\Big) \\
&= \det\Big(\pmatrix{3-\lambda & 1 \\ 0 & 2-\lambda}\Big) \\
&= (3-\lambda)(2-\lambda) - 1(0) \\
&= (3-\lambda)(2-\lambda)
\end{split}
$$
Since our eigenvalues are solutions to the equation
$$
(3-\lambda)(2-\lambda)=0
$$
We know that our eigenvalues must be 3 and 2.

Hence
$$
\sigma(A)=(3, 2)
$$
We can now use these eigenvalues to find eigenvectors for $A$. First we will find them for our dominant eigenvalue, 3.

We have the equation
$$
\begin{split}
\pmatrix{3 & 1 \\ 0 & 2} \pmatrix{x \\ y} &= 3\pmatrix{x \\ y} \\
\pmatrix{3x+y \\ 2y} &= \pmatrix{3x \\ 3y}
\end{split}
$$
Which we can split into simultaneous equations to solve. 

In this case, we can observe that $2y=3y$ is only possible when $y=0$. And when substituting that back into the $x$ term we see that $3x+0=3x$.

This means any 2-vector where the $y$ term is 0 is an eigenvector of this matrix. For example $\binom10$. 

Now let's do the same thing for the eigenvalue 2.

We have the equation
$$
\begin{split}
\pmatrix{3 & 1 \\ 0 & 2} \pmatrix{x \\ y} &= 2\pmatrix{x \\ y} \\
\pmatrix{3x+y \\ 2y} &= \pmatrix{2x \\ 2y}
\end{split}
$$
We can split this into simultaneous equations to solve.

Observe that 
$$
\begin{split}
3x+y&=2x \\
x &= -y \\
\\
&\text{AND}
\\
\\
2y &= 2y
\end{split}
$$
Since any value of $y$ satisfies $2y=2y$, and $x$ must be $-y$ any 2-vector where $x=-y$ is an eigenvector of this matrix. For example $\binom{1}{-1}$.
## Diagonalisation & Eigendecomposition
Following on from our example, let's make a new matrix $B$ where each column is an eigenvector of $A$. Using the examples we chose we get 
$$
B=\pmatrix{1 & -1 \\ 0 & 1}
$$
Now let's find the inverse of $B$
$$
\begin{split}
B^{-1}
&= \frac{1}{ad-bc}\pmatrix{d & -b \\ -c & a} \\
&= \frac{1}{1\cdot1-(-1)\cdot0}\pmatrix{1 & 1 \\ 0 & 1} \\
&= \pmatrix{1 & 1 \\ 0 & 1}
\end{split}
$$

We can actually use $B$ and it's inverse along with $A$ to construct a **diagonal matrix** $D$ where the eigenvalues of $A$ make up the leading (top-left) diagonal of $D$. The way we do that is to sandwich $A$ in-between $B^{-1}$ and $B$.
$$
\begin{split}
D 
&= B^{-1}AB \\
&= \pmatrix{1 & 1 \\ 0 & 1}\pmatrix{3 & 1 \\ 0 & 2}\pmatrix{1 & -1 \\ 0 & 1} \\
&= \pmatrix{3 & 3 \\ 0 & 2}\pmatrix{1 & -1 \\ 0 & 1} \\
&= \pmatrix{3 & 0 \\ 0 & 2}
\end{split}
$$
Conversely, we can invert this to get
$$
A=BDB^{-1}
$$

This process does not work for every square matrix. If this does work for a square matrix $A$, then we call $A$ **diagonalisable**, and call $BDB^{-1}$ its **eigendecomposition**.

Using **eigendecomposition** allows for easy computations of **matrix powers**. This is because
$$
A^n = BD^nB^{-1}
$$
for any diagonalisable matrix $A$.

Exactly why this is, is difficult to explain and unnecessary for this module. What is easier to explain is why this is useful.

Consider a diagonal $n\times n$ matrix. We multiply an matrices by summing the product of corresponding elements from the rows of the first matrix and the columns of the second matrix.

If the only non-zero elements of a matrix lie on it's diagonal, then the matrix raised to the power of $n$ is the same as the matrix obtained by raising each diagonal element to the power of $n$.

It is far less computationally costly to square the diagonal elements of a matrix rather than multiply a matrix by itself, hence why this trick is so useful.
### Can't Always Diagonalise
As stated above, you cannot always reduce a linear map to a diagonalisable scaling.

Take the matrix representation of $i$, this is also the linear map for rotating counter clockwise by $\pi/2$.
$$
A=\pmatrix{0 & -1 \\ 1 & 0}
$$
In this case we can observe that
$$
\begin{split}
\chi(A)
&= \det(A-\lambda I) \\
&= \det\Big(\pmatrix{-\lambda & -1 \\ 1 & -\lambda}\Big) \\
&= (-\lambda)^2 - (-1)\cdot1 \\
&= \lambda^2 + 1
\end{split}
$$
We know the polynomial $\lambda^2+1$ has no real roots, and therefore $i$ has no real **eigenvalues**.

No real eigenvalues means no *"real"* scaling. These linear maps do still scale the vectors they are applied to, but their scaling is **complex**.

**Complex scaling** representations rotations as well as scaling.
## Note on Practice Questions
Olga included some practice questions on the final two slides. I think these are worth going over, but I am not going to do so in these notes.