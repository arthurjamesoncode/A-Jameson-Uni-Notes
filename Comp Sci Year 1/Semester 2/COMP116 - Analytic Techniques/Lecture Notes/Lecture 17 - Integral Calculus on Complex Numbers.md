When integrating real valued functions, the result is linked to **measuring** the **area under the curve**. In complex functions no such analogy is possible. We also cannot **order** complex numbers in a consistent way so we don't have a way to compute definite integrals in the same way we usually do.

This means that we need a new understanding of both **what we are computing** and **how can we compute it**.
## Complex Integration
Consider $f:\mathbb C\to\mathbb C$ and $p,q\in\mathbb C$.

How can we compute a definite integral of $f$ between $p$ and $q$?
$$
\int_p^qf(z)dz
$$
We can use the tricks we were using for differential calculus to define $f$ as
$$
f(z)=u(z)+i\cdot v(z)
$$
where $u$ gives the real part and $v$ gives the imaginary part. For the time being, it is not particularly useful to treat $z$ as two real values and so we can ignore this.

Now we can break this down into the sum of 2 different definite integrals
$$
\int_p^qf(z)dz=\int_p^qu(z) + i \cdot\int_p^qv(z)
$$
but since complex numbers cannot be ordered the idea of "the area under $f(z)$ spanning from $p$ to $q$" does not actually work.

Instead, we must **move from $p$ to $q$ in the complex plane**. So what does this mean?
### Contour Integrals & Parameterising the Curve
If we have two points, $p$ and $q$, in the complex plane, we can plot these points and draw any number of infinite curves connecting the two. Choosing a specific curve is the same as describing the way we move from $p$ to $q$.

Choosing a specific path $\gamma$, allows us to compute the **contour integral of $f(z)$ along path $\gamma$** is given by
$$
\int_{\gamma}f(z)dz
$$
In some special cases we will have a **closed curve** (the start and end of $\gamma$ coincide) to denote these contour integrals we use
$$
\oint_{\gamma}f(z)dz
$$

The (real) range that we are interested in is $[Re(p), Re(q)]$, if we define a function $\phi:\mathbb R\to\mathbb C$ such that 
$$\phi(Re(p))=p,\; \phi(Re(q))=q$$
We can then split $\phi$ into both its real and imaginary parts
$$
x(t) = Re(\phi(t)),\; y(t)=Im(\phi(t))
$$
giving use $\phi$ in terms of two $\mathbb R\to\mathbb R$ functions
$$
\phi(t)=x(t)+i\cdot y(t)
$$
for any $t$ such that $Re(p)\leq t \leq Re(q)$.

Now we have an expression for our curve from $p$ to $q$ in terms of a single **real parameter**. Fittingly this process is called **parameterising the curve**.

>The function we choose for $\phi$ is now incredibly important to the process of finding an complex integral. How exactly to choose a good $\phi$ is difficult and you will not be asked to choose a good $\phi$ at any point in this module.
>
>You will only be tested on how to calculate integrals given $f(z),\;p,q\in\mathbb C$, and a specific **parameterisation**. Meaning you need to understand parameterisation, and learn the formula below.

It can be shown that, when a function $\phi:\mathbb R\to\mathbb C$ parameterises the curve $\gamma$ which joins $p$ and $q$ then 
$$
\int_\gamma f(z)dz \equiv \int_{Re(p)}^{Re(q)}f(\phi(t))\phi'(t)dt
$$

