There are many different ways to represent complex numbers, which have many different use cases. This lecture will be spent going over various useful forms.
## Matrix Representations
We can represent any complex number $z$ as a $2\times 2$ matrix. For $z=a+ib\in\mathbb C$, the matrix form of $z$, denoted $\mathbf{M_z}$, is given by 
$$
\mathbf{M_z}=
\begin{pmatrix}
a & -b \\
b & a
\end{pmatrix}
$$
We can represent all the basic operations as manipulations of $2\times 2$ matrices. We can use this in convenient ways.

The following section lays out which matrix operations map to which complex number operations, and then shows a general proof that they do.
### Addition
Take $u = a + ib,\; v=c+id$, we know the matrix form of these two numbers
$$
\mathbf{M}_u=\pmatrix{a & -b \\ b & a},\;
\mathbf{M}_v=\pmatrix{c & -d \\ d & c}
$$
We see that if we add these matrices we get
$$
\begin{split}
\mathbf{M}_u
& =
\pmatrix{a & -b \\ b & a}
+
\pmatrix{c & -d \\ d & c} \\
& =
\pmatrix{a+c & -(b+d) \\ b + d & a + c}
\end{split}
$$
If we add them normally you can see how the result fits the matrix
$$
u+v = (a+c)+i(b+d)
$$
### Conjugate
The complex conjugate fits the **transpose** operation. I don't think transpose operations have been taught as part of this course yet but it simply describes flipping the matrix on its diagonal (starting at the top left and ending at the bottom right).

So if we have $u=a+bi$ with matrix representation of 
$$
\mathbf{M}_u=\pmatrix{a & -b \\ b & a}
$$
We can see that the transpose of $\mathbf M_u$ is 
$$
\mathbf M_{\bar u}=\pmatrix{a & b \\ -b & a}
$$
Which we can see fits $\bar u = a - bi$
### Modulus
The modulus of of a complex number is the same as the **determinant** of the matrix representation of the number. 

Recall that the determinant $D$ of a $2\times 2$ matrix given by
$$
M = \pmatrix{a & b \\ c & d}
$$
is
$$
D = ad-cb
$$

So if we have $z=a+ib$ with matrix representation of 
$$
\mathbf M_z = \pmatrix{a & -b \\ b & a}
$$
we can see the determinant of this matrix is 
$$
\begin{split}
D_z 
& = a^2 - (-b^2) \\
& = a^2 + b^2 \\
& = |z|
\end{split}
$$
### Multiplication
We can see that multiplication of complex numbers is the same as the multiplication of their matrix representations.

Let $u=a+ib,\;v=c-id$ with matrix representations of
$$
M_u = \pmatrix{a & -b \\ b & a},\;
M_v = \pmatrix{c & -d \\ d & c}
$$
We can see that 
$$
\begin{split}
M_u\cdot M_v 
& = 
\pmatrix{a & -b \\ b & a}
\pmatrix{c & -d \\ d & c} \\
& = \pmatrix{ac-bd & -(ad + bc) \\ ad +bc & ac -bd}
\end{split}
$$
If we multiply $u$ and $v$ normally we can see 
$$
\begin{split}
v\cdot u 
& = (a+ib)(c+id) \\
& = ac + ibc + iad + i^2bd \\
& = ac -bd + i(ad+bc)
\end{split}
$$
and this fits the matrix representation.

Note as well that if we flip the order of the matrix multiplication it doesn't matter
This makes multiplication of complex numbers a **commutative** operation, unlike standard matrix multiplication.
## Complex Numbers as a Vector Space
The **complex plane** forms a **vector space**, you can look back to [[Lecture 5 - Vector Spaces]] for a refresher.

The **basis vectors** of this vector space are the vectors of $1$ $\langle1, 0\rangle$ and $i$ $\langle0, 1\rangle$.

This means that we know that additions of complex numbers are also **vector additions**.

We also know that complex numbers can be represented as a $2\times 2$ matrix. This means that each complex number represents some **linear map** or **linear transformation**.

We will now go over some key transformations.
### Multiplication as Rotation and Scaling
Lets consider the matrix representations of $i$ and $1$:
$$
M_1 =
\pmatrix{1 & 0 \\ 0 & 1},\;
M_i = 
\pmatrix{0 & -1 \\ 1 & 0}
$$
Notice that $M_1$ is just the $2\times 2$ identity matrix, however $M_i$ is a transformation.

