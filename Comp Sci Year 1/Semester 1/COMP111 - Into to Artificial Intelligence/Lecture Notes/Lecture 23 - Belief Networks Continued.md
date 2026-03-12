## Computing Joint Probability Distributions
Given a belief network, we can always assume an ordering$$F_1,...,F_n$$of it's random variables such that for all $i,j:$ $$F_i\to F_j \implies i<j$$
What this means is that one variable must come after another variable in the ordering for it to depend on it.

If we consider the domains we looked at from [[Lecture 22 - Conditional Independence and Belief Networks]], we can order the variables like so.

The student exam domain:$$Background,WorksHard,Answers,Grade$$
The fire alarm domain:$$Tampering, Fire, Alarm, Smoke, Leaving, Report$$
### The Chain Rule
The chain rule is an extension of the multiplication rule, and it states that, given $F_1,...,F_n$ we have for all $r_1,...,r_n$:$$
P(F_1=r_1,...,F_n=r_n)=P(F_1=r_1)\times P(F_2=r_2|F_1=r_1)\times...\times P(F_n=r_n|F_1=r_1,...,F_{n-1}=r_{n-1})
$$
If we use bold $\mathbf{P}$ notation this means:$$\mathbf{P}(F_1,...,F_n)=\mathbf{P}(F_1)\times\mathbf{P}(F_1|F_2)\times\mathbf{P}(F_3|F_1,F_2)\times...\times\mathbf{P}(F_n|F_1,...,F_{n-1})$$
We can combine the chain rule with belief networks to build our probability distribution.

As $parents(F_i)\subseteq \{F_1,...,F_{i-1}\}$ and any node $F$ is conditionally independent given it's parents we know that $$\mathbf{P}(F_i|F_1,...,F_{i-1})=\mathbf{P}(F_i|parents(F_i))$$
And so by combining this with the chain rule we can get $$\mathbf{P}(F_1,...,F_n)=\mathbf{P}(F_1)\times\mathbf{P}(F_2|parents(F_2)\times\mathbf{P}(F_3|parents(F_3))\times...\times\mathbf{P}(F_n|parents(F_n))$$
This is the same as the formula we saw last lecture [[Lecture 22 - Conditional Independence and Belief Networks]]$$\prod_{F\text{ in network}}\mathbf{P}(F\;|\;parents(F))$$
Consider our student exam domain. Using the formula above we can compute the full joint probability distribution $$\mathbf(P)(Background, WorksHard, Answers, Grade)$$by computing$$\mathbf{P}(Background)\times\mathbf{P}(WorksHard)\times\mathbf{P}(Answers|Background, WorksHard)\times\mathbf{P}(Grade|Answers)$$
Now consider our fire alarm domain. We can compute the full probability distribution $$\mathbf{P}(Tampering, Fire, Alarm, Smoke, Leaving, Report)$$by computing $$\mathbf{P}(Tampering)\times\mathbf{P}(Fire)\times\mathbf{P}(Alarm|Tampering,Fire)\times\mathbf{P}(Smoke|Fire)\times\mathbf{P}(Leaving|Alarm)\times\mathbf{P}(Report|Leaving)\times$$
## Querying
Consider again the fire alarm domain. Assume we have the following conditional probabilities (where we write $P(A | B)$ for $P(A = 1 | B = 1)$, $P(¬A | B)$ for $P(A = 0 | B = 1)$ and so on): 
- $P(Tampering) = 0.02$
- $P(Fire) = 0.01$
- $P(Smoke | Fire) = 0.9$
- $P(Smoke | ¬Fire) = 0.01$
- $P(Alarm | Fire ∧ Tampering) = 0.5$
- $P(Alarm | Fire ∧ ¬Tampering) = 0.99$
- $P(Alarm | ¬Fire ∧ Tampering) = 0.85$ 
- $P(Alarm | ¬Fire ∧ ¬Tampering) = 0.0001$
- $P(Leaving | Alarm) = 0.88$
- $P(Leaving | ¬Alarm) = 0.001$
- $P(Report | Leaving) = 0.75$
- $P(Report | ¬Leaving) = 0.01$

Notice how, if $Report$ is observed then the probability of $Fire$ and $Tampering$ go up:$$P(Fire)=0.01 \text{ and } P(Fire\;|\;Report)=0.2305$$$$P(Tampering) = 0.02\text{ and } P(Tampering\;|\;Report) = 0.399$$
Notice again, that if smoke is observed in addition to report the probability of $Fire$ goes up further but the probability of $Tampering$ goes down:$$P(Fire\;|\;Report\;\land\;Smoke)=0.964$$ $$P(Tampering\;|\;Report\;\land\;Smoke)=0.0284$$
If, however, $\lnot Smoke$ is observed in addition to $Report$ the probability of $Tampering$ goes up while the probability of $Fire$ goes down:$$P(Fire | Report\;\land\;¬Smoke) = 0.0294$$$$P(Tampering | Report\; ∧\; ¬Smoke) = 0.501 $$
## Summary
- Belief networks are a representation of conditional independence in probabilistic models.
- Querying can often be done using exact inference (with algorithmic tricks).
- Sometimes exact inference too hard. There are also approximate algorithms.
- Lots of research on determining belief networks from data. Either determining the conditional probabilities or even the structure of a belief network

18-11-25 Finish Belief Networks, Slide 23