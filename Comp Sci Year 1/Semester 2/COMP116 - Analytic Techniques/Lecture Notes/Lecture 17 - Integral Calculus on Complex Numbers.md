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

Choosing a specific path $\gamma$, allows us to compute the **contour integral of $f(z)$ along path $\gamma$**. Which is denoted by
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
giving us $\phi$ in terms of two $\mathbb R\to\mathbb R$ functions
$$
\phi(t)=x(t)+i\cdot y(t)
$$
for any $t$ such that $Re(p)\leq t \leq Re(q)$.

Now we have an expression for our curve from $p$ to $q$ in terms of a single **real parameter**. Fittingly this process is called **parameterising the curve**.

For example, imagine we were using the points $p=2+4i$ and $q=6+12i$, we could choose a function $\phi(t)=t+2it$. If we substitute in $Re(p)$ and $Re(q)$ we can see that we get back $p$ and $q$ respectively
$$
\begin{split}
\phi(2) 
& = 2 + 2i(2) \\
& = 2 + 4i \\
\\
\phi(6) 
& = 6 + 2i(6) \\
& = 6+ 12i
\end{split}
$$
Since, $\phi(Re(p))=p$ and $\phi(Re(q))=q$ we can say that $\phi$ parameterises the line between $p$ and $q$.

The function we choose for $\phi$ is now incredibly important to the process of finding a complex integral. Choosing a good $\phi$ can sometimes be difficult, but you will not be asked to choose a good $\phi$ at any point in this module.

In general though, you can usually use a straight line for distinct points, which means your $\phi$ will look like
$$
\phi(t) = t + i \cdot (mt + c)
$$
and if you want to use a closed curve you can use a circle, which means your $\phi$ will look something like
$$
\phi(t)=re^{it}
$$

>You will only be tested on how to calculate integrals given $f(z),\;p,q\in\mathbb C$, and a specific $\phi(t)$ which **parameterises** the curve. You may also be tested on whether a certain parameterisation is valid or not.
>
>This means you need to understand parameterisation, and learn the formula below, but don't actually need any more information (at least to pass this module).

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

Imagine we wanted to determine exact or asymptotic estimates for the number of objects of a particular type having a given size. To do this we can use a Generating Function and a result called the (Generalised) Cauchy Integral Formula.

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

We can use a **generating** function to get an **infinite** polynomial expression for this, which we can manipulate to a **closed** finite expression.

