---
cssclasses:
  - flashcards
---
## Polynomials
### Lagrange Basis Polynomials
$$
l_i(x)=\prod_{0\leq j\leq n,\;j\neq i}{\frac{(x-x_j)}{(x_i-x_j)}}
$$
### Full Lagrange Polynomial
$$
L(x)=\sum^n_{i=0}y_il_i(x)
$$

## Vectors & Vector Spaces
### Scalar/Dot Product
$$
\vec u \cdot \vec v = |\vec u| \cdot |\vec v| \cdot \cos(\alpha)
$$
OR
$$
\begin{split}
\vec u \cdot \vec v 
& = u_1v_1 + u_2v_2 + \cdot\cdot\cdot + u_nv_n \\
& = \sum^n_{i=1}u_iv_i
\end{split}
$$
### Vector/Cross Product
$$
\vec u \times \vec v = |\vec u| \cdot |\vec v| \cdot \sin(\alpha)\cdot \vec n
$$
## Differentiation
### Derivative by first principles
$$
f'(x)=\lim_{h\to0}\frac{f(x+h)-f(x)}{h}
$$
### The Constant Rule
The constant rule state that the first derivative of any constant value is 0.

So formally:
$$
f(x)=c\implies f'(x)=0
$$
### The Scalar Product Rule
The scalar product rule states that if $f(x)$ is the product of some function $g(x)$ and a scalar value $s$ then then $f(x)$ is the product of $s$ and the derivative of $g(x)$.

So formally:
$$
f(x)=sg(x)\implies f'(x)=sg'(x)
$$
### The Sum Rule
The sum rule states that if $f(x)$ is the sum of two functions then $f'(x)$ is the sum of their derivatives.

So formally:
$$
f(x)=g(x)+h(x)\implies f'(x)=g'(x)+h'(x)
$$
### The Product Rule
The product rule states that if $f(x)$ is the product of two functions then $f'(x)$ is the sum of each function multiplied by the derivative of the other function.

So formally:
$$
f(x)=g(x)\cdot h(x) \implies f'(x) = g'(x)\cdot h(x) + g(x)\cdot h'(x)
$$
### The Quotient Rule
The quotient rule states that if $f(x)$ is the result of dividing one function by another function then $f'(x)$ is the difference of the derivative of the numerator multiplied by the denominator and the derivative of the denominator multiplied by the numerator, all divided by the product of the denominator with itself.

So formally:
$$
f(x)=\frac{g(x)}{h(x)} \implies 
f'(x) = \frac{g'(x)\cdot h(x) - g(x)\cdot h'(x)}{h(x)\cdot h(x)}
$$
### The Chain/Composition Rule
The chain rule (or composition rule) states that if $f(x)$ is the composition of 2 functions that $f'(x)$ is the the derivative of the outer function composed with the inner function, multiplied by the derivative of the inner function.

So formally:
$$
f(x)=g(h(x))\implies f'(x)=g'(h(x))\cdot h'(x)
$$
### The Power Rule
The power rule states that if $f(x)$ is of the form $x^t$ where $t\in\mathbb R$ then $f'(x)$ is the product of $t$ and $x^{t-1}$.

So formally:
$$
f(x)=x^t\implies f'(x)=tx^{t-1}
$$
### Logarithm Rule
The logarithm rule states that if $f(x)$ is of the form $\log_n x$ then $f'(x)$ is the reciprocal of the product of $\ln(n)$ and $x$. 

So formally:
$$
f(x)=\log_n (x) \implies f'(x) = \frac{1}{\ln(n) \cdot x}
$$
The above is the general form for differentiating $\log_n(x)$, however often you will see functions of the form $\log(x)$ with no base. In calculus, when working with logs, it is standard to assume that $\log(x)=\ln(x)$. 

You may see a version of the rule above stated as 
$$
f(x)=\log(x)\implies f'(x)=\frac1x
$$
Or as
$$
f(x)=\ln(x)\implies f'(x)=\frac1x
$$

### The Exponential Rule
The exponential rule states that if $f(x)$ is of the form $n^x$ then $f'(x)$ is the product of $\ln(n)$ and $n^x$.

So formally:
$$
f(x)=n^x\implies f'(x)=\ln(n)\cdot n^x
$$
Most commonly you will see this rule when $n=e$. 

