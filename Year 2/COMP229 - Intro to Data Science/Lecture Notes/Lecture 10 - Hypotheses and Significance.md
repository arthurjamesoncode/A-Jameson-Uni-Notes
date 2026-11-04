## Quiz on Confidence
The lecture starts with a quiz on confidence that I am going to do. It asks us to match the terms to the expression.

**Confidence level** - 95%
**Margin of error** - $\pm z^*\frac{\sigma}{\sqrt{n}}$
**Confidence interval** - $[\bar x - z^*\frac{\sigma}{\sqrt{n}}, \bar x+\pm z^*\frac{\sigma}{\sqrt{n}}]$

- Margin of error refers to how far away the mean could be from our sample mean. 
- Confidence level is the probability that the mean is in our confidence interval
- Confidence interval is the minimum and maximum value our mean could be for that given confidence level
## Hypothesis
Last lecture we used confidence intervals to estimate a parameter from our population. These sorts of inferences are usually used to test some claim about a population parameter using sample

A hypothesis is just an educated guess. Any scientific hypothesis should be **testable**. The *null hypothesis* $H_0$ is a claim that there is no effect, no difference, or no relationship in what's being measured.

$H_0$ should be thought of as a *nullifiable hypothesis* or a *default hypothesis*. We should be able to test $H_0$ and either reject/nullify it, or fail to. We do not *accept* $H_0$ we simply fail to reject it.

An alternative hypothesis $H_a$ claims a new effect, and is often stated before formulating $H_0$.

Take the following question: "We flip a coin and get one head followed by a row of tails. How many tails should we see before claiming that the coin is biased?"

In this example we have $H_a$ which is "The coin is biased towards tails", and we have $H_0$ which is, the coin is fair. $H_a$ is called **1-sided** in this case because it assumes a direction of difference.

How about the following problem: "A lecturer is studying the effect of the number of lectures on the average of exam marks. The average exam mark for the module is 60%.

A lecturer thinks that if module lectures happen 4 times a week (instead of 3 times), the average exam mark will be higher"

Here $H_0$ could say that the mean of the exam marks would stay at $\mu=60$

While $H_a$ could say that mean of the exam marks would not stay at 60, $\mu\neq60$. This would make $H_a$ **2-sided** since it does not assume a direction of difference. 

If we reformulated $H_a$ to be $\mu > 60$ then it would become a **1-sided** hypothesis.
## Hypothesis Testing
There are 6 stages of hypothesis testing. 

The process does contain some new terms that will be defined later but the steps are listed below:
1. Define the **null hypothesis** $H_0$, and the alternate hypothesis $H_a$.
2. Choose an appropriate test. In practice we usually choose the test from the list of known tests and check whether the assumptions required to perform this test hold.
3. State statistical assumptions about the sample. For example about the independence or distributions.
4. Set a **significance level** $\alpha$ $H_0$ will be rejected if the **$p$-value** is at most $\alpha$.
5. Calculate the **test statistic** and **$p$-value**.
6. Make a **decision** about the null hypothesis. This this based on the $p$-value and $\alpha$.

These steps reference some new concepts:
- **Significance Level**
- $p$-value
These are defined below.
### $p$-value
The **test statistic** measures how far the result of a given test diverges from the value expected under $H_0$. It is essentially $z$ statistics but for our test.

For example if we were testing to see if a coin was fair or biased and we flipped the coin 100 times, the test statistic would measure how far the number of heads/tails we got deviated from the expected value.

The $p$-value is
$$
P(\text{Test Statistic Or More Extreme}| H_0)
$$
or in plain English, it is the chance we would get our **test statistic**, or a more extreme result than that, given $H_0$ was true.

