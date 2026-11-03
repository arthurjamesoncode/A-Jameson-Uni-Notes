## Exponential Distribution
The real number $e\approx 2.718$ occurs in many mathematical contexts. 

Specifically, $e$ is derived from calculus. It is the unique positive real number such that
$$
\frac{d}{dx}e^x=e^x
$$
for all $x\in\mathbb R$.

As a result we call 
$$
f(x)=e^x
$$
the exponential function.

The **exponential distribution** describes the time between event in a **Poisson process** where events occur continuously and independently at a constant average rate $\lambda$.

The **pdf** is:
$$
f(x, \lambda)=\cases{
\begin{split}
\lambda e^{-\lambda x},\;\; & x \geq 0 \\
0, \;\; & x<0
\end{split}
}
$$
and the **cdf** is:
$$
F(x, \lambda)=\cases{
\begin{split}
1 - e^{-\lambda x},\;\; & x \geq 0 \\
0, \;\; & x<0
\end{split}
}
$$

You can see both of these pictured below (pdf then cdf):
![[exponential_pdf_cdf.png]]
## Normal Distribution
A normal variable $X = N(\mu,\sigma^2)$ has the density function
$$
\phi_{\mu,\sigma^2}(x)=\frac1{\sqrt{2\pi}\sigma}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$
where $\mu$ is the mean (also the median and mode), and $\sigma$ is the standard deviation.

The standard normal variable is $X=N(0,1)$, meaning it is centered on 0 and has a standard deviation of 1.

The two key properties of this distribution are that:
$$
e^{-\frac{(x-\mu)^2}{2\sigma^2}} \to 0, \text{ as } x \to \pm\infty
$$
meaning that it converges, as well as the factor
$$
\frac1{\sqrt{2\pi}\sigma}
$$
ensures that 
$$
\int^{+\infty}_{-\infty}\phi_{\mu,\sigma}(x)dx=1
$$

>Daniel tells us not to worry too much about the formula for the normal distribution.

You can see the pdf and cdf of this distribution below
![[normal_pdf_cdf.png]]

Note that, on the pdf, changing $\mu$ moves the center of the distribution, while changing $\sigma$ stretches or squashes the distribution.

These properties are much easier to see on the **pdf**, which forms a bell curve, as opposed to the cdf. This is why generally normal distributions are shown using their pdf.

If you recall the binomial distribution, you may recall the graphs looking similar. This is because a binomial distribution (which is discrete) approximates a normal distribution on infinitely many trials.
## Students Distribution
The students distribution $t_v$ is a generalisation of the standard normal distribution. It has heavier tails which are controlled by the parameter $v$ (called the number of degrees of freedom).

As $v\to\infty$, it becomes $N(0,1)$ and it has $E(X)=0$ for all $v>1$

![[students_pdf_cdf.png]]

>Daniel doesn't even show us the formula for this function, and tells us not to worry about it because it is too complicated.

