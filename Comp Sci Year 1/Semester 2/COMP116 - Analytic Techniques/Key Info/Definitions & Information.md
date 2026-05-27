---
cssclasses:
  - flashcards
---
## Trigonometry
### Trig Values
| $\theta$       | $\sin\theta$      | $\cos\theta$      | $\tan\theta$ |
| -------------- | ----------------- | ----------------- | ------------ |
| $0$            | $0$               | $1$               | $0$          |
| $\frac\pi4$    | $\frac{\sqrt2}2$  | $\frac{\sqrt2}2$  | $1$          |
| $\frac\pi2$    | $1$               | $0$               | $undefined$  |
| $\frac{3\pi}4$ | $\frac{\sqrt2}2$  | $-\frac{\sqrt2}2$ | -1           |
| $\pi$          | 0                 | -1                | 0            |
| $\frac{5\pi}4$ | $-\frac{\sqrt2}2$ | $-\frac{\sqrt2}2$ | 1            |
| $\frac{3\pi}2$ | -1                | 0                 | $undefined$  |
| $\frac{7\pi}4$ | $-\frac{\sqrt2}2$ | $\frac{\sqrt2}2$  | -1           |
| $2\pi$         | 0                 | 1                 | 0            |

## Vector Spaces
### What is a Vector Space?
A vector space is a collection of vectors from some set $V$, which can be added together and multiplied by scalars $s$ from some set $F$ such that:
- There is closure under addition;
- There is closure under scalar multiplication;
### What is a linear combination?
$$
c_1\vec v_1+\cdot\cdot\cdot+c_k\vec v_k
$$
where $c_i\in\mathbb{R}\;\forall i\in\{1..k\}$
### What is the span of a set of vectors?
The span of vectors $v_1,...,v_n$ is the set of all their **finite linear combinations**$$
c_1,\vec v_1+\cdot\cdot\cdot+c_k\vec v_k
$$where $c_i\in\mathbb R$.
### When are vectors linearly independent?
Vectors $v_1,...,v_k$ are linearly independent if  
$$
c_1\vec v_1+\cdot\cdot\cdot+c_k\vec v_k=\vec 0
$$
is true only when 
$$
c_1=\cdot\cdot\cdot=c_k=0
$$

Equivalently, it can be said that $v_1,...,v_k$ are linearly independent if for all $1\leq i \leq k$
$v_i$ is not part of the span of $\{v_1,...,v_k\} \setminus v_i$.
### What does basis vectors of vector space mean?
For a vector space $V$, the basis vectors of the vector space is any set of vectors $v\in V$ which span the entirety of $V$.
### What are standard basis vectors?
The **standard basis** of a vector space $\mathbb R^m$ is the set of linearly independent vectors which can span the vector space where each vector is a unit vector for which 1 component is 1 and the rest are 0.
### What are the dimensions of a vector space?
The **dimension** of a vector space is the minimum number of **basis** vectors required to span the vector space.
### What is a subspace?
Any vector space within a larger vector space.
## Linear Maps
### What is a linear map?
A linear transformation, also called a linear map, is a type of function $f$ from $\mathbb R^m\to \mathbb R^k$. 

A function $f:\mathbb R^m\to \mathbb R^k$ is a linear map if, and only if, for all $\vec u,\vec v\in\mathbb R^m$ and $s\in\mathbb R$ 
$$
f(s\vec v) = sf(\vec v)
$$
and
$$
f(\vec u + \vec v) = f(\vec u) + f(\vec v)
$$
Another way to understand these conditions is that a linear map **cannot move the origin**.

Any linear map $f$ is determined by the images $f(\vec e_1),...,f(\vec e_m)$ of a **standard linear basis** $\vec e_1,...,\vec e_m$.

We can represent this a $k\times m$ matrix of the linear map $\mathbf{A}$ which consists of $m$ columns that are the values of $f(\vec e_1),...,f(\vec e_m)$ in the output dimension $k$.
### What does composition of two linear maps mean?
The composition of two linear maps, is the single linear map created by applying both linear maps back to back. It is the same as the matrix product of the two maps.

When applying the composition $P\cdot Q$ to a linear map, this is the same as applying $Q$ first and then applying $P$.
### What is an affine map?
An affine map is any transformation which isn't the linear map. This is things like translations since they move the origin?
### How can we turn an affine map into a linear map?
By increasing the matrix dimensions to $n+1$, and adding the translation vector as the first $n$ items in the final column of the new matrix.

## Calculus
### What is a first derivative?
The first derivative of $f(x)$ is the function which gives us the gradient of the line tangent to a curve given by $f(x)$ and is denoted by:
- $f'(x)$
- $\frac{dy}{dx}$ 
- $\frac{df}{dx}$
### What is a critical point?
The **critical points** of a function are any values $x$ such that $f'(x)=0$.
### What types of critical points are there?
- Maximum points - Was increasing and starts to decrease
- Minimum points - Was decreasing and starts to increase
- Inflection points - Flattens out and continues in the same direction
### What is a second derivative?
The second derivative of a function $f(x)$ is the derivative of $f'(x)$ denoted by $f''(x)$.
### How do you determine the type of a critical point?
- If $f'(x)=0$ and $f''(x)<0$ then $(x,f(x))$ is a (possibly local) **maximum**.
- If $f(x)=0$ and $f''(x)>0$ then $(x,f(x))$ is a (possibly local) **minimum**.
- If $f'(x)=0$ and $f''(x)=0$ then $(x,f(x))$ it can be an **inflection point**, or **minimum** or **maximum**
### What is a partial derivative?
A partial derivative is a derivative of a multivariable function, in which you treat all variables except one as a constant.