We can then differentiate this **finite** expression $n$ times, and pass in 0 to get the number of objects of size $n-1$. Exactly why this works you can read about [[#Finding the Coefficients/The Generalised Cauchy Integral Formula|below]]. 

Given a function $G(z)$, we can find the $n^{th}$ derivative of $G(z)$ (denoted by $g^{(n)}(z))$ using the formula below
$$
g^{(n)}(z) = \frac{n!}{2\pi i}\oint_C\frac{g(\beta)d\beta}{(\beta-z)^{(n+1)}}
$$

This is one of the **primary uses** of complex integration.

You can have a look below for a more in depth exploration of the example of "The number of binary trees with $n$ leaves".
### Generating Functions
To estimate these values accurately we can use a **generating function**.

Take the function $G$ given by
$$
G(z)=\sum^{\infty}_{n=0}a_nz^n
$$
This is a generating function, which generates a **polynomial** which has coefficients of $z^n$ that match the given sequence. 

Importantly $z^n$ is not a value, but instead a placeholder which represents the **object of size $n$** with which we are concerned. The coefficient $a_n$ represents the number of objects of size $n$ which exist.

Another way to understand this, is that $G(z)$ represents the **sum** of all of the given objects of all possible sizes.

While this might not immediately seem useful, we can (depending on the objects in the sequence) manipulate the sum to find a simpler **closed form**.

Consider the sequence given by "The number of binary trees with $n$ leaves". We can define a **recursive** function which gives us this sequence.

First, lets quickly define what a binary tree is, and what a leaf is. A **binary tree** is a tree in which each node can only have up to two children. These children represent a **left subtree** and a **right subtree**. A **leaf** is any node with a tree that has **no children**.

We will also add 1 more restriction on top of this. We are counting the number of **full binary trees**, also called **proper binary trees**. In a full binary tree each node always has **exactly** zero or two children. This is an important distinction to make as otherwise there are an infinite amount of binary trees with only a single leaf.

Note that, when we say a tree is **unique** we are only considering the structure of the tree for this, not the data it holds.

So now we have a recursive definition for our **full binary tree**, it either
- Is a single node with no children (base case)
- Is a root node with a left and a right subtree (recursive rule)

First we need the base case, a tree with a single root node and no children. There is only one of these and it has 1 leaf and so $t_1=1$.

Now lets consider $t_2$, this is the number of of binary trees with only 2 leaves. We know that there is only 1 of these as well, a single node with 2 children.

Lets consider $t_3$, we have:
- A root node with two children where the left child also has 2 children
- A root node with two children where the right child also has 2 children

And finally if we consider $t_4$ we have:
- A root node with two children, where both children have 2 children
- A root node with two children, where the left child has two children, and the left child's left child has two children
- A root node with two children, where the left child has two children, and the left child's right child has two children
- A root node with two children, where the right child has two children, and the right child's left child has two children
- A root node with two children, where the right child has two children, and the right child's right child has two children

We can see that keeping track like this can get unruly very quickly, which is why we want to find some kind of generalised function.

If $w(t)$ is the function for the number of leaves of a tree then
$$
w(t) = w(t_l) + w(t_r)
$$
where $t_l$ represents the left subtree and $t_r$ represents the right subtree.

Understanding it like this, we can find the number of trees with $n$ leaves as the number of **choices of unique subtrees** we can combine. 

If you recall the [[Lecture 28 - Combinatorics#The Product Rule|product rule]] from combinatorics, we know that if $t_k$ and $t_{n-k}$ represent the number of unique subtrees with $k$ and $n-k$ leaves respectively, then just by joining these subtrees we can create $t_k \cdot t_{n-k}$ unique subtrees.

This is true for all values of $1 \leq k < n$. This lets us use the [[Lecture 28 - Combinatorics#Sum Rule|sum rule]] from combinatorics to find $t_n$ like so
$$
t_n = \sum_{k=1}^{n-1}t_k\cdot t_{n-k}
$$

Now that we have a way to get $t_n$ we can create a **generating function** like so
$$
B(z)=\sum_{n=0}^{\infty}t_nz^n
$$
where $t_n$ is the number of full binary trees with $n$ leaves. Remember that $z^n$ isn't an actual value, but is a placeholder to represent the idea of a tree of size $n$.

If we understand $B(z)$ as the **sum** of all **full binary trees**, we can break this down into our base case and our recursive rule. We know that there is a **single** binary tree with only 1 leaf, which in $B(z)$ is represented by $z$. 

We also know that there are **infinite** binary trees which are the **combination** of two binary trees. We can represent all of these as $B(z)\cdot B(z)=B(z)^2$.

This means we can re-write our generating function **in terms of these recursive rules** to get
$$
B(z) = z + B(z)^2
$$

Now that we have this **recursive definition** of our generating function we can rearrange it to get
$$
B(z)^2-B(z)+z = 0
$$
And we can now use the **quadratic formula** to find a solution for this in terms of $z$
$$
\begin{split}
B(z) 
& = \frac{-(-1)\pm\sqrt{(-1)^2-4(1)(z)}}{2(1)} \\
& = \frac{1\pm\sqrt{1-4z}}{2} \\
\end{split}
$$
There is still one question about this solution, **which sign do we choose**?

When we have a generating function of the form 
$$
G(x) = a_0x^0+a_1x^1+a_2x^2+\cdots
$$
notice that if we set $x=0$, all that remains is the coefficient of the $x^0$ term (since $0^0=1$), which is the number of objects of size 0.

We know that no binary trees exist which have no leaves, and we laid out possible trees for up to $t_4$. This means that 
$$
B(z) = 0z^0 + 1z^1 + 1z^2 + 2z^3 + 5z^4 + \cdots
$$

This means that $B(0)$ **must be** 0, as the coefficient of $z^0$ is 0 and this is the only term which is not removed from the function.

So if we look back at our solution
$$
\begin{split}
B(0) 
& = \frac{1 + \sqrt{1-4(0)}}{2} \\
& = \frac22 \\
& = 1 \\
\\
B(0)
& = \frac{1 - \sqrt{1-4(0)}}{2} \\
& = \frac02 \\
& = 0
\end{split}
$$

We can see that the **plus** sign leads to an invalid answer meaning that
$$
B(z) = \frac{1 - \sqrt{1-4z}}{2}
$$

Since this is a finite expression, and $B(z)$ is an infinite function we call this the **closed form** of $B(z)$. It is common to denote infinite functions with a capital letter and closed forms with a lower case letter.

So
$$
\begin{split}
B(z) & = \sum^{\infty}_{n=0}t_nz^n \\
\\
b(z) & = \frac{1 - \sqrt{1-4z}}{2}
\end{split}
$$
### Finding the Coefficients/The Generalised Cauchy Integral Formula
Now we have a **finite expression** $b(z)$ (closed form) for the **infinite function $B(z)$** defined in terms of $z$. So how does this help us when it comes to calculating the number of binary trees with $n$ leaves.

To do this we need to find the coefficient of $z^n$ in $B(z)$. 

We saw above how when we choose $z=0$ then $B(z)$ becomes the number of objects of size 0. 
Since $B(z)$ is a polynomial, we can use the power rule to generalise this to 
$$
\frac{d^nB}{dz^n}(0) = n!\cdot a_n 
$$

This means that to find the coefficient of $z^n$ in $B(z)$ we can differentiate $B(z)$ $n$ times, pass in $z=0$ and then divide by $n!$.

The problem with this is that differentiating $n$ times is not always trivial, especially in the case of **complex functions**.

The way we get around this is to use the [Generalized Cauchy Integral Theorem](https://dspace.mit.edu/bitstream/handle/1721.1/49419/18-112Fall-2006/NR/rdonlyres/Mathematics/18-112Fall-2006/5F5BE6FC-6F17-4BE5-9C8E-C9325ACCAD58/0/lecture13.pdf) to calculate the $n^{th}$ derivative of a function.

Let $G(z)$ be a generating function with a closed form of $g(z)$. We denote the $n^{th}$ derivative of $g(z)$ by $g^{(n)}(z)$.

Now if we choose a closed contour $C$ then
$$
g^{(n)}(z) = \frac{n!}{2\pi i}\oint_C\frac{g(\beta)d\beta}{(\beta-z)^{(n+1)}}
$$

Since we are looking for a value of $a_0$, we can substitute in $z=0$ and see our formula for $a_n$.
$$
a_n = \frac{n!}{2\pi i}\oint_C\frac{g(\beta)d\beta}{\beta^{(n+1)}}
$$
And so we can finally find use this to estimate the **binary trees with $n$ leaves**, or other objects of size $n$.
### Summary
Both **generating functions** and **Cauchy's Integral Formula** would require a whole modules worth of teaching to cover in detail, and as such we have only touched the surface of them.

This whole section is not something you will be tested on during this module. Instead, it is simply to give you an idea of why these ideas which we are being taught are actually useful.



