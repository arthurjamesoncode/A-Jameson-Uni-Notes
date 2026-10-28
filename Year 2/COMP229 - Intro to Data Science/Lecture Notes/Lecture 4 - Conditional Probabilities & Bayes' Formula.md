## Fair Coin Flips
Imagine you flip a fair coin 2025 times and you get 2025 heads. What is the probability of getting heads on your 2026'th flip?

The answer, since it is a fair coin, is 0.5. This is because individual coin flips are independent of each other.

However the probability of getting 2025 heads in a row is very small at
$$
0.5^{2025}
$$
which genuinely returns 0 if you put it into a calculator because of how small that number is.

>It's not actually 0 it's just so small the calculator approximates it as 0. $0.5^{329}$ is the smallest power of 0.5 that returns 0 in a calculator, so you can see how insanely small $0.5^{2025}$ is.

This probability that it makes sense to adjust our expectation of the coin away from being fair and towards being biased. More details on this sort of thing in [[Lecture 10 - Hypotheses and Significance]].

It is actually possible to get a fair game from a biased coin. John von Neumann came up with an algorithm to do so which is:
- Flip the coin twice;
- If we get HH or TT, ignore the results and flip the coin twice again;
- If we get HT or TH, ignore the second flip and use the outcome of the first flip;

This guarantees a sequence that behaves like a fair coin because the probability of getting HT and TH are the same, given that each individual coin flip is independent. Ignoring repeated results means no results will show up more than would be possible/reasonable with a fair coin.

We can see this formally with
$$
\begin{split}
P(H)=p,\;P(T)=q 
\implies 
&P(HH)=p^2, \\
&P(TT)=q^2, \\
&P(TH)=pq=P(HT)
\end{split}
$$
## Conditional Probability
For events $A$ and $B$ the conditional probability that $A$ happens given $B$ has happened is
$$
P(A|B)=\frac{P(A\cap B)}{P(B)}
$$

This extends into the general product rule which is that
$$
P(A\cap B)=P(A|B)P(B)
$$

For example take the image below
![[probability_venn.png]]

From this we can compute the probability of $A$ given $B_1$, $B_2$, and $B_3$
$$
\begin{split}
P(A|B_1)
&= \frac{0.1}{0.1} \\
&= 1 \\
\\
P(A|B_2)
&= \frac{0.12}{0.12+0.04} \\
&= \frac34 \\
\\
P(A|B_3)
&=\frac0{0.1} \\
&=0
\end{split}
$$

As another example consider the following problem:
	"Because males have only one X chromosome and females have two, men are about 16 times more likely to suffer the adverse effects of a defective X chromosome, and therefore to be colour blind. 
	Assume that the male/female ratio is 50/50, and about 4.25% of all people are colour blind. Find the conditional probabilities $P(CB | male)$ and $P(CB | female)$ (CB meaning colour blind)"

We know that 
- $P(CB)=0.0425$
- $P(male)=0.5=P(female)$
- $P(male \cap CB)=16\cdot P(female \cap CB)$

We can work out from this that
$$
\begin{split}
P(CB | male) &= \frac{P(CB \cap male)}{0.5} \\
P(CB | female) &= \frac{P(CB \cap female)}{0.5} \\
\end{split}
$$
So if we can just find the probability that someone is both colour blind and male, or colour blind and female, we have our answer.

Given that $4.25\%$ of people are colourblind and $\frac{16}{17}$ of these people are male, we know that
$$
4.25\% \cdot \frac{16}{17} =4\%
$$
of all people are male and colourblind, leaving $0.25\%$ of people being female and colourblind.

Since we have this we can see
$$
\begin{split}
P(CB | male) 
&= \frac{0.04}{0.5} \\
&= 0.08 \\
P(CB | female) 
&= \frac{0.0025}{0.5} \\
&= 0.005
\end{split}
$$
So 8% of men are colour blind and 0.5% of women are colour blind.
### Law of Total Probability
The above example implicitly used something called the law of total probability. 

This states that if the sample space $\Omega$ can be partitioned into pairwise disjoint events 
$$
(B_1,...,B_n)\;\text{ where }\; \Omega=\bigsqcup_nB_n
$$
then for any event $A$
$$
P(A|B_n)=\frac{P(A\cap B_n)}{P(B_n)}
$$
and therefore 
$$
\begin{split}
P(A) 
&= \sum_nP(A\cap B_n) \\
&= \sum_nP(A|B)P(B)
\end{split}
$$

>$\bigsqcup$ means disjoint union.