So for a function $f(x, y)$ the $x$ partial derivative is given by $$
f'_x(x,y)=\frac{\partial f}{\partial x}=\lim_{h\to0}\frac{f(x+h, y) - f(x, y)}{h}
$$but we can just use our standard rules for computing derivatives.
### What is the Nabla?
The gradient function for a multivariable function is a vector that packages the partial derivatives together. We call this function the "nabla" and denote it by $\nabla f$.

So formally:$$
\nabla f(x,y) 
= \begin{bmatrix}
f'_x(x,y) \\
f'_y(x,y)
\end{bmatrix}
$$This can also be expanded to more dimensions.
### What critical points exist in 3D space
- A **saddle point** means that the surface curves upwards in one direction and downward in another. It is named this because it looks similar to a saddle.
- A (local) **minimum** is a point which curves upwards in all directions.
- A (local) **maximum** is a point which curves downwards in all directions.
### What is the hessian?
The Hessian is a matrix made of all the partial second derivatives of a 2 variable function
$$
\mathbf{H} =
\begin{bmatrix}
f_{xx} & f_{xy} \\
f_{yx} & f_{yy} 
\end{bmatrix}
$$

- $f_{xx}$ means the second partial derivative of $f$ with respect to $x$ both times;
- $f_{xy}$ means the second partial derivative of $f$ with respect to $x$ first and then $y$;
- $f_{yx}$ means the second partial derivative of $f$ with respect to $y$ first and then $x$;
- $f_{yy}$ means the second partial derivative of $f$ with respect to $y$ both times.
### How do you determine the type of critical point for multivariate functions?
Using the determinant of the hessian at $(x,y)$ and the value of $f_{xx}(x,y)$.

$$
D = f_{xx}(x,y) \cdot f_{yy}(x,y) - f_{xy}(x, y)^2
$$

- $D(x,y) < 0$ means that the point is a **saddle point** (explained below);
- $D(x, y) > 0$ and $f_{xx}(x,y) > 0$ means that the point is a (local) **minimum**;
- $D(x, y) > 0$ and $f_{xx}(x,y) < 0$ means that the point is a (local) **maximum** 
- $D(x, y) > 0$ and $f_{xx}(x,y) = 0$ is **not possible**. 
- $D(x, y) = 0$ is **inconclusive**, and we will need to compute higher order derivatives.
### How do you compute integrals from first principles?
We use a function $A$ derived from the method of exhaustion 
$$
A(h, a, b)=\lim_{h\to0}\sum^{N-1}_{k=0}hf(a+kh)
$$
We assume that $f(x)=F'(x)$ and so
$$
f(x) = \lim_{h\to0}\frac{F(x+h)-F(x)}{h}
$$
Which lets us get
$$
\begin{split}
A(h,a,b) 
& = \lim_{h\to 0}\sum^{N-1}_{k=0}h\cdot(\frac{F(a+(k+1)h)-F(a+kh)}{h}) \\
& = \lim_{h\to 0}\sum^{N-1}_{k=0}{F(a+(k+1)h)-F(a+kh)}
\end{split}
$$
We still can't completely remove the limit as $h$ still exists in the denominator of the expression for $N$, but we can show
$$
A(h,a,b)=\lim_{h\to 0}F(b)-F(a+h)
$$
by noticing that much of the sum cancels itself out.

Since we no longer use $N$, we can now remove the limit and safely set $h=0$ to get
$$
A(a, b) = F(b) - F(a)
$$

In conclusion, the area under a the graph of $f(x)$ between $x=a$ and $x=b$ is given by
$$
F(b)-F(a)
$$
where $f(x)=F'(x)$.
### What is an antiderivative?
The function $F(x)$ for which $f(x)=F'(x)$ is called the **anti-derivative** of $f(x)$.

We know from the constant rule that when we differentiate a constant it becomes 0, because of this we can't be sure that $F(x)$ does not have a constant term. To indicate this we have to add the term $C$ to our anti-derivative to indicate some arbitrary constant.
### What does signed area mean?
When we compute the area under a graph, we are actually computing the **signed area**. Area above the graph has a positive sign and area below the graph has a negative sign.
## Complex Numbers
### What is a complex number?
A complex number $z$ is any number of the form
$$
z=a+ib
$$
Where $i=\sqrt{-1}$ and $a,b\in\mathbb R$.
### What does complex conjugate mean?
The complex conjugate of a complex number $z$ is the same as $z$ but with the negation of it's imaginary part. We denote the complex conjugate as $\bar z$.