We can understand what transformation $M_i$ represents by remembering that the **columns** of $M_i$ are the **images** of the standard basis vector after they have been transformed by $M_i$.

This means we know that $\langle1, 0\rangle$ becomes $\langle0, 1\rangle$ and $\langle0, 1\rangle$ becomes $\langle-1, 0\rangle$. You can see this transformation goes from the red dots
![[before_i_mult.png]]
to the blue dots
![[after_i_mult.png]]

From this, we can clearly see that multiplication by $i$ represents a **counter-clockwise rotation by $\frac\pi2$ or $90\degree$.

If instead of $1$ and $i$ we look at $a$ and $ib$ we can see
$$
M_a=\pmatrix{a & 0 \\ 0 & a},\;
M_{ib}=\pmatrix{0 & - b \\ b & 0}
$$

From this, we know if we have a complex number $z=a+ib$ then multiplication by $Re(z)$ is equivalent to scaling by $a$ and multiplication by $Im(z)$ is equivalent to a rotation of $\frac\pi2$ and a scaling by $b$.

This means that multiplication by the complex number $z=a+ib$ is the same as the vector sum of the vectors resulting from:
- A counter clockwise rotation of $\frac\pi2$ and a scaling by $b$;
- A scaling by $a$.

You can see an example of this below
![[complex_mult_transform.png]]
## Conjugate as Reflection
The complex number $z=a+bi$ has the complex conjugate $\bar z=a-bi$ which has the matrix representation of =
$$
M_{\bar z}=\pmatrix{a & b \\ -b & a}
$$
What this means is that the complex conjugate represents a reflection of $z$ in the **real-axis**.

You can see this below for $z=5+3i$
![[geometric_conjugate.png]]

## Polar Coordinate Form
Polar coordinate form is a way to represent **vectors**, and therefore complex numbers, which uses the vectors **magnitude and direction** instead of its end points.

For $z=a+ib$ we say that its **polar form** is 
$$z=(r,\theta)$$
where $r=|z|$ and $\theta$ is the **counter clockwise angle** from the **real axis** (measured in radians) to the vector $(a, b)$.

We denote the angle of $z$ as $\arg z$, and it is also called the **phase** of $z$. It  is important to remember these terms.

There are infinitely many representations of any single complex number as  
$$
(r, \theta) = (r, \theta + 2\pi k)\; \forall k\in\mathbb{Z}
$$
The principle value is denoted by $\text{Arg}\;z$ and must be in the range $[0,2\pi)$ or $(-\pi, \pi]$.

>Computers (and sometumes humans) often find it easier to use the range $(-\pi,\pi]$ but both are perfectly valid.

We can calculate $\text{Arg}(a+ib)$ by using a special function $atan2(b, a)$. This function is essentially $\arctan(\frac ba)$, except that it gives back a value in the range $(-\pi, \pi]$ ($\arctan$ only gives values in the range $(-\frac\pi2, \frac\pi2)$) and takes into account the quadrant of the grid the point $(a, b)$ lies in.

So $atan2(1, 1) = \frac\pi4$, and $atan(1, -1)=\frac{3\pi}4$ while $\arctan(\frac{1}{-1})=-\frac\pi4$.
## Trigonometric Form and The Euler Form
For $z=a+ib$ with $|z|=r$ and $\arg z=\theta$, the **Euler form** of $z$ is 
$$z=r\cdot e^{i\theta}$$
So how do we get this?

Well we actually start by looking at the **unit circle**. We can recall the the point $(x,y)$ on a unit circle is exactly $(\cos\theta, \sin\theta)$, where $\theta$ is the angle between the $x$-axis and the vector given by $(x,y)$.
![[sin_cos.png]]

This means that the set of complex numbers $z$ where $|z| = 1$ can be represented by
$$
z_1=(1, \theta) = \cos\theta + i\cdot sin\theta
$$
Since we are representing these numbers just using their **magnitude** and angle, we can say that
$$
z=(r, \theta)=r(\cos\theta+i\cdot\sin\theta)
$$
We call this representation the **trigonometric form**.

