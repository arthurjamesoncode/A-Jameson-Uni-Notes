## Probability Distributions
The probability distribution for a random variable gives the probabilities of all the possible values of the random variable.

For example let $Weather$ be a random variable with values $$(sunny,rain,cloudy,snow)$$such that its probability distribution is given by:
- $P(Weather=sunny)=0.7$
- $P(Weather=rain)=0.2$
- $P(Weather=cloudy)=0.08$
- $P(Weather=snow)=0.02$

We assume the order of the values is fixed and instead write $$
\mathbf{P}(Weather)=(0.7,0.2,0.08,0.02)
$$
The bold $\mathbf{P}$ indicates that the result is a vector of numbers representing the individual values of $Weather$.

If we assume the random variable $Die$ can take the values $1,2,3,4,5,6$ and represents a fair die then we can define it's probability distribution as $$
\mathbf{P}(Die)=(\frac16,\frac16,\frac16,\frac16,\frac16,\frac16)
$$
Consider the random variable $F(ab)=a+b$ from the sample space $S=\{1,2,3,4,5,6\}^2$ with $P(ab)=\frac1{36}$ for all $a,b\in\{1,2,3,4,5,6\}$.

The possible values for this variable are $2,3,4,5,6,7,8,9,10,11,12$ and we can define it's probability distribution as $$\mathbf{P}(F)=(\frac{1}{36},\frac{2}{36},\frac{3}{36},\frac{4}{36},\frac{5}{36},\frac{6}{36},\frac{5}{36},\frac{4}{36},\frac{3}{36},\frac{2}{36},\frac{1}{36})$$
## Joint Probability Distributions
Let $F_1,...,F_k$ be random variables. A joint probability distribution for $$F_1,...,F_k$$gives the probabilities $$P(F_1=r_1,...,F_k=r_k)$$for the events $$(F_1=r_1) \text{ and } ... \text{ and } (F_k=r_k)$$for all possible values $r_1,...,r_k$.

The joint probability distribution is denoted by $$\mathbf{P}(F_1,...,F_k)$$
Essentially, the joint probability distribution assigns a probability to each combination of events.

Consider the following table. It gives us a joint probability distribution $\mathbf{P}(Weather ,Cavity)$ for the random variables $Weather$ and $Cavity$.

![[joint_weather_cavity.png]]

>Notice that all the probabilities in this distribution still sum to 1!

### Full Joint Probability Distribution
A full joint probability distribution $\mathbf{P}(F_1,...,F_k)$ is a joint probability distribution for all relevant random variables $F_1,...,F_k$ for a domain of interest.

Every probability question about a domain can be answered by the full joint probability distribution because the probability of every event is a sum of probabilities $$P(F_1=r_1,...,F_k=r_k)$$
Often, we call $r_1,...,r_k$ data points, or sample points.

If we assume the random variables $Toothache, Cavity, Catch$ fully describe a visit to the dentist then we can see a full joint probability distribution given by the following table:
![[full_joint_example.png]]

The full joint probability for the student exam domain, discussed in [[Lecture 20 - Random Variables]], would be denoted $$\mathbf{P}(Grade,Answers,Background,WorksHard)$$and would give the probability of every possible combination of values of the random variables $Grade$, $Answers$, $Background$, and $WorksHard$.

The full joint probability distribution for the fire alarm domain gives the probability for every possible combination of values of the random variables $Fire$, $Alarm$, $Tampering$, $Smoke$, $Leaving$, and $Report$.
### Marginalization
The marginal probabilities of a random variable within a domain, is the same as that variables single probability distribution.

When given a joint probability distribution $\mathbf{P}(F_1,...,F_k)$, you can compute the marginal probabilities of the random variables $F_i$ by summing out the remaining variables.

If we consider the dentist joint probability table, we can find the probability of a cavity by summing the first row of the table $$
P(Cavity=1)=0.108+0.012+0.072+0.008=0.2
$$
We can then find the probability of not having a cavity either by summing the second row of the table, or by using the complement rule.
### Conditional Probability Distributions
We can also compute conditional distributions from the full joint distribution. We use the $\mathbf{P}$ notation for conditional distributions.

$\mathbf{P}(F\; |\; G)$ gives the conditional distribution of $F$ given $G$ given by the probabilities $\mathbf{P}(F = r\;|\; G = s)$ for all values $r$ and $s$. 

Using $\mathbf{P}$ notation, the general version of the multiplication rule is as follows: $$\mathbf{P}(F, G) = \mathbf{P}(F | G)\mathbf{P}(G)$$which stands for the list of equations $$\mathbf{P}(F = r_1, G = s_1) = \mathbf{P}(F = r_1 | G = s_1)\mathbf{P}(G = s_1),\;\;\mathbf{P}(F = r_1, G = s_2) = \mathbf{P}(F = r_1 | G = s_2)\mathbf{P}(G = s_2)\;... $$
### Probabilistic Inference
Probabilistic inference is the computation of probabilities for certain query variables, given observed evidence.

If we call our query variable $Q$ and our observed results of the variables $E_1,...,E_n$ we will call $e_1,...,e_n$ then we can define probabilistic inference as computing $$\mathbf{P}(Q|E_1=e_1,...,E_n=e_n)$$
We can use a joint probability distribution to do this. Consider the following problem.

"Given the joint probability distribution table below, compute the conditional probability distribution for $Cavity$ given the observation $Toothache=1$.

![[full_joint_example.png]]
"

To start this problem let's consider what our query variable is and what our observed results are:
- Our query variable is $Cavity$
- We only have 1 observed result and that is that $Toothache=1$

And so we just need to compute:
- $P(Cavity=1\;|\;Toothache=1)$
- $P(Cavity=0\;|\;Toothache=1)$

Using our rules for conditional probability, and the table we can compute these easily.
$$P(Cavity=1\;|\;Toothache=1)=\frac{P(Cavity=1,Toothache=1)}{P(Toothache=1)}=\frac{0.12}{0.2}=0.6$$$$P(Cavity=0\;|\;Toothache=1)=\frac{P(Cavity=0,Toothache=1)}{P(Toothache=1)}=\frac{0.08}{0.2}=0.4$$
We can use the denominator $0.2$ to find a normalisation constant, $\alpha$. This gives us a way to quickly compute conditional probability distributions.

We get $\alpha$ by dividing by our denominator, so $\alpha=\frac{1}{0.2}=5$. If we multiply all the probabilities of the joint probability distribution where our observed result is true by $\alpha$ then we get the conditional probability. The normalisation constant ensures that all the probabilities sum to 1.

So instead of computing what we did above we can do $$\mathbf{P}(Cavity\;|\;Toothache=1)=\alpha \mathbf{P}(Cavity, Toothache=1)=5(0.12,0.08)=(0.6,0.4)$$

Essentially what a normalisation constant allows for us to is to give us a quick way to compute conditional probability distributions.
## Combinatorial Explosion
This approach does not scale well: for a domain described by $n$ random variables taking $k$ distinct values each we face two problems: 
- Writing up the full joint distribution requires $k^n − 1$ entries;
- How do we find the numbers (probabilities) for the entries? 

For these reasons, the full joint distribution in tabular form is not a practical tool for building reasoning systems.