>You do not need to understand the proof of this identity, but if you want to read about it you can [here](https://en.wikipedia.org/wiki/Line_integral).
>
>It is, however, important to memorise the formula.

Now recall that
$$
\int_\gamma f(z)dz=\int_p^qf(z)dz=\int_p^qu(z) + i \cdot\int_p^qv(z)
$$

This means, given curve $\gamma$ parameterised by a function $\phi$, we finally have a full expression for our integral
$$
\int_\gamma f(z)dz = \int_{Re(p)}^{Re(q)}Re\Bigl(f\bigl(\phi(t)\bigr)\phi'(t)\Bigr) dt + i \cdot \int_{Re(p)}^{Re(q)} Im\Bigl(f\bigl(\phi(t)\bigr)\phi'(t)\Bigr) dt
$$
### Example 1
Consider the function $f:\mathbb C\to\mathbb C$ given by $f(a+ib)=a^2+ib^2$ and the points $p=0$ and $q=1+i$. How could we integrate $f$ between $p$ and $q$?

Well first we need a **path** $\gamma$ from $p$ to $q$ parameterised by a function $\phi:\mathbb R\to\mathbb C$. In this case we can use a straight line from 0 to (1,1) given by $\phi(t)=t+it$. 

In this module, you don't need to know **how** to choose a good $\phi$, you will be given one whenever you are asked to calculate a complex integral. At minimum, you will always be able to a straight line between the two points.

Now we need to find our expression for 
$$
f\bigl(\phi(t)\bigr)\phi'(t)
$$
which requires us to differentiate $\phi$.

Since
$$
\phi(t) = u(t) + i \cdot v(t)
$$
where $u(t)=v(t)=t$, we can differentiate $\phi$ using the sum rule as 
$$
\phi'(t) = u'(t) + i \cdot v'(t)
$$
We know, from the product rule, that $u'(t)=v'(t)=1$ which means
$$
\phi'(t) = 1 + i
$$
Now that we have this we can find
$$
\begin{split}
f\bigl(\phi(t)\bigr)\phi'(t) 
& = (t^2 + i\cdot t^2)(1+i) \\
& = t^2+it^2+it^2+i^2t^2\\
& = 2it^2
\end{split}
$$
If we recall how we find our **contour integral** we can see that 
$$
\int_\gamma f(z)dz = \int_{0}^{1}Re\Bigl(2it^2\Bigr) dt + i \cdot \int_{0}^{1} Im\Bigl(2it^2\Bigr)dt
$$

We can make our lives a bit easier by recognising that $2it^2$ has no real part and so can be forgotten, leaving us with
$$
\int_\gamma f(z)dz = i \cdot \int_{0}^{1} 2t^2
$$

And now we can find our **contour integral** through simple substitution
$$
\begin{split}
\int_\gamma f(z)dz 
& = i \cdot \int_{0}^{1} 2t^2dt \\
& = i \cdot \Bigl[ \frac23t^3 \Bigr]^1_0 \\
& = i \cdot \Bigl( \frac23(1)^3-\frac23(0)^3 \Bigr) \\
& = \frac23i
\end{split}
$$
### Example 2
Consider if we wanted to find the **contour integral** of a function $f:\mathbb C \to\mathbb C$ given by $f(x)=\frac1z$ along **the path of the unit circle** $\mu$.

In this case, $\mu$ represents a **closed path**. In practice this doesn't change how we compute the integral, but does mean we use the following notation for the integral
$$
\oint_uf(z)dz
$$

First we need a way to **parameterise** this path, along with start and end points on this path. 
We can choose the function 
$$\phi(t)=e^{2i\pi t}$$
and the values $p=q=1$. Since $e^{2i\pi}=e^0=1$, this means we can use $t\in[0,1]$.

Now we need to find $\phi'(t)$, for which we must remember the [[Lecture 8 - First Derivative#The Exponential Rule|exponential rule]].
$$
\phi'(t) = 2i\pi\cdot e^{2\pi it}
$$

Now that we have an expression for $\phi(t)$ we can find
$$
\begin{split}
f\bigl(\phi(t)\bigr)\phi'(t)
& = \frac{1}{e^{2\pi it}}\cdot 2\pi i \cdot e^{2\pi it} \\
& = 2\pi i
\end{split}
$$
So now we can find our integral. Notice again that since we have no real part it can be forgotten.
$$
\begin{split}
\oint_uf(z)dz 
& = \int_0^1 2\pi i\;dt \\
& = 2\pi i \cdot \int_0^1 1\;dt \\
& = 2\pi i \cdot \bigl[t \bigr]^1_0 \\
& = 2\pi i \cdot (1 - 0) \\
& = 2\pi i
\end{split}
$$
### Applications in CS - Counting Objects
The techniques outlined in this note and its predecessors provide a basic introduction to complex analysis. One of the most powerful practical applications of these techniques lies in the study of **counting objects**.

Imagine we wanted to determine exact or asymptotic estimates for the number of objects of a particular type having a given size. Two tools which are very useful for this are the notion of a Generating Function and a result called the (Generalised) Cauchy Integral Formula.

>This section is meant to give you an idea of how the things you are being taught are used. You won't be tested on your knowledge of this, and this is only a very brief overview.

Imagine a given sequence of objects
$$
\langle a_0, a_1, a_2,\cdots,a_n,\cdots\rangle
$$

This sequence represents the number of objects of size $n$ (denoted by $a_n$). So $a_0$ represents the number of objects with size 0 etc.

This could represent any number of things, for example:
- The number of binary trees with $n$ leaves;
- The number of permutations of $n$ items which leave at least one item in the same position;
- The sum of $\frac{1}{n^2}$.

Being able to accurately estimate quantities like this is often crucial when it comes to determining how an algorithm behaves **on average**.
### Generating Functions
To estimate these values we can use a **generating function**.

Take the function $G$ given by
$$
G(z)=\sum^{\infty}_{n=0}a_nz^n
$$
This is a generating function, which uses the given sequence to create some value.

While this might not immediately seem useful, we can (depending on the objects in the sequence) manipulate the sum to find a simpler **closed form**.

Consider the sequence given by "The number of binary trees with $n$ leaves". We can define a function 