### Uncertainty
Logic based KR&R methods mostly assume that knowledge is certain, which is obviously not always the case. Often things are either uncertain or it's impossible to list every assumption that makes them certain.

Consider the following problem "When going to the airport by car, how early should I start?" 

45 minutes should be enough from Liverpool to Manchester Airport, but only under the assumption that there are no accidents, no lane closures, that my car does not break down, and so on. This uncertainty is hard to eliminate, but still an agent has to make a decision.

Consider also "A dental patient has toothache. Does the patient have a cavity?" 

One might want to capture the relationship between patients having a cavity and patients having toothache by the rule: $$Toothache(x) → Cavity(x)$$But this does not work as not every toothache is caused by a cavity. But it's hard to come up with exhaustive list of reasons: $$Toothache(x) → Cavity(x)∨GumProblem(x)∨Abscess(x)∨· · ·$$
If we try to use exact rules to cope with a domain like medical diagnosis or traffic, we will fail. This is because:
- Laziness. It is too much work to list an exceptionless list of rules
- Theoretical Ignorance. Medical science has, in many cases, no strict causality between some symptoms and diseases.
- Practical ignorance. Even if we have strict laws, we may not be able to act with certainty because a particular patient because not all the necessary tests have been, or even can be, run.

Probability gives us a way to summarize all the uncertainty that comes from our laziness or ignorance.

We might not know for sure what a particular patient has, but if they have a toothache we can say that there is an (arbitrary) 80% chance that a patient has a cavity.

This 80% summarises all the cases in which factors needed for a cavity to cause a toothache are present, but also includes all the cases in which the patient has a toothache and cavity but they are unrelated.

The other 20% summarizes all the other possible causes of toothache that we are too lazy or ignorant to confirm or deny.
### Discrete Probability
We represent random experiments using **discrete probability spaces** $(S, P)$ consisting of:
- The **sample space** $S$ of all **elementary events** $x\in S$. We call members of $S$ the **outcomes** of the experiments. Each individual outcome is mutually exclusive, meaning that they cannot happen at the same time, but sets of these outcomes may overlap.
- A **probability distribution** $P$ assigning a real number $P(x)$ to every elementary event $x\in S$ such that for all $x\in S,\; 0\leq P(x)\leq 1$ and $\sum_{x\in S}P(x)=1$. This tells us the chance of each individual event happening.

>$\sum_{x\in S}P(x)=1$ means the sum of all the probabilities for $P(x)$

For example, consider the random experiment of flipping a coin once. The probability space $(S,P)$ for this experiment is given by:
- $S=\{H,T\}$
- $P(H)=P(T)=\frac{1}{2}$

We can see that $S$ contains 2 outcomes, heads (H) and tails (T). We can see the probability assigned to each one is $\frac{1}{2}$.

If we consider, instead, the random experiment of flipping a coin twice, the probability space $(S,P)$ is given by:
- $S=\{HH,HT,TH,TT\}$
- $P(HH)=P(HT)=P(TH)=P(TT)=\frac{1}{4}$

Here we have twice as many outcomes, but there are still few enough to list and they still all have the same probability.

Consider the random experiment of rolling of die. The probability space $(S,P)$ for this experiment is given by:
- $S=\{1,2,3,4,5,6\}$
- $\forall x\in S: P(x)=\frac{1}{6}$

>$\forall$ means for all. The above means that the probability of all outcomes  is $\frac{1}{6}$

Consider the probability of rolling a die $n$ times. Then the probability $(S,P)$ is given as follows:
- $S$ is the set of sequences of length $n$ of the digits $\{1,...,6\}$. This can be denoted by $\{1,...,6\}^n$.
- $\forall x\in S: P(x)=\frac{1}{6^n}$. This is because there are $6^n$ elements of $S$ and they all have the same probability.