In the above example we stated that if men are 16 times more likely to be colourblind then women that $\frac{16}{17}$ of all colourblind people were men. This implicitly uses this law of total probability, and is why that works.
### Bayes-Price-Laplace Formula
From the conditional probability formula we can derive
$$
P(A|B)=\frac{P(B|A)P(A)}{P(B)}
$$

this is of course because 
$$
P(A\cap B) = P(B|A)P(A)
$$

## Cancer Screening Example
Consider the following problem:
	"At the age of 40, about 1% of women have breast cancer. Screening gives a (true) positive result for 80% of women with breast cancer, and a (false) positive result for 10% of women without breast cancer. A woman in her 40s tested positive. What’s the probability that she has cancer?"

Intuition might suggest that since it correctly detects cancer $80\%$ of the time that the probability that a woman who tested positive has cancer is $80\%$.

However this makes a fatally wrong assumption that
$$
P(Positive|Cancer)=P(Cancer|Positive)
$$
This is not the case, and this assumption is called the **base rate fallacy**.

We know the following from the question:
- $P(Cancer) = 0.01$
- $P(Positive|Cancer)=0.8$
- $P(Positive|No\;Cancer)=0.1$
- We are looking for $P(Cancer|Postive)$.

We know that
$$
\begin{split}
P(Cancer|Positive) 
&= \frac{P(Positive|Cancer)P(Cancer)}{P(Positive)} \\
&= \frac{0.8\cdot0.01}{P(Positive)} \\
&= \frac{0.008}{P(Positive)}
\end{split}
$$

So if we find the value for $P(Positive)$ we find our answer.

We know that 
$$
\begin{split}
P(Positive \cap Cancer) 
&= P(Positive|Cancer)P(Cancer) \\
&= 0.8 \cdot 0.01 \\
&= 0.008
\\
P(Positive \cap No\; Cancer)
&= P(Positive|No\;Cancer)P(No\; Caner) \\
&= 0.1\cdot0.99 \\
&= 0.099
\end{split}
$$

By the law of total probability we know
$$
\begin{split}
P(Postive) 
&= 0.008 + 0.099 \\
&= 0.107
\end{split}
$$

And so
$$
\begin{split}
P(Cancer|Positive) 
&= \frac{0.008}{0.107} \\
&= 0.07476635514
\end{split} 
$$
<u><b>So about 7.5% chance of this woman having cancer</b></u>.

This is quite a stark difference given the reasonably high accuracy stated by the test. The problem is that false positives matter a huge amount more given that the size of the population who is actually positive is much larger.

You can see this pictured below.
![[cancer_detected_venn.png]]

If we change the accuracy of the test on people who do have cancer the above probability won't change that much:
- If $P(Positive|Cancer)=0.7$ then $P(Cancer|Positive)=0.066$
- If $P(Positive|Cancer)=1$ then $P(Cancer|Positive)=0.09$

If we change the accuracy of the test on people who don't have cancer it has a larger effect. If we see change the chance of a false positive to 0.2 given no cancer we see 
$$
P(Cancer|Positive)=4\%
$$

If we change $P(Cancer)$ to $0.02$ this will have the largest effect. Now we see:
$$
P(Cancer|Positive)=20.6\%
$$

The ratio
$$
\frac{P(Positive|Cancer)}{P(Positive)}
$$
tells us how much a positive test multiplies the probability of someone having cancer.
## Measurements of Successful Tests
This part of the lecture is spent going over some measurements of successful tests and when they are useful, or when they are misleading.
### Accuracy
**Accuracy** is one measure of success, but is not the best one.

Given that 1% of women at the age of 40 have breast cancer, how can we make a test that is 99% accurate.

The simplest way to do this is to just make a test that always says no. It will be right in 99% of cases and wrong in 1%.

This is obviously a flawed way to go about it, and shows the limits of **accuracy** as a measurement of success for any classifier.

Instead we usually use the following measures to measure the success of a test.
### Better Measures
**Sensitivity** is the proportion of relevant test cases that are successfully detected and is given by
$$
P(test\;positive | actually\;positive)
$$

Specificity is the number of non-relevant cases that are correctly rejected and is given by
$$
1-P(test\;positive|actually\;negative)
$$
These are two relevant measures for almost all tests.

Another two measures that are used are precision and recall.

**Recall** is the number of correct positives divided by the total number of items that should have been classified as positive, given by
$$
\frac{\text{True Positives}}{\text{True Positives + False Negatives}}
$$

**Precision** is the number of correct positives divided by the number of items that have been classified as positives, given by
$$
\frac{\text{True Positives}}{\text{True Positives + False Positives}}
$$