It is not the same as $P(H_0)$. That would be an example of the **base rate fallacy** covered in [[Lecture 4 - Conditional Probabilities & Bayes' Formula#Cancer Screening Example|lecture 4]].

Since the alternative hypothesis can be **1-sided** or **2-sided**, $p$-values can also be 1 or 2 sided.

For example, imagine we start a hypothesis test from the lecturer example above. We begin by:
1. Defining $H_0$ that $\mu=60$ and $H_a$ that $\mu\neq 60$ or $\mu > 60$ (we will do both 1 and 2 sided tests for illustration purposes. In practice one would be chosen)
2. Choosing a test - The 25 students exam results after changing to 4 lectures a week
3. State the assumptions:
	- Students exam results are identically distributed and independent (i.i.d.), and therefore by the CLT we assume the results to be normally distributed
	- The standard deviation of exam marks is 15

We will skip setting a **significance level** for now, and go straight on to calculating our $p$-value.

After the exam results the sample mean achieved is $69$. This seems to suggest an improvement under the new system, but we need to work to quantify the chance of this being true using $p$-values.

Our $p$-values are:
- 1-sided: $P(X\geq 69)$
- 2-sided: $P(|X-60|\geq 9)$

We now need to find our test statistic $\bar z$.

From the central limit theorem we can infer that
$$
\begin{split}
\bar z 
&= \frac{\bar x - \mu_0}{\frac{\sigma}{\sqrt n}} \\
&= \frac{69 - 60}{\frac{15}{\sqrt {25}}} \\
&= \frac{9}{3} \\
&= 3
\end{split}
$$
We will work through the 1 and 2 sided cases separately.

In the 1-sided case, we first check that the sign of $\bar z$ aligns with the alternate hypothesis:
- For $\bar z<0$, if $H_a$ suggests $\mu$ should be greater than $\mu_0$ then $\bar z$ does **NOT** support rejecting $H_0$
- For $\bar z > 0$, if $H_a$ suggests $\mu$ should be less than $\mu_0$ then $\bar z$ does **NOT** support rejecting $H_0$
In either case, no more work needs to be done, however another test with the other side version, or 2 sided version of $H_a$ may be useful depending on the experiment.

If the sign of $\bar z$ aligns, we can then work to find our $p$-value in terms of $Z$ and $\bar z$:
- If $\bar z < 0$ then our $p$-value is $P(Z<\bar z) = P(Z > |\bar z|)$
- If $\bar z > 0$ then our $p$-value is $P(Z>\bar z)$

Reminder that $Z$ is our standard normal distribution achieved via the central limit theorem
$$
Z = \frac{\bar X-\mu_0}{\frac{\sigma}{\sqrt{n}}}\sim N(0,1)
$$
where
$$
\bar X = \frac1n\sum^n_{i=1}X_i
$$

In the two sided case we compute
- $P(|Z|\geq |\bar z|)$ which covers two regions

>Note that in the one sided case, $>$ is used and in the 2 sided case $\geq$ is used. Either is fine in both cases. This has no effect on the result since the variable is a continuous random variable and the chance of any specific outcome is 0.

For our specific example this means we need:
- For the one sided case we need $P(Z \geq 3)\approx0.0015$
- For the two sided case we need $P(|Z| \geq 3)\approx 0.003$ 

>We know the above by the $1-2-3$ rule.

So the chance of this result being achieved given the null hypothesis $H_0$ is 0.3% in the 2 tailed version and 0.15% in the one tailed test?

So could we safely reject the null hypothesis? To answer that question we need to look at significance levels.
### Significance Levels
If 
$$
p<\alpha
$$
where $p$ is a $p$-value and $\alpha$ is a specified significance level, then we say the result is **statistically significant** at level $\alpha$.

If the data is deemed statistically significant, we can **reject** $H_0$.

Significance levels are are somewhat arbitrary. They should be chosen before the study to avoid unjustified conclusions, or shifting the significance level to achieve a desired conclusion.

Typically significance levels will be 5% or 1%, however others may be used.

The experiment we worked through about is statistically significant at $\alpha=1\%$ so it would be fine to reject the null hypothesis off of that result, however if we were stricter and chose $\alpha = 0.1\%$ then we would not be able to reject it.

Below you can see a table of $z$-statistics and the maximum significance levels they satisfy for both 1 and two sided tests

| $z$-statistic | 2-Sided | 1-Sided |
| ------------- | ------- | ------- |
| 1.645         | 10%     | 5%      |
| 1.96          | 5%      | 2.5%    |
| 2.326         | 2%      | 1%      |
| 2.576         | 1%      | 0.5%    |
If we changed the result of our experiment such that $\bar x=66$ this would change our $z$-statistic to
$$
z=\frac{66-60}{3}=2
$$
which from the table above would satisfy the 5% significance level but not the smaller, more accurate levels.

You can see an illustrative diagram below.
![[critical_values.png]]

There are two types of errors you can make when hypothesis testing:
- A **type 1** error is changing your mind when you shouldn't, rejecting a $H_0$ that is true
- A **type 2** error is not changing your mind when you should, not rejecting a false $H_0$

A lower significance level, decreases the probability of type 1 errors ($\alpha$ is actually synonymous with the probability of a type 1 error), although it increases the probability of a type 2 error.
### Sample Size
There is also a note here on sample size, but no detail is gone into. 

Obviously sample size has a massive impact on experiments. Smaller sample sizes will provide larger $p$-values for more extreme results where as sample sizes get larger you will start to see smaller $p$-values for comparatively smaller deviations.

For example a difference in the sample mean of 1 would mean very little when it comes to a sample of 10, but could mean a huge amount in a sample of 10,000,000.
## Fisher's Exact Test
Fisher's exact test is a test used to determine from a table, if there is a none random association between two categorical variables.

For example take the table below
![[fisher_example_table.png]]

The null hypothesis $H_0$ here would be that there is no association between the journal and the type of article.

Below is a general table of the same format
![[fisher_general_table.png]]
With $n=a+b+c+d$.

R. Fisher showed that this distribution is **hypergeometric**, and specifically showed that the $p$ value for this table and the given $H_0$ is given by
$$
\begin{split}
p 
&= \frac{\binom{a+b}a\binom{c+d}c}{\binom n{a+c}} \\
&= \frac{\binom{a+b}{b}\binom{c+d}d}{\binom n{b+d}} \\
&=\frac{(a+b)!(c+d)!(a+c)!(b+d)!}{a!b!c!d!n!}
\end{split}
$$

>Reminder that $\binom nk$ is the binomial coefficient

So in the case of this specific data we get
$$
\begin{split}
p_{data} = \frac{(5!)^26!4!}{5!0!1!4!10!} = 0.0238
\end{split}
$$

This $p$ value can vary widely even for datasets with all the same totals
![[fisher_same_marginals.png]]

This is called an **exact** test because the numbers are exact, not approximated. For larger samples, the factorials require large computations so instead the $\chi^2$ test is used. Read about that [here](https://en.wikipedia.org/wiki/Chi-squared_test).
## Closing Problem
"Let $n = 16$, $σ = 20$, $\bar x = 47.5$. Should we reject (or not reject) the null hypothesis $H_0$ that $µ = 60$ at the significance level 1%?"

We first need to find our $\bar z$ which is 
$$
\begin{split}
\bar z 
&= \frac{47.5-60}{\frac{20}{\sqrt n}} \\
&= \frac{12.5}{5} \\
&= 2.5
\end{split}
$$

Meaning that we can reject $H_0$ if doing a one tailed test, but cannot reject it if doing a two tailed test.