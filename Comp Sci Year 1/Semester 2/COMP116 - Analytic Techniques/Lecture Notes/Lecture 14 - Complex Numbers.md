## Origins of Complex Numbers
The idea of **complex numbers** initially came from a problem we saw earlier, **roots of polynomials**.

The claim was made that "All polynomials of degree $k$ have $k$ roots". 

This claim had a few problems. One was polynomials of the form $p(x)^n$. 

We know that any polynomial $p(x)$ of degree $k$ with $k$ roots can be written as 
$$
p(x)=\prod_{i=1}^k(x-r_i)
$$
where $r_i$ is the $i$th root of $p(x)$, raising $p(x)$ to the power of $n$ means that
$$
p(x)^n=\prod_{i=1}^k(x-r_i)^n
$$
and therefore $p(x)^n$ does not have any more distinct roots than $p(x)$ despite having a degree of $nk$ instead of $k$.

The way around this claim is **multiplicity**, which was discussed as a sidenote in [[Lecture 3 - Polynomials]] when talking about roots of polynomials. What multiplicity means is that if $r$ is a root of $p(x)$ then $r$ is also $n$ **coinciding roots** of $p(x)^n$.

Understanding it like this makes the claim closer to true as now $x^2$ (or similar polynomials) no longer have 1 root of 0, they have 2 coinciding roots at 0. 

But what about $x^2+1$? This has no real roots since if we plug this into our quadratic formula we see:
$$
\begin{split}
x & = \frac{-0\pm\sqrt{0^2-4(1)(1)}}{2(1)} \\
x & = \frac{\pm\sqrt{-4}}{2} \\
\end{split}
$$
Since $-4$ is negative it means that there is no real solution to what $\sqrt{-4}$ is. Originally it just just said that $\sqrt{-4}$ is undefined and therefore $x^2+1$ has no roots.

This was the case until someone came along and said "Imagine that there exists a number $i$ which is equal to $\sqrt{-1}$" this allowed the roots of $x^2+1$ to be written like so:
$$
\begin{split}
x 
& = \pm\frac{\sqrt{-4}}{2} \\
& = \pm\frac{\sqrt{-1\cdot4}}{2} \\
& = \pm\frac{2i}{2} \\
& = \pm i
\end{split}
$$
This gave $x^2+1$ two roots ($i$ and $-i$), and so if we operate like this then the claim finally becomes true.

In fact, the introduction of $i$ allows us to write the root of any negative number as the product of some real number and $i$. 

