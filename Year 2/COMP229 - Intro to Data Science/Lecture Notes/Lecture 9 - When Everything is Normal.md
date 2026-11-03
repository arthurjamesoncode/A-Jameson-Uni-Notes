## The $\sigma-2\sigma-3\sigma$ Rule & $Z$-Scores
The $\sigma-2\sigma-3\sigma$ rule states that in a normal distribution:
- About 68% of observations are in the range $[\mu-\sigma, \mu+\sigma]$
- About 95% of observations are in the range $[\mu-2\sigma, \mu+2\sigma]$
- About 99.7% of observations are in the range $[\mu-3\sigma, \mu+3\sigma]$

![[1-2-3 rule.png]]

We can standardise any normal variable $X$~$N(\mu,\sigma^2)$ by performing
$$
Z = \frac{X-\mu}\sigma
$$
meaning that $Z$~$N(0,1)$.

This gives us
$$
P(X<v)=P(\frac{X-\mu}{\sigma}<\frac{v-\mu}{\sigma})=P(Z<\frac{v-\mu}{\sigma})
$$

Now the $\sigma-2\sigma-3\sigma$ rule becomes the $1 - 2 - 3$ rule, which is even easier to apply.

For example take the following problem: "Let exam marks have a normal distribution with $µ = 60$ and $σ = 10$. 
1) What proportion of the class has failed the exam? 
2) Find the proportion of 70+ marks."

Since 40 is the fail rate for an exam, and $60 - 40=30=2\sigma$ we know that half of $1-0.95=0.05$ failed the exam. So 2.5% of students failed.

Since $70-60=10=\sigma$, we know that half of $1-0.68=0.32$ got a mark above or equal to 70 marks. Therefore 16% of students got 70 or better.

We take half since the 95%, or 68% refers to the middle of the distribution, therefore what is not in the range incudes both tails. Since we are only interested in the lower tail for the first question, and the upper tail for the second question, we half it.

When standardising for Z score, this is usually done using a table of values.
1) Z score is $\frac{40-\mu}{10}=-2$
2) Z score is $\frac{70-\mu}{10}=1$

The table would have a corresponding value for these scores, which would give you
1) $P(Z<-2)$
2) $P(Z< 1)$

In the case of the second, we actually want $P(Z>1)$ so you would do $1-P(Z<1)$.

This is just another method to do the same thing we showed above.
## The Central Limit Theorem
Suppose $X_1,...,X_n$ are **independent, identically, distributed** (i.i.d.) variables with expected value $\mu$ and variance $\sigma^2$.

The **Law of Large Numbers** states that
$$
\lim_{n\to+\infty}\bar X_n = \lim_{n\to+\infty}\frac1n\sum^n_{i=1}X_i=\mu
$$

The **Central Limit Theorem** states that
$$
\lim_{n\to+\infty}\frac{\bar X-\mu}{\sigma/\sqrt n} = N(0,1)
$$
Essentially, to put this informally, at the limit any average is normal.

This is essentially what proves that binomial distributions approximate a normal distribution. A result of this is we often assume random variables we can't control to be normal.
## Statistical Inference
Probability theory studies problems when a probability distribution is known, or at least assumed to be. For example we work with a normal distribution with a given $\mu$ and $\sigma$.

In practice we have sample data and wish to make conclusions about a population. For example we want to try and give estimates for "true" parameters such as $\mu$ and $\sigma$ of a normally distributed variable in the population.

Drawing conclusions about this is called **statistical inference**.
### Point Estimates & Interval Estimates
A point estimate is a single value estimated from a sample. The sample mean 
$$
\bar x = \frac1n\sum^n_{i=1}x_i
$$
is a point estimate of the mean $\mu$ of a normal density.

An **interval estimate** specifies an interval containing the estimated parameter. It is essentially a point estimate but taking into account a given margin of error.

So instead of saying $\mu=\bar x$ we would say
$$
\mu \in [\bar x - \text{margin of error}, \bar x + \text{ margin of error }]
$$
This would come with a specific confidence level attached to it, which essentially states how sure we can be that $\mu$ is in this interval.
### Calculating Interval Estimates
In order to infer something from a sample we need a set of conditions or assumptions. We call these conditions a **statistical model**. 

Our assumptions are:
- We have a simple random sample (SRS) from the larger population
- The variable we are interested is $N(\mu, \sigma^2)$ with a known standard deviation $\sigma$
- We know the standard deviation $\sigma$ but not the mean $\mu$

Take the following problem

