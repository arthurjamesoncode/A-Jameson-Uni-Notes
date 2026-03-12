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

Well first we need a **parameterised path** from $p$ to $q$. In this case we can use a straight line from 0 to (1,1) given by $\phi(t)=t+it$. (You don't need to know **how** to choose a good $\phi$, you will be given one whenever you are asked to calculate a complex integral).

