## Ordering Complex Numbers
Over the last two lectures we have been learning about complex numbers. One of the most interesting aspects of these numbers is that they **cannot be ordered** in the same way that **real** numbers can be.

Think about this. Each complex number $z=a+ib$ can be represented as a vector $(a, b)$. How can we order vectors?

One answer would be to look at the **magnitude** of the vector and try to order them off of this. In a lot of cases this is very trivial, and allows us to see which number is **larger** (by this metric). 

However, there are infinitely many vectors of any particular length (represented by a circle), so how could we decide which of these vectors is larger. One answer could be the **angle**, but since 
$$
re^{i\theta}=re^{i(\theta+2\pi)}=re^{i(\theta-2\pi)}
$$
angle also falls apart as a way to order these vectors.

This is something that is useful to understand as we start to work with calculus on complex numbers. In particular, this causes huge problems for integral calculus.
## Differentiating Real to Complex Functions
How can we differentiate a function $f:\mathbb C \to \mathbb C$ which maps from complex number to complex number? This question quite complicated, since complex numbers have two fundamentally different parts. 

Lets first consider a subset of these functions, any function $f:\mathbb R\to\mathbb C$ which maps from a real number to a complex number.

We can understand these functions as **two real-valued** functions $f_{Re}$ and $f_{Im}$ such that:
$$
f(x) = f_{Re}(x)+i\cdot f_{Im}(x)
$$
and, since $i$ is just a constant such that $i=\sqrt{-1}$, this means that we can simply differentiate $f(x)$ using the **sum rule** to get
$$
f'(x)=f'_{Re}(x)+i\cdot f'_{Im}(x)
$$
as well as do the same thing with integration to get
$$
\int^q_p f(x)dx=\int^q_pf_{Re}(x)dx+i\cdot\int^q_pf_{Im}(x)dx
$$

This is fairly simple, but it gets much more complicated when it comes to differentiating complex to complex functions.
## Differentiating Complex to Complex Functions
When our function is $f:\mathbb R\to\mathbb C$, our input is a single **real** number. This is not true when our function is $f:\mathbb C\to\mathbb C$ as now we take in a single **complex** number instead.

But this whole time we have been representing complex numbers as pairs of real numbers, so maybe we can define our $f:\mathbb C\to\mathbb C$ as a **multivariate** function.
$$
f(z) = f(a + ib) = f(a, b)
$$

After doing this, we can steal an idea from when we were differentiating **real to complex** functions and represent $f$ as a pair of functions that give us our **real** and **imaginary** parts. The only difference is that this time we require 2 **multivariate** functions. So
$$
f(a, b) = u(a, b) + i \cdot v(a, b)
$$
So now we are dealing strictly with **real-valued** functions with **two variables**. This means that we can apply **partial derivatives** to find our derivative.

There are still some issues with this. Think back to the **first-principles** formula for the first derivative
$$
f'(x)=\lim_{h\to 0}\frac{f(x+h)-f(x)}{h}
$$

Now, if you notice that we are still just applying this formula to complex numbers, you might have realised a problem. That problem being that $h\in\mathbb C$ and $\lim_{h\to0}$ actually encapsulates both
$$
Re(h)\to 0,\; Im(h)\to0
$$
This basically means that we have **infinite** directions from which $h$ can approach 0 and this leads to a very important consequence: "For the derivative of a function $f:\mathbb C\to\mathbb C$ to be well defined, it must be the case that **all** of the **infinite** ways for $h$ to approach 0 must be equivalent".

Essentially if you approach 0 from 1 direction, lets say along the **real**-axis, it should be the same as approaching from another direction, lets say along the **imaginary**-axis.

This requirement gives rise the **Cauchy-Riemann Conditions**.
### The Cauchy Riemann Conditions
Consider a function $f:\mathbb C\to\mathbb C$ such that
$$
f(z)=f(a,b)=u(a,b)+i\cdot v(a,b)
$$

The **Cauchy-Riemann** conditions state that for $f'(z)$ to be well defined via **partial derivatives** with respect to $u(a,b)$ and $v(a,b)$ it must be the case that
$$
\frac{\partial u}{\partial a} = \frac{\partial v}{\partial b}\; \mathbf{AND}\; \frac{\partial u}{\partial b} = -\frac{\partial v}{\partial a}
$$
In plain English the **Cauchy-Riemann** conditions state two things:
- That the partial derivative of the **real part** of the function with respect to the **real part** of the input must be the same as the partial derivative of the **imaginary part** of the function with respect to the **imaginary part** of the input;
- That the partial derivative of the **real part** of the function with respect to the **imaginary part** of the input be the same as the negation of the partial derivative of the **imaginary part** of the function with respect to the **real part** of the input.