We can then use [Euler's formula](https://en.wikipedia.org/wiki/Euler%27s_formula), which is 
$$
e^{i\theta}=\cos\theta+i\sin\theta
$$
to get 
$$
z = (r, \theta) = re^{i\theta}
$$

You need to know **Euler's formula**, but you don't need to know its proof. I recommend reading about it if you want to stretch yourself.
## In All Forms
Lets quickly look at $z=1+i$ in all the forms discussed.

First we have the **matrix form** of
$$
M_z=\pmatrix{a & -b \\ b & a}\pmatrix{1 & -1 \\ 1 & 1}
$$

Then, for the rest of the forms, we need $r=|z|$, which we can see is
$$
|z| = \sqrt{1+1}=\sqrt{2}
$$
and we also need $\theta=\text{Arg}\; z$ which we know is
$$
\text{Arg}\;z=\frac\pi4
$$
This lets us write $z$ in its **polar form** of
$$
z = (r, \theta)=(\sqrt2,\frac\pi4)
$$
as well as its **trigonometric form** of 
$$
z = r(\cos\theta+i\sin\theta)=\sqrt2(\cos\frac\pi4+i\sin\frac\pi4)
$$
and finally its **Euler form** of
$$
z=re^{i\theta}=\sqrt2e^{\frac\pi4i}
$$
## Consequences of the Euler Form
Consider the product of a two complex numbers given by 
$$
\begin{split}
z_1 = r_1e^{i\theta_1} \\
z_2 = r_2e^{i\theta_2}
\end{split}
$$
We can get the complex number $z_1\cdot z_2$ like so
$$
z_1\cdot z_2=r_1r_2e^{i(\theta_1+\theta_2)}
$$
This also works in the trigonometric form, since Euler's form is just a simplification of that
$$
z_1+z_2=r_1r_2(\cos(\theta_1 + \theta_2)+i\sin(\theta_1 + \theta_2))
$$

Consider now the number $z^n$ where $z\in\mathbb C$, what does this look like for various $z$? 

Well first lets consider when $e^{i\theta}$ (when $r=1$). What happens if we square it?
$$
z^2=e^{i(\theta+\theta)}
$$
Since we add the angles, it is obvious that, in this case, multiplying $z$ by $z$ is actually a rotation of $z$ by $\theta$.

What we can see is that 
$$
z^n = e^{in\theta}
$$
And so $z^n$ is actually $n$ rotations of $z$ by the angle $\theta$.

Consider $e^{\frac\pi2\theta}$, which is just $i$. Lets table out the first 5 values

| $n$ | $i^n$ |
| --- | ----- |
| 0   | $1$   |
| 1   | $i$   |
| 2   | $-1$  |
| 3   | $-i$  |
| 4   | 1     |
And view the graph below 
![[i_to_n.png]]
We can see that this graph and tables shows $i^n$ is cyclic, and functions as a repeated rotation of $\frac\pi2$.

Now consider $e^{ik}$. What will we see if we look at this graph?
![[e_to_ik.png]]
As before, we can witness that, as the power increases, more  and more rotations by 1 (in radians) are applied to this number.

Notice also that, since $1$ doesn't divide nicely into $2\pi$, that for $k=7$, it isn't immediately cyclic like $i^n$.

But what about when $r\neq1$? Well in this case we get 
$$
z^2 = r^2e^{i(\theta+\theta)}
$$
Which we can see is a scaling of $z$ by $r$.

From this we can see that $z^n$ where $z=re^{i\theta}$ is actually a rotation by $n\theta$ and a scaling by $r^{n-1}$.

We can see this in $(1+i)^k$ (given by $\sqrt{2}^ke^{\frac\pi4ik})$, which creates this outward spiral as $k$ increases which you can see on the graph below
![[(i+k)_to_k.png]]

Likewise, if you consider $(0.5+0.5i)^k$ (given by ${\frac{\sqrt2}2}^ke^{\frac\pi4ik})$, you can see that it creates this inward spiral as $k$ increases
![[(05+05i)_to_k.png]]
## Roots of Complex Numbers
How can we calculate the $k^{th}$ root of a complex number?

Consider a given complex number $u=re^{i\theta}$ which can be written as $v^k$ where $k\in\mathbb Z^+$.

We know that
$$
\begin{split}
v 
& = u^{\frac1k} \\
& = r^{\frac1k} \cdot e^{i\frac{\theta}k}
\end{split}
$$
Giving us 1 value for $v$, but can we find any more?

Well we know that 
$$
u=re^{i\theta}=re^{i(\theta + 2\pi)}
$$
which actually means there are infinite possible values of $\theta$ for any given $u$. In particular, with regards to the problem of finding the $k$th root of $u$, this means that as long as $v^k=re^{i(\theta+2m\pi)}$ where $m\in\mathbb Z$ then $v$ is also a $k^{th}$ root of $u$.

Let's quickly evaluate what this means for a specific $k$, let's choose $k=3$. Consider the table below of possible angle values $\alpha$ for our $3^{rd}$ root of $re^{i\theta}$.

| $m$ | $\alpha$                                                                                                              |
| --- | --------------------------------------------------------------------------------------------------------------------- |
| $0$ | $\frac{\theta+2\cdot0\cdot\pi}{3}=\frac{\theta}3$                                                                     |
| 1   | $\frac{\theta+2\cdot1\cdot\pi}{3}=\frac{\theta+2\pi}3=\frac{\theta}{3}+\frac{2\pi}{3}$                                |
| 2   | $\frac{\theta+2\cdot2\cdot\pi}{3}=\frac{\theta+4\pi}3=\frac{\theta}3+\frac{4\pi}3$                                    |
| 3   | $\frac{\theta+2\cdot3\cdot\pi}{3}=\frac{\theta+6\pi}3=\frac{\theta}3+2\pi$                                            |
| 4   | $\frac{\theta+2\cdot4\cdot\pi}{3}=\frac{\theta+8\pi}3=\frac{\theta}3+\frac{8\pi}3=\frac{\theta}3+\frac{2\pi}{3}+2\pi$ |
Notice that when $m=k$ (in this case $m=3$), the number obtained is exactly $2\pi$ greater than the value when $m=0$, and when $m=k+1$ (in this case $m=4$) the number obtained is exactly $2\pi$ greater than the value when $m=1$.

This example suggests to us that there are exactly $k$ unique **principal**, meaning in the range $[0,2\pi)$, values for the $k^{th}$ root of a complex number $u$.

Lets now try and prove the general case.

Let $u=re^{i\theta}=v^k$ where $k\in\mathbb Z^+$ and $m\in\mathbb N$. 

Observe that
$$
\begin{split}
(r^{\frac1k}\cdot e^{i\frac{\theta+2m\pi}{k}})^k=re^{i(\theta+2m\pi)}
\end{split}
$$
Since $m\in\mathbb N$ this means that
$$
re^{i(\theta+2m\pi)}=re^{i\theta}=u
$$
and therefore we know that $v$ is given by
$$
v=r^{\frac1k}\cdot e^{i\frac{\theta+2m\pi}{k}}
$$
where $m\in\mathbb N$.

Now all we need to prove is how many values of $m$ give a unique value.

Observe
$$
\begin{split}
v
& = r^{\frac1k}\cdot e^{i\frac{\theta+2n\pi}{k}} \\
& = r^{\frac1k}\cdot e^{i(\frac{\theta}k+\frac{2(k+n-k)\pi}{k})} \\
& = r^{\frac1k}\cdot e^{i(\frac{\theta+2k+2n\pi-2k\pi}{k})} \\
& = r^{\frac1k}\cdot e^{i(\frac{\theta+2(k+n)\pi}{k}-\frac{2k\pi}k)} \\
& = r^{\frac1k}\cdot e^{i(\frac{\theta+2(k+n)\pi}{k}-2\pi)}
\end{split}
$$
We can see from this that $\forall m\in\mathbb N$, 
$$
\frac{\theta+2n\pi}{k}=\frac{\theta+2(k+n)\pi}{k}-2\pi
$$
which shows us that the angle for $m=n$ is exactly $2\pi$ less than the angle for as $m=n+k$. 

Since $e^{i\theta}=e^{i(\theta+2\pi)}$ is shows that only the values from $m=0$ to $m=k-1$ offer unique roots.

And so we have proved that there are exactly $k$ unique **principle** values for the $k^{th}$ root of a complex number.
### Primitive Roots of Unity
Lets consider the $k^{th}$ roots of $u=1=e^{0i}$.

We know we have $k$ distinct roots $v_m,\;0 \leq m < k$, given by
$$
v_m = e^{\frac{2\pi m}{k}}
$$

These roots represent the solutions to $x^k-1=0$, and are called the **primitive roots of unity**.

Primitive roots of unity underpin the [Fourier Transform](https://en.wikipedia.org/wiki/Fourier_transform) which is widely used in signal processing and other electronics applications.

The [Discrete Fourier Transform](https://en.wikipedia.org/wiki/Discrete_Fourier_transform) has a key use in computer science as the basis of the fastest known multiplication algorithm.