There is a note here that knowing the connections between distributions is useful for choosing the correct tools for each particular problem. Along with a link to [connections between distributions](https://en.wikipedia.org/wiki/Relationships_among_probability_distributions). 

This obviously makes intuitive sense, and is probably useful to learn but I am unsure on how much of this we will be tested on. Probably only the stuff mentioned in lectures, which I have documented.
## Continuous Variables on Higher Dimensions
For any domain $D\subset R^n$ with a volume of $vol(D)$ the uniform continuous random variable $X$ on $D$ has the density:
$$
f_x(p)=\cases{
\begin{split}
\frac{1}{vol(D)},\;\; & p\in D, \\
0, \;\; & p\in\mathbb R^n-D
\end{split}
}
$$

Now for any $A\in \mathbb R^n$ we have
$$
P(X\in A)=\frac{vol(A\cap D)}{vol(D)}
$$
If you go back to the one dimensional case where $D$ was a line $[a,b]$ we can see that $vol(D)$ would be $a-b$ and that the above is consistent with our formula for the density of uniform continuous variable covered [[Lecture 7 - From Discrete To Continuous Distributions|last lecture]]. This is just a generalisation of that formula.
## Curse Of Dimensionality
There are some counter intuitive properties of analogues of objects from $\mathbb R^2$ and $\mathbb R^3$.

We will look at 2 problems that illustrate this.
### Problem 1
Consider the following problem: "Uniformly choose a random point q in the cube $[−1, 1]^n$ . What’s the probability that $q$ has a distance more than 1 from the origin $\vec0 ∈ \mathbb R^n$?"

In this problem $[-1,1]^n$ means a *cube* centered on the origin, which sides/faces that extend out by 1 in all directions.

For $n=1$, this cube is the line $[-1,1]$, in this case all points are within 1 from the origin and therefore the property is 0.

For $n=2$, this cube is a square that is larger than the unit circle. The area of this square is 
$$
(1-(-1))^2 = 4
$$
while the area of the unit circle (the points within 1 of the origin) is 
$$
\pi\cdot 1^2 = \pi
$$
and so the probability that a point in this cube is more than 1 away from the origin is
$$
\frac{4-\pi}4 \approx 0.215
$$

For $n=3$ the cube is a cube with side length $2$, so has a volume of
$$
2^3
$$
which is larger than the unit sphere which has a volume of 
$$
\frac43\pi
$$
So the probability that a point lies inside the cube but outside of this sphere is:
$$
\frac{\frac43\pi}8=\frac16\pi\approx0.524
$$

So we can see the chance of missing the ball is going up and up from this.

If we want to generalise this to $n$ dimensions we need the formula for an $n$-dimensional ball of radius 1, which is:
$$
V_n = \frac{\pi^{n/2}}{\Gamma(\frac n2+1)}
$$
where
$$
\Gamma(m) = (m-1)! \text{ and } \Gamma(m+\frac12)=(m-\frac12)(m-\frac32)\cdots\frac12\sqrt\pi
$$

The gamma function
$$\Gamma(m)$$
is essentially the factorial function but generalised to be continuous. 

>Daniel doesn't go in detail about this, so I doubt we will need to know about it but [here](https://en.wikipedia.org/wiki/Gamma_function) is the Wikipedia page.

Now the function
$$
\frac{V_n}{2^n}
$$
quickly converges to 0. Meaning that as the dimensions increase the probability of missing the ball tends to 1.
### Problem 2
Consider the following problem "What is the radius $r_n$ of the ball whose volume is 50% of the unit ball’s volume in $\mathbb R^n$?"

For $n=1$ the ball is a line and the volume is the length 1. So $r_1$ is simply 0.5.

For $n=2$ the ball is the unit circle and the volume is an area so $r_2$ satisfies
$$
\pi r^2_2 = \frac12\pi
$$
and therefore
$$
r_2 = \sqrt{\frac12}=\approx 0.7
$$

This actually generalises to
$$
r_n = \sqrt[n]{\frac12}
$$
which quickly converges to 1 as $n\to\infty$.

In a 3 dimensional sphere, about 50% of the volume is within the outer 21% layer. In a 10 dimensional sphere the outer 7% layer contains 50% of the volume.
### Conclusion
These problems show us something about higher dimensions. 

A uniform distribution in higher dimensions concentrate in unexpectedly narrow regions and does not "uniformly" cover the space as we expect.

This has implications for nearest neighbour machine learning algorithms, related search patterns and the overall information coverage of any real data.

In ML, a rule of thumb is that you need at least 5 training examples for each dimension (feature) in the representation. This means the amount of required data grows quickly with each new feature.

>They go over the formulas from these example problems in more detail in the slides but I am assuming they won't be evil enough to put this in the exam and therefore I am skipping that in favour of just noting the main point about uniform distributions in higher dimensional spaces spaces.
## Closing Problem
We know from the options that:
- B is a less strict version of A, and therefore if A is true B is also true but if B is true A is not necessarily true
- The same above applies except replace B with D and A with C
- This means that A and C cannot be correct, since only 1 can be correct
- Left with B and D we know that if the statement is true for x > 1 then it is also true for x > 2 meaning that if B is true D is also true, but this condition is not reversible.
- Again this contradicts the condition that only one is correct.

Therefore the answer is D, as this is the only condition that does not imply another condition.