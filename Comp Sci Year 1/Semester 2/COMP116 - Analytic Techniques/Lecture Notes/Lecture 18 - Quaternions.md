Quaternions are an extension of the idea of the **complex plane** to a 3D space. Considering how complex numbers themselves are an extension of the **real numbers** (a 1D space) and are made of $1+1=2$ disparate parts, it makes sense that for quaternions (and extension of 3D space) we use $3+1=4$ disparate parts.

Since quaternions are pretty much just a representation of a 4D space, visualising what they actually are is very difficult (or more accurately impossible). In the lecture we were shown [this video](https://www.3blue1brown.com/?v=quaternions) by 3Blue1Brown which explains what they are and helps us understand them in terms of a projection of this 4D space onto 3D space. I recommend watching the full video.

>Olga seemed to suggest that we won't be tested much on quaternions. 
>
>At minimum, she concretely said that we won't be tested on **quaternion multiplication** since the convenient form of it requires the cross product of two 3D vectors, which we have not been shown how to compute. 
>
>She didn't say as much for the other operations on quaternions, but they are all relatively simple extensions of what we have done so far. In fact, there is a question about **unit-quaternions** in the mock test, but this is just a Euclidean norm question.
>
>I would recommend familiarising yourself with the basic operations and Hamilton rules, but not worrying too much about whether you fully understand this for the test.
## Quaternion Structure & Convention
Recall that complex numbers are any number $z=a+ib$ where $a,b\in\mathbb R$ and $i^2=-1$.

We can represent these as 2-vectors $(a,b)$ in the Complex Plane.

Similarly we can represent **quaternions** as 4-vectors $(w, x, y, z)$ where in the same vein as $z=a+ib$ we have 
$$
q=w + ix + jy + kz
$$
where $w,x,y,z\in\mathbb R$ and $i$, $j$, and $k$ are defined via the **Hamilton rules**.

The Hamilton rules state that
$$
i^2=j^2=k^2=-1
$$
but also that
$$
\begin{split}
jk = -kj = i \\
ki = -ik = j \\
ij = -ji = k \\
\end{split}
$$
The constants $i,j,k$ are all imaginary and all square to $-1$, but importantly are not equal.

>Notice that $jk\neq kj$. This is because **quaternion multiplication** is **not-commutative** meaning that the order of the operands matters. This will be discussed in more depth later.

We use $\mathbb H$ to denote the set of all quaternions. Notice that
$$
w + xi + 0j + 0k\in\mathbb H
$$
meaning that $\mathbb C \subset \mathbb H$.

For any arbitrary $q\in\mathbb H$ we can represent it 2 ways
$$
q=w + ix + jy + kz
$$
as shown above or
$$
q = [w, \underline{v}]
$$
where $\underline v$ is a the vector $\langle x,y,z \rangle\in\mathbb R^3$.

Before we used the notation $\vec v$ to indicate that $v$ is a vector. We can still use this notation, but are using the notation $\underline v$ to help draw a distinction between other vectors and quaternions.

The notation $\mathbb H$ is in honour of [William Hamilton](https://en.wikipedia.org/wiki/William_Rowan_Hamilton) who is credited with founding Quaternion Algebra. He is also the namesake of the Hamilton rules.
## Quaternion Operations
Quaternion operations are mostly a simple extension of the operations on complex numbers. A slight exception exists in **quaternion multiplication** where the extension is a little more complicated, and will be discussed when we get there.

Each operation will be given a brief explanation in plain English, before I show the general case. These are mostly simple so I won't be providing examples.
### Addition
The addition of two quaternions $p$ and $q$ is a new quaternion where each component is the sum of the corresponding components from $p$ and $q$.

So formally, if $p,q\in\mathbb H$, $p=a+ib+jc+kd$, and $q=w+ix+jy+kz$ then 
$$
p+q = (a + w) + i(b + x) + j(c + y) + k(d + z)
$$
or equivalently if we use $p=[a, \underline u]$ and $q=[w, \underline v]$ then
$$
p + q = [a + w, \underline u + \underline v]
$$
### Multiplication by a Scalar
The multiplication of a quaternion $q$ by a scalar value $s$ is a new quaternion where each component is the product of $s$ with the corresponding component from $q$.

So formally if $s\in\mathbb R$ and $q=w+ix+jy+kz\in\mathbb H$ then
$$
sq = sw + isx + jsy + ksz
$$
or equivalently if we use $q=[w,\underline v]$ then
$$
sq = [sw,s\underline v]
$$
### Conjugate
The conjugate of a quaternion $q$ is the same as $q$ but with the negation of all the **imaginary parts** of $q$.

So formally, if $q=w+ix+jy+kz\in\mathbb H$ then
$$
\bar q = w - ix - jy - kz
$$
or equivalently if we use $q=[w,\underline v]$ then
$$
\bar q = [w, -\underline v]
$$
### Modulus
The modulus of a quaternion $q$ is the same as the magnitude of the equivalent 4-vector in the Euclidean norm. Essentially it is the square root of the sum of the squares of each component.

So formally if $q=w+ix+jy+kz\in\mathbb H$ then
$$
||q|| = |q| = \sqrt{w^2 + x^2 + y^2 + z^2}
$$
or equivalently if we use $q=[w,\underline v]$ then
$$
||q|| = |q| = \sqrt{w^2 + ||\underline v||^2}
$$

If $||q||=1$ then we call $q$ a **unit quaternion**.
### Reciprocal
Given $q=w+ix+jy+kz\in\mathbb H$ how can we compute $\frac1q$?

We actually use the exact same process detailed [[Lecture 14 - Complex Numbers#Complex Division|here]], in the complex division portion of Lecture 14. 

Essentially if we multiply $q$ by its conjugate we get
$$
q\bar q = w^2 + x^2 + y^2 + z^2
$$
which has no imaginary part and the same as $||q||^2$.

This means we can use the exact same process of **rationalising the denominator** to arrive at the conclusion that
$$
\frac1q = \frac{\bar q}{||q||^2}
$$
If we combine this with **multiplication** we can then do **quaternion division**.
### Quaternion Products
Given $s,t\in\mathbb H$ where $s=a+ib+jc+kd$ and $t=w+ix+jy+kz$ how can we find the product of $s$ and $t$?

We could use the normal rules we have established for expanding brackets, along with the **Hamilton** rules, to expand the expression
$$
s \cdot t = (a + ib + jc + kd)(w + ix + jy + kz)
$$

This does work and will simplify to a new quaternion, but gets incredibly messy given 4 components and makes it hard to understand the actual effect in 3 dimensions.

There is a much more elegant solution which uses our [[Lecture 4 - Vectors and Operations#Scalar/Dot Product|vector products]].

If we write $s=[\alpha, \underline u]$ and $t=[\beta,\underline v]$ we can then write
$$
s \cdot t = [\alpha\beta - \underline u \cdot \underline v,\; \alpha\underline v + \beta\underline u + \underline u \times \underline v]
$$
where $\underline u \cdot \underline v$ is the **scalar** (or dot) product of our imaginary vectors and $\underline u\times \underline v$ is **vector** (or cross) product of our imaginary vectors.

Note that since we know that vector/cross product is **not commutative** we also know that **quaternion product** is also **not commutative**.

Put simply
$$
s\cdot t \neq t\cdot s
$$
## Applications in 3D graphics
We have seen, earlier in this module, the ways in which we can use matrix vector products for transformations.

This works fairly well in 2 dimensions but in 3 dimensions rotational effects become very awkward and costly if we still use matrix vector products directly.

One of the reasons for this is **Gimbal Lock** (pictured below). This is a phenomenon where some directions of movement are lost when the axes of two "gimbals" become parallel.
![[Gimbal_Lock_Plane.gif]]

To understand this in terms of matrices, a matrix for a rotation is defined in terms of **trigonometric functions** which can give undefined values when combining rotations about some angles.

This means that the graphical simulation either **freezes** or otherwise [behaves strangely](https://www.reddit.com/r/GamePhysics/comments/9gonwb/fifa_18_seemed_to_me_like_this_belongs_here_lol/).

Quaternions offer a solution, as they **cannot** lead to Gimbal Lock.
### Rotations Using Quaternions
Imagine we want to rotate a point $(x,y,z)$ about some **axis of rotation** (an infinite line in 3 dimensions) by some angle $\theta$.

We can choose a quaternion 
$$
q_{\theta}=\Bigl[\cos(\frac\theta2), \sin(\frac\theta2)\underline v\Bigr]
$$
choosing $\underline v$ such that it has the same direction as our **axis of rotation** and makes $q_{\theta}$ a **unit-quaternion**.

We can then represent the computation "Rotate $\underline w=\langle x,y,z \rangle$ by $\theta$ about $\underline v$" as
$$
q_\theta \cdot [0, \underline w] \cdot q_{\theta}^{-1}
$$

The **imaginary vector** portion of the result is the new point after the rotation has been done.

