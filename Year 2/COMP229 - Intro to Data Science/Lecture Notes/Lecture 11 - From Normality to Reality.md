## Non-Normal Distributions
Last lecture, we looked at normal distributions, and often we make the assumption that variables follow a normal distribution. 

This lecture is going to be spent looking at some alternative, continuous distributions that may be better models for our data. These distributions are not rare, and it worth remembering them as when choosing models for your data. 

In particular we will look at an example of a **ratio** and a **power law** distribution, which are very different to normal.
## Cauchy Distribution
A **Cauchy** random variable $X$ has the density function:
$$
f_{(m,\gamma)}(x)=\frac{1}{\pi\gamma}\Bigg[\frac{\gamma^2}{(x-m)^2+\gamma^2}\Bigg]
$$
Where $m$ is the location of the peak, and $\gamma$ specifies the half-width at half maximum.

You can see this pictured below:
![[cauchy_distribution.png]]

The standard Cauchy distribution has the probability density function
$$
f_{(0,1)}(x)=\frac{1}{\pi(1+x^2)}
$$
If the variables $X_i$ are **i.i.d.** with a standard Cauchy density then the average of these variables fit the standard Cauchy distribution, not a normal distribution.

At first glance this seems like a contradiction to the central limit theorem, but this is wrong. **CLT** requires a **finite variance**, which the Cauchy distribution doesn't have. 

The Cauchy distribution has no defined mean, and subsequently no defined variance (since variance is the average difference to the mean squared), but it does have a mode and a median which are both equal to $m$.

The reason for this undefined mean, and therefore variance, is that the integral of it's density function doesn't converge when taken from $-\infty\to+\infty$ . Put simply, the tails are too fat, and the area under the graph is infinite, meaning that the mean and variance are both infinite.

In plain English, the main difference between this and the normal distribution is that in a normal distribution you are very unlikely to see a result that is too far away from the mean/median, while in the Cauchy distribution, while you are still more likely to see a result near the median, the lack of convergence means you are much more likely to see a result a much larger or much smaller number than in the normal distribution.

For two independent standard normal variables $U\sim N(0,1)$ and $V\sim N(0,1)$, the ratio $U/V$ has the standard Cauchy distribution.

This sort of distribution isn't rare. Many rates have "fat tails", and should be approached with cautio when modelling. 

Sometimes the assumption of finite variance doesn't make sense, and in this case a **stable** distribution which is not normal, such as the Cauchy distribution, makes much more sense.

>A **stable** distribution is a distribution which produces the same distribution under a linear combination. For a reminder on linear combinations you can look to [[Lecture 5 - Vector Spaces]] from COMP116.
## Pareto Distribution
A **Pareto** random variable $X$ is defined by the survival/tail function
$$
F(x)=P(X>x)=
\begin{cases}
\big(\frac{(x_m)}x\big)^\alpha, & x \geq x_m \\
1, & x<x_m
\end{cases}
$$
Where $x_m>0$ is the minimum possible value of $X$ and $\alpha$ is a positive shape parameter, determining how much of the graph is concentrated at the front.

$x_m$ must be more than 0, because we cannot divide by 0 and therefore the tail function would be undefined.

The PDF is
$$
f_X(x)=
\begin{cases}
\frac{\alpha x^{\alpha}_m}{x^{\alpha+1}}, & x\geq x_m \\
0, & x < x_m
\end{cases}
$$

Which means that Pareto is a [**power-law**](https://en.wikipedia.org/wiki/Power_law) distribution. 

You can see some example pareto distributions below, all with $x_m=1$.
![[pareto_distribution.png]]

You may have heard of the **80-20** rule (called the pareto principle), which states that 80% of the outcomes are caused by 20% of the causes. 

This is a simplification of the pareto distribution, where the vast majority of outcomes are clustered around the start, before the rest drop off.

Similar laws hold for different parameters although with different numbers. There are a lot of areas where a small fraction of causes accounts for most of the effect in many areas (the slides list examples but I will not do that)

The 80-20 split is just a rule of thumb. The exact numbers vary and might only account for most outcomes not all.
## Limits of $p$-values
The slides now go through an example of how experiment design affects the resulting $p$-value.

Suppose we are assessing the probability $p$ of a certain outcome in experimental trials, and set 
$$
H_0 = \{p = 0.5\}
$$

Adam, a scientist, conducted 12 trials and obtained 3 successes and 9 failures. One of those successes was the 12th and last observation. Then Adam left the lab for good. 

Bill, a colleague in the same lab, continued Adam’s work, and did a significance test: 
$$
\begin{split}
P(3 \text{ or fewer successes in } 12 \text{ trials}) 
&= \left[ \binom{12}{9} + \binom{12}{10} + \binom{12}{11} + \binom{12}{12} \right] \left(\frac{1}{2}\right)^{12} \\
&= \frac{299}{4096} = 0.073
\end{split}
$$

This is not significant at the 5% level.

When another scientist comes in they say that Adam was performing the experiment until he had 3 successes. Given this they calculate another $p$-value
Here is the equation from slide 25 (labeled slide 12 in the deck) formatted using a $\begin{split}\end{split}$ environment for clean line-breaking:
$$
\begin{split} 
P(\text{conduct 12 or more experiments}) 
&= 1 - \Big[ \binom{10}{2}\left(\frac{1}{2}\right)^{11} + \binom{9}{2}\left(\frac{1}{2}\right)^{10} + \dots + \binom{2}{2}\left(\frac{1}{2}\right)^{3} \Big] \\ 
&= 0.0327 
\end{split}
$$
which is statistically significant at the 5% level.

The difference here isn't anything to do with the data, but just with the design of the experiment.

The lesson here is that $p$-values can be manipulated, and that studies that are conducted with a specific goal can often have their values nudged or "p-hacked".

Even when a result is not significant at a given significance level, if it's close studies may claim significance is some loose way.

![[bad_ps.png]]

$p$-values are not the end all be all of truth, and we should be careful how we interpret them.

There are 6 principles of NHST that should be considered:
1. $p$-values can indicate how incompatible the data are with a specified statistical model and the web of assumptions. 
2. $p$-values do not measure the probability that $H_0$ is true, or that the data were produced by random chance alone. 
3. Proper inference requires full reporting and transparency. 
4. A $p$-value, or statistical significance, does not measure the size of an effect or the importance of a result. 
5. By itself, a $p$-value does not provide a good measure of evidence regarding a model or $H_0$. 
6. Scientific conclusions and business or policy decisions should not be based only on whether a $p$-value passes a specific threshold.

If we did 20 independent tests (trying to reject a $H_0$ that was true) with a significance level of 5%, we would expect 1 false significant result.

This follows into a group of 6 actionable rules for NHST:
1. Check the assumptions
2. Avoid statements about the truth of $H_0$
3. Report the whole process, including underlying definitions and data exploration.
4. Avoid statements about the absence of an effect
5. Avoid statements about the effect size
6. Use multiple types of analysis and measures and **think**.

>Daniel actually says he somewhat disagrees with rule 6, and says that the methodology and measures should be defined before the experiment to avoid $p$-hacking, although I don't think that is completely counter to this rule.
>
>They also call data exploration **data torture** which is a nod to the fact that you can get data to tell you anything if you do enough to it.
>