$e^x$ is the same as $\exp(x)$. As a result you may see this rule expressed as
$$
f(x)=\exp(x)\implies f'(x)=\exp(x)
$$
### The Trigonometric Rules
The trigonometric rules state that if $f(x)$ is of the form $\sin(x)$ then $f'(x)$ is $\cos(x)$. They also state that if $f(x)$ is $\cos(x)$ then $f'(x)$ is $-\sin (x)$.

So formally:
$$
\begin{split}
& f(x) = \sin(x)\implies f'(x)=\cos(x) \\
& f(x) = \cos(x)\implies f'(x)=-\sin(x)
\end{split}
$$

If you remember that $$
\tan(x) = \frac{\sin(x)}{\cos(x)}
$$You can use a combination of these rules and the quotient rule to find the derivative of $\tan (x)$.
## Integration
### The Scalar Product Rule
The scalar product rule states that if $f(x)$ is the product of a function $g(x)$ and a scalar value $s$, then the integral of $f(x)$ is the product of the integral of $g(x)$ and $s$.

So formally:
$$
f(x)=sg(x)\implies \int f(x)dx = s\cdot\int g(x)dx
$$
### The Sum Rule
The sum rule states that if $f(x)$ is the sum of two other functions $g(x)$ and $h(x)$ then the integral of $f(x)$ is the same as the sums of the integrals of $g(x)$ and $h(x)$.

So formally:
$$
f(x)=g(x)+h(x)\implies \int f(x)dx = \int g(x)dx + \int h(x)dx
$$
### The Power Rule
The polynomial rule states that if $f(x)$ is of the form $x^k$ then the integral of $f(x)$ is the same as $\frac{x^{k+1}}{k+1}$. This is an inverse of the power rule for differentiation, and does not work for $k=-1$.

So formally:
$$
\forall k\in\mathbb{R}\setminus \{-1\},\; f(x)=x^k\implies \int f(x)dx = \frac{x^{k+1}}{k+1}
$$
### The Reciprocal Rule
The reciprocal rule states that if $f(x)$ is of the form $\frac 1x$ then the integral of $f(x)$ is $\ln(x)$. This is an inverse of the logarithm rule for differentiation. The combination of this and the power rule allows us to integrate functions of the form $x^k$ $\forall k\in\mathbb{R}$.