You can see these four measures compared below
![[measures compared.png]]

>You might notice that recall and sensitivity are actually the same thing, but the terms are used in different contexts, hence they have both been explained.

So for the cancer example above we can see:
- Sensitivity and recall are $P(Positive | Cancer) = 0.8=80\%$
- Specificity is $1-P(Positive| No\; Cancer)=1-0.1=0.9=90\%$
- Precision is $P(Cancer|Positive)\approx 0.075=7.5\%$

What's better is to use a **full confusion matrix** which depicts the actual condition vs predictions. You can see an example of this below.

![[confusion_matrix.png]]

The top left is the actual confusion matrix, the rest are all derived metrics.
### F Scores
The F Score of a test is its harmonic mean of precision and recall.

So
$$
\frac1{F_1}=\frac{\frac1{recall}+\frac1{precision}}2
$$
and
$$
F_1=2\cdot\frac{precison\cdot recall}{precision+recall}
$$

This can also be generalised to add a weight. If recall is $\beta$ times more important than precision then
$$
F_\beta=(1+\beta^2)\cdot(\frac{precision\cdot recall}{\beta^2\cdot precision + recall})
$$

1 is the maximum (and best) while 0 is the minimum (and worst).

Given a model which has:
- 100 True positives
- 100 False positives
- 0 False Negatives
How good is this model using an $F_1$ score?

Well we can just plug in our values
$$
\begin{split}
recall 
&= \frac{100 }{100 + 100} \\
&= \frac12
\\
precision
&= \frac{100}{100+0} \\
&= 1
\\
F_1
&=2\cdot\frac{1\cdot\frac12}{1+\frac12} \\
&=\frac1{\frac32} \\
&=\frac23 \\
&\approx 0.667
\end{split}
$$
This seems like a pretty good F score, but what if our model is imbalanced? Consider the confusion matrix below.

![[confusion_matrix_f.png]]

True negatives are not considered at all by our F score. If TN is 0, and our model only outputs true, it could still give a reasonable high F score.

The problem is that when classes become unbalanced, F score is not an appropriate measure. The general assumption in ML is that there are a huge number of negatives, although this can be violated in practice.
## Closing Problem
The lecture ends with the following problem:

"In genetics, Bayes’ rule helps estimate the probability of a specific genotype, such as the risk of being affected by a disease or of carrying a recessive gene. Let’s apply it to cystic fibrosis, a genetic disorder caused by mutations in the CFTR gene, leading to thick, sticky mucus that primarily affects the lungs and digestive system. 

Genetic testing for cystic fibrosis (CF): a female patient with a family history of CF tests negative for carrier status. 

If both her parents are carriers, she inherits one of four equally likely gene combinations: CN or NC (she is a carrier), NN (non-carrier) or CC (affected). The patient is unaffected, so the CC case is excluded, leaving three possible combinations: CN or NC when she is a carrier, and NN when she’s not. Hence the prior probability of being a carrier is 2/3, and of being a non-carrier is 1/3. 

The genetic test detects 90% of carriers: the probability of a negative result is 0.1 if she is a carrier, and 1 if she is not. Her male partner has the same priors and also tests negative. What is the probability that their child will still be affected by CF?"

We are looking for $P(Child\;is\;Carrier)$ which depends on:
- $P(Mum\; is\; Carrier)$
- $P(Dad\;is\;Carrier)$
The above are independent, have the same conditions and are therefore equal.

If both parents are carriers, the child will be affected 1/4 of the time.

We are going to use $C$ for "is carrier" and $N$ for negative test
$$
\begin{split}
P(C|N) 
&= \frac{P(N|C)P(C)}{P(N)} \\
&= \frac{0.1\cdot\frac23}{P(N)} \\
&= \frac{2}{30P(N)}
\end{split}
$$

We know from the law of total probability that
$$
\begin{split}
P(N) 
&= P(N|C)P(C) + P(N|\lnot C)(1-P(C)) \\
&= 0.1\frac23 + 1\frac13 \\
&= 0.4
\end{split}
$$
And so 
$$
\begin{split}
P(C|N) 
&= \frac{2}{30(0.4)} \\
&= \frac16
\end{split}
$$
Which makes the chance that both parents are carriers
$$
(\frac{1}{6})^2 = \frac{1}{36}
$$

and since the child has a 1/4 chance to be affected only if both parents are carriers the total chance of the child being affected is
$$
P(Affected) = \frac14\cdot\frac{1}{36} = \frac{1}{144} = 0.00694
$$