"Imagine we know only 9 exam marks
$$
\{x_1,...,x_9\} = \{60,70,80,50,90,40,30,45,75\}
$$
which are all measurements of 
$$
X_1,...,X_9 \sim N(\mu, \sigma)
$$
Given $\sigma=15$, estimate an interval for the mean $\mu$ with confidence 95%."

To do this first we need our sample mean $\bar x$
$$
\bar x= \frac{60+70+80+50+90+40+30+45+75}9=60
$$
Now we can consider the mean as an expression of a random variable $\bar X$
$$
\bar X=\frac1n\sum^n_{i=1}X_i
$$

Following from the law of large numbers and the central limit theorem, if
$$
X\sim N(\mu, \sigma^2)
$$
then 
$$
\bar X\sim N(\mu,\frac{\sigma^2}n)
$$
So the standard deviation of $\bar X$ from our sample is 
$$
\sigma_{\bar X}=\sqrt{\frac{\sigma^2}{n}}=\sqrt{\frac{15^2}{9}}=\frac{15}3=5
$$

Note that is $X_i\sim N(\mu,\sigma^2)$ but only the sample deviation $s$ is deliverable (meaning known/available/obtainable from the data), then it's better to use the different model: **t-statistic**.
$$
t=\frac{\bar X - \mu}{\frac s{\sqrt n}}\sim t_{n-1}
$$
which follows the students distribution with $n-1$ degrees of freedom.

Now that we have our standard deviation for the mean and our sample mean we can estimate the mean with 95% confidence by referring to the $1\sigma-2\sigma-3\sigma$ rule which states that 95% of observations fall within $2\sigma$ of the mean.

Giving us our final interval of
$$
[60 - 2\sigma, 60 + 2\sigma] = [60-10,60+10]=[50,70] 
$$

And so we can say with a 95% confidence interval that 
$$
\mu \in [50, 70]
$$
### Finding Confidence
We can generalise finding the confidence interval to the following.

Let $z^*$ be the critical value satisfying $P(|Z|<z^*)=\alpha$ for a given confidence level $\alpha$ and standard normal variable $Z\sim N(0,1)$.

If $n$ samples are drawn from $X\sim N(\mu, \sigma^2)$, then $\mu$ has the confidence interval $\bar x\pm z^*\frac{\sigma}{\sqrt{n}}$.

Were this procedure to be repeated many times, the confidence interval will the contain the true value of $\mu$ with probability $\alpha$. I.e. The chance that $\mu$ is in the confidence level is $\alpha$.

For a higher confidence level, the confidence interval will be wider. This makes sense as to be more confident a value is in a given region, you can make the region wider.

If you have a narrower confidence interval given the same confidence level, that means you have more **certainty** about the result.

To get the critical values $z^*$ we can look at the **standard normal table** or **Z table** (this was referenced earlier).

In the previous problem we approximated 95% with a $z^*$ of 2. The better value is $z^*=1.96$

The most commonly used confidence levels and their $z^*$ values are

| Confidence Level | Critical Value $z^*$ |
| ---------------- | -------------------- |
| 90%              | $1.645\approx 1.7$   |
| 95%              | $1.96\approx 2$      |
| 99%              | $2.546\approx 2.6$   |
### Word on Assumptions
There is a famous quote saying:
	"All models are wrong, but some are useful" - George E.P.Box

This is built of the idea that assumptions are never exactly true. 

The question therefore is not:
- "Is this model correct"
It is
- "Is this model good enough"

It is always important to check whether the assumptions being made make sense or not for your model.
## Closing Problem
"The sample
$$
\{60, 70, 65, 80, 85, 35, 55, 50, 100, 20, 90, 60, 40, 30, 45, 75\}
$$
is from a normal distribution with standard deviation $\sigma = 20$. Estimate the mean with confidence 95%, 99% and 90%."

To do this first we find our sample mean
$$
\begin{split}
\bar x 
&= \frac{60+70+ 65+ 80+ 85+ 35+ 55+ 50+ 100+ 20+ 90+ 60+ 40+ 30+ 45+ 75}{16} \\
&= \frac{960}{16} = 60
\end{split}
$$

Now we can find the standard deviation of our mean using the CTL and the law of large numbers
$$
\sigma_{\bar X} = \sqrt{\frac{20^2}{16}} = \frac{20}4=5
$$

We know from our confidence level table that we want $z^*$ values of:
- 1.7 for 90%
- 2 for 95%
- 2.6 for 99%

And so we can calculate our intervals as:
- $[60-8.5, 60+8.5]=[51.5,68.5]$ for 90%
- $[60-10, 60+10]=[50,70]$ for 95%
- $[60-13,60+13]=[47,73]$ for 99%

