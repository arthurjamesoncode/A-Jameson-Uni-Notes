## Vector Spaces
A vector space is a collection of vectors from some set $V$, which can be added together and multiplied by scalars $s$ from some set $F$ such that:
- There is closure under addition;
- There is closure under scalar multiplication;

Closure under addition means that:$$
\forall\vec v, \vec u\in V,\;\vec u + \vec v \in V
$$While closure under scalar multiplication means that:$$
\forall\vec v \in V \text{ and } \forall s\in F,\; s\vec v\in V
$$
Less formally, a vector space is an infinite set of vectors which contains every vector that can be obtained by performing an addition or scalar multiplication on a vector in that set.

Let's now go through some examples and use this definition to prove whether they are or are not vector spaces.
### Example 1
Do the vectors from $\mathbb{R}^n$ with scalars from $\mathbb{R}$ form a valid vector space. Yes, and we can show that they do like so:

Let $\vec v,\vec u$ be fixed but arbitrary vectors such that $\vec v,\vec u\in \mathbb{R}^n$ and $s$ be a fixed but arbitrary scalar such that $s\in \mathbb{R}$

By definition, $\vec v$ and $\vec u$ are $n$-vectors made up of real components. So
$$
\begin{split}
\vec v & = (v_0,...,v_n) \\
\vec u & = (u_1,...,u_n)
\end{split}
$$Using this we can define $\vec u + \vec v$ and $s\vec v$ like so: $$
\begin{split}
\vec u + \vec v & = (v_0+u_0,...,v_n+u_n) \\
s\vec v         & = (sv_0,...,sv_n)
\end{split}
$$
As $v_0,...,v_n\in\mathbb{R}$ and $u_0,...,u_n\in\mathbb{R}$ we know that $v_0+u_0,...,v_n+u_n\in\mathbb{R}$. Therefore $\vec u + \vec v\in\mathbb{R}^n$.

As $s\in \mathbb{R}$ and $v_0,...,v_n\in\mathbb{R}$ we know that $sv_0,...,sv_n\in\mathbb R$. Therefore $s\vec v\in\mathbb R^n$.

As $\vec u + \vec v\in\mathbb{R}^n$ and $s\vec v\in\mathbb R^n$ we know that vectors from $\mathbb R^n$ and scalars from $\mathbb R$ form a valid vector space.
### Example 2
Do the vectors formed from the coefficients of polynomials $\mathbb P_n$ of degree $n$ or less with scalars from $\mathbb R$ form a valid vector space? Yes, and we can show that they will like so:

Let $p(x)$ be a polynomial of degree $a$ and $q(x)$ be a polynomial of degree $b$ where $a,b\leq n$. We know that $p(x)+q(x)$ has a degree of the maximum of $a$ and $b$ as polynomials cannot increase their degree through addition of a polynomial with a lower degree. As $a,b\leq n$, $p(x)\in\mathbb{P}_n$

Let $s\in \mathbb R$. We know that $s\cdot p(x)$ has degree $a$ as multiplication by a scalar does not affect the degree of a polynomial. As $a\leq n$, we know that $s\cdot p(x)\in \mathbb P_n$.
### Example 3
Do all $n$-vectors of unit length with scalars from $\mathbb R$ form a valid vector space? No, and we can show this with a counter example.

Let $\vec v$ be an $n$-vector with a first component of 1 with all other components being 0. We know $$|\vec v| = \sqrt{1^2 + (n-1)\cdot (0^2)}=1$$and therefore $\vec v$ is a unit vector.

For this to be a valid vector space, $\vec v+\vec v$ must also be a unit vector. We know that $\vec v + \vec v$ would have a first component of 2 and the rest of the components would be 0, so we know $$
|\vec v+\vec v| = \sqrt{2^2 + (n-1)\cdot (0^2)}=2
$$And therefore $\vec v+\vec v$ is not a unit vector and this is not a valid vector space.
### Example 4
Do vectors from $\mathbb Z^2$ with scalars from $\mathbb{R}$ form a valid vector space? No, and we can show this with a counter example.

Let $\vec v = (1,1),\; s=0.5$.

This means that $s\vec v=(0.5,0.5)$.

As $s\vec v\notin\mathbb Z^2$, this shows that this is not a valid vector space.
## Linear Independence
Let vectors from $V$ with scalars from $\mathbb R$ be a vector space. 

A linear combination of $\vec v_1,...,\vec v_k\in V$ is an element of $V$ of the form $$
c_1\vec v_1+\cdot\cdot\cdot+c_k\vec v_k
$$where $c_i\in\mathbb{R}\;\forall i\in\{1..k\}$

Vectors are linearly independent if a linear combination $$
c_1\vec v_1+\cdot\cdot\cdot+c_k\vec v_k=\vec 0
$$only when $$
c_1=\cdot\cdot\cdot=c_k=0
$$
>$\vec 0$ means a vector for which every component is 0

Consider the vectors $$
\vec u = (1,0),\; \vec v=(0,1),\; \vec w = (1,1)
$$Are these vectors linearly independent?