So formally:
$$
f(x)=x^{-1}=\frac1x\implies \int f(x)dx = \ln (x)
$$
### Trigonometric Rules
The trigonometric rules for integration are the inverse of the trigonometric rules for differentiation. These rules state that the integral of $\sin(x)$ is $-\cos(x)$ and the integral of $\cos(x)$ is $\sin(x)$. The integral for $\tan(x)$ is a bit more complicated, and outside the scope of this course, but if curious you can read about it [here](https://math.stackexchange.com/questions/2696282/integral-of-tanx).

So formally:
$$
\begin{split}
& f(x)=\sin(x)\implies \int f(x)dx = -\cos(x)\\
\\
& f(x)=\cos(x)\implies \int f(x)dx = \sin(x)
\end{split}
$$
### The Exponential Rule
The exponential rule is the inverse of  the exponential rule for differentiation. It states that if $f(x)$ is of the form $n^x$ then the integral of $f(x)$ is $\frac{n^x}{\ln(n)}$.

So formally:
$$
f(x)=n^x\implies \int f(x)dx=\frac{n^x}{\ln(n)}
$$
Again this is most common when $n=e$ and therefore $\ln(n)=1$. Because of this, you may see this rule expressed as
$$
f(x)=\exp(x)\implies \int f(x)dx=\exp(x)
$$
### The Logarithm Rule
The logarithm rule is actually **not** the inverse of the logarithm rule from differentiation. It states that if $f(x)$ is of the form $\ln(x)$ then the integral of $f(x)$ is $x\ln(x)-x$.

So formally:
$$
f(x)=\ln(x)\implies \int f(x)dx = x\ln(x)-x
$$

The proof for this uses [integration by parts](https://en.wikipedia.org/wiki/Integration_by_parts), which I recommend you read about but is not needed for this course. If you want to see the full proof you can view it [here](https://www.cuemath.com/calculus/antiderivative-of-lnx/).
## Linear Regression
### Line of best fit
To find the line of best fit $y=ax + b$ we do
$$
\begin{split}
a 
& = \frac{\sum_{i=1}^n(x_i-\bar x)(y_i-\bar y)}{\sum_{i=1}^n(x_i-\bar x)^2} \\
\\
b & = \bar y -a\bar x
\end{split}
$$
Where $\bar x$ and $\bar y$ are the arithmetic means of all $x_k$ and $y_k$ values respectively.
### $R^2$ Formula
$$
R^2 = 1 - \frac{SS_{res}}{SS_{tot}}
$$
Where
$$
\begin{split}
SS_{res} & = \sum_{k=1}^n(y_k-f(x_k))^2 \\
\\
SS_{tot} & = \sum_{k=1}^n(y_k-\bar y)^2
\end{split}
$$
Essentially, $SS_{res}$ is the sum of the squares of the residuals, and $SS_{tot}$ is the sum of the square of the difference between each $y$ value and the mean $y$ value.
## Complex Numbers
### Matrix Form
The matrix form of $z\in\mathbb C$, denoted $\mathbf{M_z}$, is given by 
$$
\mathbf{M_z}=
\begin{pmatrix}
a & -b \\
b & a
\end{pmatrix}
$$
### Polar Coordinate Form
For $z=a+ib$ we say that its **polar form** is 
$$z=(r,\theta)$$
### Trigonometric Form
For $z=a+ib$ with $|z|=r$ and $\arg z=\theta$, the **Trigonometric form** of $z$ is 
$$
z=(r, \theta)=r(\cos\theta+i\cdot\sin\theta)
$$
### Euler Form
For $z=a+ib$ with $|z|=r$ and $\arg z=\theta$, the **Euler form** of $z$ is 
$$z=r\cdot e^{i\theta}$$
### $k^{th}$ root of 
The $k^{th}$ root of a complex number $z=v^k$ is
$$
v=r^{\frac1k}\cdot e^{i\frac{\theta+2m\pi}{k}}
$$
where $m\in\mathbb N$.
## Determinants
### Expansion Formula
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

### Determinant Transpose Rule
$$
\det (A^T) = \det A
$$
### Determinant Multiplication Rule
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

One big consequence of this is that if any two rows of a matrix $A$ are identical, or if any 2 columns of $A$ are identical, then $\det A=0$.
## Spectral Methods
### Characteristic Polynomial
o find the eigenvalues of $A$, we find solutions to the **characteristic equation**
$$
\det(A-\lambda I)=0
$$
We use $\chi(A)$ as a shorthand to denote $\det(A-\lambda I)$.
### Diagonal Matrix
A diagonal matrix for a matrix diagonalisable $A$ is a matrix whose leading diagonal is made of the eigenvalues of $A$
$$
D = B^{-1}AB
$$
### Eigendecomposition
$$
A=BDB^{-1}
$$
where $B$ is a matrix made of eigenvectors of $A$ and $D$ is the diagonal matrix for $A$

Using **eigendecomposition** allows for easy computations of **matrix powers**. This is because
$$
A^n = BD^nB^{-1}
$$
for any diagonalisable matrix $A$.
### Rayleigh Quotient
The **Rayleigh Quotient** is
$$
\frac{\vec v^T A\vec v}{\vec v^T\vec v}=\lambda
$$
where $\vec v$ is an eigenvector of $A$ and $\lambda$ is the associated eigenvalue for $\vec v$.
### Number of Edges
The number of edges $|E|$ in a graph $G$ represented by an adjacency matrix $A$ is exactly
$$
|E|=\frac12\sum^n_{k=1}(\lambda_k(G))^2
$$
Where $\lambda_k$ represents the $k^{th}$ eigenvalue of $A$.
### Chromatic Number
We can use the eigenvalues of the matrix representation $A$ to determine some bounds for this chromatic number, which we will label $C(G)$. 

In particular
$$
1 + \frac{\lambda_{max}(G)}{|\lambda_{min}(G)|}\leq C(G) \leq \lambda_{max}(G) + 1
$$

Note that we use $\lambda_{max}$ and $\lambda_{min}$ specifically because we are working with their real values, not absolute values. I.e. $\lambda_{min}$ is **most negative*** eigenvalue and $\lambda_{max}$ is the **most positive** eigenvalue.
### PageRank Matrix
We can define an $n\times n$ transition matrix $W$ with
$$
w_{ij}=\cases{
\begin{split}
0\;\;& \text{if } (p_j,p_i)\notin L \\
\frac1{|P_{k\leftarrow j}|}\;\; & \text{if } (p_j,p_i)\in L
\end{split}
}
$$
Where $P_{k\leftarrow j}$ is the set of pages linked to by $p_j$.
### Required Space for Image Compression
The total required space is
$$
np + pk + p = p(n + k + 1)
$$
Where 
- $n$ is the height of the
- $k$ is the width of the image
- $p$ is the number of values we choose