This (**informally**) states that the infinite ways to approach 0 are all equivalent, meaning that we can find $f'(z)$ by applying the same set of standard rules that we usually do.

We can also see what this means geometrically. 

Consider a function $f$ (which maps a vector to another vector), a vector $X$, and a complex number $z$.

If the result of multiplying $X$ by $z$ and then applying $f$ is the same as the result of applying $f$ to $z$ and then multiplying by $X$ then $f$ satisfies the Cauchy-Riemann conditions. Essentially it must be the case that $df(zX)=zdf(X)$ for $f$ to satisfy the Cauchy-Riemann conditions.

You can see this pictured below
![[Cauchy-Riemann.svg.png]]

We know that multiplication by a complex number $z=a+ib$ and vector $\vec v$ is essentially the addition of the vector obtained by multiplying $\vec v$ by $a$ and the vector obtained by multiplying $\vec v$ by $ib$. Multiplication by $a$ is a scaling, multiplication by $ib$ is a rotation and a scaling, and multiplying by $a+ib$ is the addition of multiplying by both.

For the order of application of $f$ and multiplication by $z$ to not matter, it must be the case that $f$ does not do anything which **changes** how a rotation or scaling would be applied. We will see this in an example later.

>This section is meant to give you an idea of why complex functions must conform to the Cauchy-Riemann conditions in order to have well-defined derivatives, but you do not need to understand all of this to answer the questions on the test.
>
>For this module, you are just expected to know how to **show** these functions conform to the Cauchy-Riemann conditions as well as how to differentiate functions which do conform (the latter is just an application of partial derivatives, which we have covered).
### Example 1
Consider the function $f:\mathbb C\to\mathbb C$ given by $f(z)=z^2$. How can we differentiate this function? Well first we need to check if this satisfies the Cauchy-Riemann conditions. If it doesn't we **can't** differentiate it at all.

First let $z=a+ib$, we can see that
$$
\begin{split}
f(a+ib)
& = (a+ib)^2 \\
& = a^2 + 2iab + i^2b^2 \\
& = a^2 - b^2 + i(2ab)
\end{split}
$$
letting us define 
$$
f(a, b) = u(a, b) + i\cdot v(a, b)
$$
where
$$
u(a,b)=a^2-b^2,\; v(a, b)=2ab
$$

Now we can find our partial derivatives of $u$ and $v$ with respect to both $a$ and $b$ just by using our standard rules
$$
\begin{split}
\frac{\partial u}{\partial a} &= 2a \\
\frac{\partial u}{\partial b} &= -2b \\
\\ 
\frac{\partial v}{\partial a} &= 2b \\
\frac{\partial v}{\partial b} &= 2a  
\end{split}
$$

Using these can check the **Cauchy-Riemann** conditions
$$
\begin{split}
\frac{\partial u}{\partial a} & = \frac{\partial v}{\partial b} \\
2a & = 2a \\
\\
\frac{\partial u}{\partial b} & = -\frac{\partial v}{\partial a} \\
-2b & = -(2b)
\end{split}
$$
and observe that they are satisfied, meaning that our function $f(z)=z^2$ is differentiable as normal. 

So now we can find $f'(z)$ by simply applying the power rule to get $f(z)=2z$.

Now observe
$$
f'(z) = 2z = 2a + 2ib
$$
which is the same as
$$
f'(z) = \frac{\partial u}{\partial a} + i\frac{\partial v}{\partial b}
$$
which again is the same as
$$
f'(z) = \frac{\partial v}{\partial a} + i\cdot (-\frac{\partial u}{\partial b})
$$
### Example 2
Consider the function $f:\mathbb C \to\mathbb C$ given by $f(z)=\bar z$. How could we differentiate this function? Well first we need to check if this satisfies the Cauchy-Riemann conditions. If it doesn't we **can't** differentiate it at all.

Let $z=a+ib$, we can see that
$$
f(a+ib)=a-ib
$$
letting us define
$$
f(a, b) = u(a, b) + i \cdot v(a, b)
$$
where 
$$
u(a, b) = a,\; v(a, b) = -b
$$