Originally, after these numbers were conceptualised, [René Descartes](https://www.google.com/search?q=Ren%C3%A9+Descartes&rlz=1C1UEAD_en-GBGB1162GB1162&oq=Who+came+up+with+ima&gs_lcrp=EgZjaHJvbWUqBwgAEAAYgAQyBwgAEAAYgAQyBggBEEUYOTILCAIQABgKGAsYgAQyCwgDEAAYChgLGIAEMggIBBAAGBYYHjIICAUQABgWGB4yCAgGEAAYFhgeMggIBxAAGBYYHjIICAgQABgWGB4yCAgJEAAYFhge0gEINDI3MGowajeoAgCwAgA&sourceid=chrome&ie=UTF-8&ved=2ahUKEwjM89mMoouTAxVOaEEAHWGXOFQQgK4QegYIAQgBEAE) coined the term **imaginary numbers** (which was originally meant as an insult) since there is no real word 1 dimensional number line equivalent. We now use **imaginary number** as a way to describe any number of the form $ix$ where $x\in\mathbb R$.

>The term **imaginary numbers** is actually a bit of a misnomer. Operations on them have observable consequences for the whole field of mathematics and therefore they are "real" in the same sense that anything else you can observe is real.
>
>We still use **imaginary** as a label to differentiate them from **real** numbers, with which we are very familiar.

However some polynomials, don't have roots that can be expressed neatly as just an imaginary number. If, for instance, we solve $x^2+4x+5$ we can see
$$
\begin{split}
x 
& = \frac{-4\pm\sqrt{4^2-4(1)(5)}}{2(1)} \\
& = \frac{-4\pm\sqrt{-4}}{2} \\
& = \frac{-4\pm2i}{2} \\
& = -2\pm i
\end{split}
$$
and so $x^2+4x+5$ has 2 roots $-2+i$ and $-2-i$. 

Both of these are still just 1 number which is the sum of a **real number** (2) and an imaginary number ($\pm i$). We call numbers of this form **complex numbers**.

>Small sidenote: $xi$ and $ix$ are obviously equivalent, but generally you will see people write $ix$, as placing the $i$ first makes it more clear that the number is imaginary. 
>
>When $x$ is a defined constant, i.e. $x=4$, we write $4i$ instead of $i4$ to keep this consistent with other algebraic expressions.
## Complex Numbers Overview
As said above, a complex number $z$ is any number of the form
$$
z=a+ib
$$
Where $i=\sqrt{-1}$ and $a,b\in\mathbb R$.

We call $a$ the **Real Part** of $z$ and we denote it by $Re(z)$, and we call $b$ the **Imaginary Part** of $z$ which we denote by $Im(z)$. We also denote the set of complex numbers with $\mathbb C$.

Notice that $a + 0i\in \mathbb{C}$ and $0+ib\in\mathbb C$ so complex numbers are actually a **superset** of both imaginary and real numbers.

>Notice that $Re(z)$ is actually a function $Re(z):\mathbb C \to \mathbb R$. Likewise $Im(z)$ is also a function $Im(z):\mathbb C \to \mathbb R$.

The pairs of Real and Imaginary numbers $\{(Re(z), Im(z))\; |\;z\in\mathbb C\}$ form the **complex plane**, as opposed to the **cartesian plane** formed by $\{(x,y)\;|\;x,y\in\mathbb R\}$. 

You can understand the **complex plane** as the cartesian plane where the $x$-axis is replaced with the **real-axis** and the $y$-axis is replaced with **imaginary-axis**.

When we see depictions of complex numbers as vectors on a grid we call this grid an **Argand diagram**.
## Operations on Complex Numbers
There are a number of simple (and more complicated) operations which we can perform on complex numbers. We will go through them here.
### Addition
To perform addition on complex numbers we just sum the real and imaginary parts respectively.

If $u,v\in\mathbb C$ and $z=u+v$ then:
- $Re(z)= Re(u)+R(v)$
- $Im(z) = Im(u) + Im(v)$

For example, let $u=1+2i,\; v=3+4i$, this means that
$$
\begin{split}
u+v 
& = (1 + 3) + (2+4)i \\
& = 4 + 6i
\end{split}
$$
### Complex Conjugate
The complex conjugate of a complex number $z$ is the same as $z$ but with the negation of it's imaginary part. We denote the complex conjugate as $\bar z$.

If $z\in\mathbb C$ then:
- $Re(\bar z)=Re(z)$
- $Im(\bar z)=-Im(z)$

Notice that $\bar{\bar z}=z$.

>You may notice that the pairs of complex roots for the quadratic polynomials we did above we pairs of **complex conjugates**. 
>
>This is always the case for complex roots of polynomials. For polynomials of higher degrees, they may have both real and complex roots, and may have multiple pairs of complex roots.

For example, let $z=5-4i$, this means that
$$
\begin{split}
\bar z 
& = 5 - (-4)i \\
& = 5 + 4i
\end{split}
$$
### Modulus
The modulus of a complex number $z$ is the same as the **magnitude** of the vector $(Re(z),Im(z))$ in the standard Euclidean norm.

If $z\in\mathbb C$ then $|z|=\sqrt{Re(z)^2+Im(z)^2}$

For example, let $z=3+4i$, this means that
$$
\begin{split}
|z|
& = \sqrt{3^2+4^2}\\
& = \sqrt{9+16} \\
& = \sqrt{25} \\
& = 5
\end{split}
$$
### Multiplication by a Scalar
Multiplication of a complex number by a scalar $s\in\mathbb R$ is achieved by multiplying both the real and imaginary part of the complex number by $s$.

If $z\in\mathbb C,\;s\in\mathbb R$ then:
- $Re(s\cdot z) = s\cdot Re(z)$
- $Im(s\cdot z)=s\cdot Im(z)$

For example, let $z=2+i$ and $s=5$ this means that
$$
\begin{split}
s\cdot z 
& = 5\cdot 2 + 5 \cdot i \\
& = 10 + 5i
\end{split}
$$
### Complex Multiplication
Multiplication of two complex numbers is achieved the same as multiplication of two brackets each with two terms. This is because of the distributive nature of multiplication over addition.

If $u,v\in\mathbb C$, $u=a+ib,\; v= c+id$ and $z=u\cdot v$ then
$$
\begin{split}
z 
& = (a+ib)(c+id) \\
& = ac + ibc + iad + i^2bd \\
& = ac - bd + i(bc + ad)
\end{split}
$$
So:
- $Re(z)=Re(u)\cdot Re(v) - Im(u)\cdot Im(v)$
- $Im(z)=Re(u)\cdot Im(v) + Re(u)\cdot Im(v)$

Personally I don't think it's necessary to remember the formulas above, you can just apply the standard principles of expanding brackets.

For example, let $u=3+4i,\; v=1-2i$, this means that
$$
\begin{split}
u\cdot v 
& = (3+4i)(1-2i) \\
& = 3 + 4i - 6i -8i^2 \\
& = 11 - 2i
\end{split}
$$
### Complex Division
Given $u,v\in\mathbb C$ how could we compute $z=\frac uv$?

Well since we know how to multiply two complex numbers, all we need to do is find a definition for $w=\frac1v$ and then we can compute $z$ as $u\cdot w$.

For the simplest forms of fractions, we only want **rational** numbers in the denominators of our fractions, this is why we write $\frac{\sqrt2}{2}$ instead of $\frac1{\sqrt2}$ (called **rationalising** the denominator). If this is something you're not familiar with you can read about it [here](https://www.mathsisfun.com/algebra/rationalize-denominator.html).

Similarly, as $\mathbb Q\subset \mathbb R$, we can't have any **imaginary** or **complex** numbers in our denominator as these are **not** rational numbers. So we apply a similar technique to fractions involving complex numbers. We do this to both **realise** (make real) and **rationalise** (make rational) the denominator.

Lets see how we can compute $\frac 1v$.

We know that 
$$\forall x,\; \frac xx=1$$
and therefore that 
$$\frac{\bar v}{\bar v} = 1$$

We also know that 
$$
\forall x,\; 1 \cdot x = x
$$

and therefore that
$$
\frac1v\cdot\frac{\bar v}{\bar v} = \frac1v
$$

Let's try and compute this for a general $v=a+ib$
$$
\begin{split}
\frac 1v
& = \frac1{a+ib} \\
& = \frac1{a+ib}\cdot \frac{a-ib}{a-ib} \\
& = \frac{a-ib}{(a+ib)(a-ib)} \\
& = \frac{a-bi}{a^2+iba-iba-i^2b^2} \\
& = \frac{a-bi}{a^2+b^2}
\end{split}
$$
We can notice that 
$$
\frac{a-bi}{a^2+b^2}=\frac{\bar v}{|v|^2}
$$
and so we know that 
$$
\frac1v = \frac{\bar v}{|v|^2}
$$
We can now find $z=\frac uv$ by multiplication of $\frac1v=\frac{a-ib}{a^2+b^2}$ and $u=c+id$ like so
$$
\begin{split}
z 
& = \frac uv \\
& = \frac{u\bar v}{|v|^2} \\
& = \frac{(a-ib)(c+id)}{a^2+b^2} \\
& = \frac{ac-ibc+iad-i^2bd}{a^2+b^2} \\
& = \frac{ac+bd+i(ad-bc)}{a^2+b^2} \\
& = \frac{ac+bd}{a^2+b^2} + i\frac{ad-bc}{a^2+b^2}
\end{split}
$$

So if $u,v\in\mathbb C$ and $z=\frac uv$ then:
$$
Re(z)=\frac{Re(v)\cdot Re(u)+Im(v)\cdot Im(u)}{|v|^2}
$$
and 
$$
Im(z)=\frac{Re(u)\cdot Im(v) + Re(u)\cdot Im(v)}{|v|^2}
$$