The answer is no because $$
1\cdot(1,0) + 1\cdot(0,1) - 1\cdot(1,1) = 0
$$and $1\neq -1$.

Now consider the vectors$$
\vec u = (1,1),\; \vec v = (1,-1)
$$Are these vectors linearly independent?

Let $c_1,c_2\in\mathbb R$ be constants such that $$
c_1\vec u + c_2\vec v = \vec 0
$$
This means that $$
\begin{split}
c_1\cdot(1,1)+c_2\cdot(1,-1) & = (0, 0) \\
(c_1,c_1)+(c_2, -c_2) & = (0,0)
\end{split}
$$giving us the equations $$
\begin{split}
c_1 + c_2 & = 0 \\
c_1 & = -c_2 \\
\\
c_1 - c_2 & = 0 \\
c_1 &= c_2
\end{split}
$$Which means that $c_2 = -c_2$ which is only possible when $c_2$, and therefore $c_1$, is 0.

Therefore $\vec u$ and $\vec v$ are linearly independent.
## Span of Vectors
The span of vectors $v_1,...,v_n$ is the set of all their **finite linear combinations**$$
c_1,\vec v_1+\cdot\cdot\cdot+c_k\vec v_k
$$where $c_i\in\mathbb R$.

Another way to understand linear independence of a set of vectors is to say that no vector is part of the span of the rest of the vectors.

Vectors $\vec e_1 = (1,0)$ and $\vec e_2=(0,1)$ are linearly independent. 

These vectors are called the **standard basis** of $\mathbb R^2$, which means that $$
\text{any }\vec v\in \mathbb R^2 = (x, y) = x\vec e_1 + y\vec e_2
$$
The span of the **standard basis** vectors for $\mathbb R^n$ is $\mathbb R^n$.

For a single vector $\vec v$, linear independence means that $\vec v\neq\vec 0$ and the span of $\vec v$ is a straight line. This is because $c\vec v =0$ only if $c=0$ or $v=0$ and the collection of $c\vec v\; \forall c\in\mathbb R$ is a straight line in the direction of $\vec v$. 

For two vectors $v_1, v_2$, linear independence means that $v_1$ and $v_2$ are not proportional to each other. Meaning they are not parallel or anti-parallel. The span of $v_1$ and $v_2$ forms a plane. This is because every possible vector on this plane is a linear combination of $v_1$ and $v_2$.

We call $v_1$ and $v_2$ **basis** vectors of a vector space $\mathbb R^2$. This is different to **standard basis** vectors. 

The **basis** of a vector space is any set of linearly independent vectors which can span the vector space

The **standard basis** of a vector space $\mathbb R^m$ is the set of linearly independent vectors which can span the vector space where each vector is a unit vector for which 1 component is 1 and the rest are 0.

You can see an image that can give you an idea of why this works below below:
![[span.png]]
## Dimensions
So far, you may understand the dimension of a vector space as the number of components of a vector from that vector space.

**This is not always the case.**

The definition of the **dimension** of a vector space is the minimum number of **basis** vectors required to span a vector space.

Understanding the dimension of a vector as the number of components of vector from a vector space overlaps with the **correct**, formal definition for vector spaces formed by vectors from $\mathbb R^n$ and scalars from $\mathbb R$, but not all vector spaces.

Take for example the vector space formed from vectors from $\mathbb R^3$ for which all components are equal with scalars from $\mathbb R$. We will call this vector space $V$.

We can show that this is a valid vector space like so:

Let $\vec u,\vec v\in V$, $s\in \mathbb R$

By definition we know that $$
\begin{split}
\vec u & = (x,\;x,\;x)\\
\vec v & = (y,\;y,\;y)
\end{split}
$$Where $x,y\in\mathbb R$ and from this we can deduce $$
\begin{split}
\vec u + \vec v & = (x+y,\;x+y,\;x+y) \\
s\vec v & = (sy,\;sy,\;sy) 
\end{split}
$$
As $x,y,s\in\mathbb R$ we know that $x+y\in\mathbb R$ and $sy\in\mathbb R$ and so $\vec u + \vec v\in V$ and $s\vec v\in V$. Therefore $V$ is a valid vector space.

As these vectors require each component to be equal we only require 1 vector to span the whole space. $\vec v = (1,1,1)$ can be combined with some scalar $c$ to form any vector vector of the form $\vec u = (x,x,x)$.

And so the dimension of $V$ is actually 1, despite vectors from $V$ being made up of 3 components.
## Subspace
Consider a 2D plane in $\mathbb R^3$ that can be defined as $$
\{(x,y,0):x,y\in\mathbb R\}
$$We know this is a vector space, as $$
(a,b,0)+(c,d,0)=(a+c,b+d,0)
$$and $$
s(a,b,0)=(sa,sb,0)
$$where $s\in \mathbb R$

As $\mathbb R^3$ with scalars from $\mathbb R$ is already vector space, that makes this 2D plane a **subspace**. 

Since we know $$
(x,y,0)=x(1,0,0)+y(0,1,0)
$$we know that we only need to 2 vectors to span this whole space, which proves that the dimension of this sub space is 2.