If $z\in\mathbb C$ then:
- $Re(\bar z)=Re(z)$
- $Im(\bar z)=-Im(z)$
### What are the primitive roots of unity?
They are the solutions to $x^k=1$
## Spectral Methods
### What is the determinant of a matrix?
The **determinant** of a matrix is a single number that indicates how much the linear map **scales** the vector or group of vectors. For groups of vectors from $\mathbb R^2$, this measures how much the total **area** increases. For groups of vectors from $\mathbb R^3$ however, this measures how much the total **volume** increases.
### What are the eigenvalues and eigenvectors of a matrix?
Given an $n\times n$ matrix $A\in\mathbb R^{n\times n}$, find all scalar values $\lambda\in\mathbb R$ for which there is an $n$-vector $\vec v_\lambda\neq0$ satisfying the equation
$$
A\cdot\vec v_\lambda = \lambda\cdot \vec v_\lambda
$$
The scalar values $\lambda$ are called the **eigenvalues** of $A$.

The $n$-vectors $\vec v_\lambda$ are called the **eigenvectors** of $A$.

If $\vec v_\lambda$ is an eigenvector of $A$, then so is $c\vec v_\lambda$ for all $c\in\mathbb R$.

Geometrically, this means that matrix $A$, when applied as a linear map, scales all vectors in the direction of $\vec v_\lambda$ by the factor $\lambda$.
### What is the spectrum of a matrix?
The list of all eigenvalues $\lambda_1$ is called the spectrum of $A$ and is denoted like so
$$
\sigma(A)=(\lambda_1, \lambda_2, \lambda_3,...,\lambda_n)
$$
By convention, the eigenvalues are ordered from largest absolute value $|\lambda_1|$ to smallest absolute value $|\lambda_n|$ .

$\lambda_1$ is called the **dominant eigenvalue** of $A$. If $\lambda_1$ appears multiple times, then $A$ is said to have **multiple dominant eigenvalues**.

>This is the consensus I am finding online, however the lecture slides state that $\lambda_1$ is only called the dominant eigenvalue if unique. I doubt this will be relevant, but it's probably useful to know there is some variation in how people use it.
### What is the spectral radius?
The maximum of the absolute values of all eigenvalues is called the spectral radius and is denoted with $\rho(A)$. 
### What do we know about complex eigenvalues?
For **complex values** if $\lambda$ is an eigenvalue $\bar\lambda$ is also an eigenvalue. You can understand this is you recall that all eigenvalues of $A$ are roots of an $n$ degree polynomial.
### What do we know about symmetric matrices and their eigenvalues?
If $A$ is symmetric, then all eigenvalues $\lambda_k$ of $A$ are real. Symmetric matrices are not the only matrices which have exclusively real eigenvalues, but they are guaranteed to have them.
### What is the Perron-Frobenius Theorem?
The Perron Frobenius Theorem states that, if $A\in\mathbb R^{n\times n}$ and $A_{i,j}>0$ for all $1\leq i,j\leq n$, then:
- There is a unique, dominant, real, positive eigenvalue $\lambda_{pf}$ associated with it.
- This eigenvalue has an eigenvector (called the **Perron vector**) $\vec v_{pf}$ which contains only real positive components.
- For any initial positive $\vec v_0\neq \vec 0$, the sequence of normalised iterations converges to the perron vector.

This last condition formally states that 
$$
\frac{A^k\cdot\vec v_0}{|A^k\cdot\vec v_0|} \to \vec v_{pf} \text{ when } k\to\infty
$$

There is a generalisation of this theorem to some **non-negative** matrices as well.
### What is the power method?
- Choose an initial, non-zero guess for $\vec v_0$. The simplest guess is to choose a vector made of all 1s.
- Set $i=0$
- Compute $\vec w_{i+1}$ using the formula $\vec w_{i+1}=A\vec v_i$.
- Normalise to find $\vec v_{i+1}$ using the formula $\vec v_{i+1}=\frac{\vec w_{i+1}}{|\vec w_{i+1}|}$
- Set $i=i+1$
- Repeat these computations until $\vec v_i$ stops changing, or $i$ reaches a user defined max value.
### How are the SVD matrices derived?
Given an image matrix $W$ we can find two square matrices $W\cdot W^T$ and $W^T\cdot W$.

If we find the spectra $(\lambda_1,\lambda_2,...,\lambda_i,...,\lambda_n)$ of these matrices we can use it to derive $U$, $\Sigma$ and $V^T$.
- $\Sigma$ is defined as containing elements $s_{ij}$ such that
$$
s_{ij}=\cases{
\begin{split}
0\;\; & \text{ if } i\neq j \\
\sqrt{\lambda_i}\;\; & \text{ if i = j}
\end{split}
}
$$
- $U$ is defined as containing columns such that the $i^{th}$ column of $U$ is an eigenvector of $W\cdot W^T$ with eigenvalue $\lambda_i$.
- $V^T$ is defined as containing rows such that the $i^{th}$ row of $V^T$ is an eigenvector of $W^T\cdot W$ with eigenvalue $\lambda_i$