Now we can find our partial derivatives of $u$ and $v$ with respect to both $a$ and $b$ just by using our standard rules
$$
\begin{split}
\frac{\partial u}{\partial a} &= 1 \\
\frac{\partial u}{\partial b} &= 0 \\
\\ 
\frac{\partial v}{\partial a} &= 0 \\
\frac{\partial v}{\partial b} &= -1  
\end{split}
$$

This lets us check our **Cauchy-Riemann** conditions 
$$
\begin{split}
\frac{\partial u}{\partial a} & = \frac{\partial v}{\partial b} \\
1 & \neq -1 \\
\\
\frac{\partial u}{\partial b} & = -\frac{\partial v}{\partial a} \\
0 & = -(0)
\end{split}
$$
and observe they are not met since $\frac{\partial u}{\partial a} \neq \frac{\partial v}{\partial b}$.

This means that the Complex Conjugate function is **not differentiable**.

If you recall the **geometric explanation** from earlier in this note, you might already understand the geometric reason for this.

The reason is that $f$ is a **reflection** of $z$ in the real-axis, meaning that it reverses the direction of the **phase** (or angle) of $z$, and so applying it after a rotation and scaling (multiplying by an imaginary number) gives a different result to applying it before a rotation and scaling.
### Example 3
Now consider the function $f:\mathbb C \to\mathbb C$ given by $f(z)=z^{-1}=\frac1z$. How could we differentiate this function? Well first we need to check if this satisfies the Cauchy-Riemann conditions. If it doesn't we **can't** differentiate it at all.

Here we can start by rewriting
$$
\frac1z = \frac{\bar z}{|z|^2} = \frac{a-ib}{a^2+b^2}
$$
This allows us to define
$$
f(a, b) = u(a, b) + i \cdot v(a, b)
$$
where 
$$
u(a,b) = \frac{a}{a^2+b^2},\; v(a, b) = \frac{-b}{a^2+b^2}
$$

We have to use the quotient rule to find our partial derivatives, making the process a little more complicated.
$$
\begin{split}
\frac{\partial u}{\partial a} 
& = \frac{1(a^2+b^2)-a(2a)}{(a^2+b^2)(a^2+b^2)} \\
& = \frac{b^2-a^2}{a^4+2a^2b^2+b^4} \\
\\
\frac{\partial u}{\partial b} 
& = \frac{0(a^2+b^2)-a(2b)}{(a^2+b^2)(a^2+b^2)} \\
& = \frac{-2ab}{a^4+2a^2b^2+b^4}
\\\\
\frac{\partial v}{\partial a} 
& = \frac{0(a^2+b^2)-(-b)(2a)}{(a^2+b^2)(a^2+b^2)} \\
& = \frac{2ab}{a^4+2a^2b^2+b^4} \\
\\
\frac{\partial v}{\partial b} 
& = \frac{-1(a^2+b^2)-(-b)(2b)}{(a^2+b^2)(a^2+b^2)} \\
& = \frac{b^2-a^2}{a^4+2a^2b^2+b^4} \\ 
\end{split}
$$

We can see from this 
$$
\begin{split}
\frac{\partial u}{\partial a} & = \frac{\partial v}{\partial b} \\
\frac{b^2-a^2}{a^4+2a^2b^2+b^4} & = \frac{b^2-a^2}{a^4+2a^2b^2+b^4} \\
\\\\
\frac{\partial u}{\partial b} & = -\frac{\partial v}{\partial a} \\
\frac{-2ab}{a^4+2a^2b^2+b^4} & = -(\frac{2ab}{a^4+2a^2b^2+b^4})
\end{split}
$$

Meaning that the **Cauchy-Riemann** conditions are met. We can now differentiate it using $f(z)=z^{-1}$ and the power rule.
$$
f'(z) = -z^{-2} = -\frac1{z^2}
$$
And we can get our full expression for this by substituting in $z=a+ib$
$$
\begin{split}
f'(a+ib) 
& = -\frac{1}{(a+ib)^2} \\
& = -\frac{1}{a^2+2iab+i^2b^2} \\
& = -\frac{1}{a^2-b^2+i(2ab)} \\
& = -\frac{(a^2-b^2)-i(2ab)}{(a^2-b^2)^2+(2ab)^2} \\
& = -\frac{(a^2-b^2)-i(2ab)}{a^4-2a^2b^2+b^4+4a^2b^2} \\
& = -\frac{(a^2-b^2)-i(2ab)}{a^4+2a^2b^2+b^4} \\
& = -\frac{(a^2-b^2)-i(2ab)}{(a^2+b^2)^2}
\end{split}
$$
