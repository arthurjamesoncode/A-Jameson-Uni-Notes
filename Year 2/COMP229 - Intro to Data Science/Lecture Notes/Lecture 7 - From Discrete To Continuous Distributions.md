## Poisson Distribution
The **Poisson** distribution is the number $X$ of events that occur independently in a fixed interval of time, when the expected number of occurrences is $\lambda > 0$.

It's pmf is
$$
f(k)=P(X=k)=\frac{\lambda^ke^{-\lambda}}{k!}
$$
and it's expectation is
$$
E(X)=\lambda
$$

You can see an example pmf and cdf below:
![[possion_pmf_cdf.png]]

Can be derived from the binomial distribution.

The **Poisson limit theorem**, also called the law of rare events, states that when $n\to\infty$ and $p\to0$ with $np=\lambda$ the binomial distribution $B(n,p)$ tends to the Poisson distribution.

![[binomial_to_poisson.png]]

This essentially means we can use the Poisson distribution to model systems that have large numbers (n is big) of rare events (p is small):
- Number of phone calls in a minute
- Number of laser photons hitting a detector in a time interval

As a rule of thumb, this works with
$$
n\geq1000 \text{ and } np\leq10
$$

If we give the average rate $r$ instead of the average number of events then we can use $\lambda = rt$ and
$$
P(X=k\; \text{in an interval of length t})=\frac{(rt)^ke^{-rt}}{k!}
$$
## Uniform Continuous Variables
A random variable $X$ is **uniform continuous** on an interval $[a, b]$ if it's cumulative distribution function is
$$
F_X(v)=
\cases{
\begin{split}
0 \;\;\; & \text{for } v\leq a \\
\frac{v-a}{b-a} \;\;\; & \text{for } v\in[a, b] \\
1 \;\;\; & \text{for } v\geq b \\
\end{split}
}
$$
You can see an example **cdf** below
![[uniform_cont_cdf.png]]

This is an extension of the discrete uniform distribution, but if $n$ tended to $\infty$, and instead of specific values we were given a range of values.

Interestingly the chance $X$ being any specific value in the range $[a,b]$ is 0, despite it being possible for $X$ to be that value. This is because there are infinitely many possible values for X and therefore the chance of 1 specific one is so small it must be functionally equivalent to 0. 

Take the problem below

"Let X be the uniform continuous random variable on the interval $[0, 2] ⊂ \mathbb R$. 

Find the probabilities $P(X < 0), P(X < 2), P(X < 1.35)$ and $P(X ≤ 0)$."

We can do this using the above formula:
- $P(X<0)=0$ 
- $P(X<2) = 1$
- $P(X < 1.35)$ is $\frac{1.35-0}{2-0}=0.675$
- $P(X\leq 0)=0$
## Density Functions
Density functions rely slightly on an understanding on **calculus** which was covered in [[Lecture 7 - Intro to Calculus|lectures 7]]-[[Lecture 12 - Integration and Area|12]] in the COMP116 module. I am not going to go back over it here.

We saw the notion of a **probability mass function** for **discrete variables**. These gave the probability of the variable taking any specific value. However given that the probability of a continuous variable taking any specific value is 0, this same idea doesn't work.

Now we use something called a **probability density function**. We get this function by taking the derivative of the cumulative distribution function of a continuous variable.

Formally, if a continuous random variable $X$ has a cumulative distribution function $F_x(v)$ then it's probability density function $f(v)$ is given by
$$
f(v)=\frac{dF_x(v)}{dv}=F'_x(v)
$$

Using this, we can get $P(X<v)$ by integrating $f(v)$
$$
P(X<v)=F_x(v)=\int_{-\infty}^vf(x)dx
$$
Similarly we can get $P(v_1<X<v_2)$ 
$$
P(v_1<X<v_2)=\int_{v_1}^{v_2}f(x)dx
$$

Continuous random variables are often defined by their density function $f(x)\geq0$, which is always
$$
f(x)=
\cases{
\begin{split}
\frac1{b-a} \;\;\; & \text{for } x\in[a, b] \\
0 \;\;\; & \text{for } x\notin[a, b] \\
\end{split}
}
$$
Which you can see pictured below
![[probability_density_function.png]]

The green area is $P(X < v)$, while the yellow area is $P(X>v)$

The density function is different to the mass function because the line does not represent the probability that $X$ takes the corresponding value on the x-axis (since that probability is always 0). Instead it represents probability that $X$ is clustered around that point.

Because of this we have to take areas, and we cannot just take the probability of single values.
## Example Uniform Variable
Problem "For a uniform variable $X$ on $[1, 5]$, find $P(X ∈ [2, 4))$ in two ways: from the CDF and from the PDF."

From the CDF we can do:
$$
\begin{split}
P(X<4) &= \frac{4-1}{5-1}= \frac34 \\
P(X<2) &= \frac{2-1}{5-1}= \frac14 \\
\\
\therefore P(2\leq X < 4)&= \frac34-\frac14=\frac12
\end{split}
$$

From the PDF we can do the following. 

We know that all the values in the range $[2,4)$ have density $\frac1{5-1}=\frac14$. This lets us do
$$
P(2\leq X < 4)=\frac14\cdot(4-2)=\frac12
$$
## Closing Problem
"A call centre receives calls at a mean rate of 2 calls per minute. Assuming that calls are independent of each other, find the probability of having to deal with exactly 5 calls in 1 minute."

We can use the Poisson distribution for this.

We know that 
$$
P(X=k\; \text{in an interval of length t})=\frac{(rt)^ke^{-rt}}{k!}
$$
and that $r=2$ and that $t=1$.

Therfore
$$
P(X=5 \text{ in an interval of 1 minute})=\frac{2^5e^{-2}}{5!}\approx0.036
$$

