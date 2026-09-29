## Random Variables
Let $(S,P)$ be a probability space. A random variable $F$ is a function $F:S\to \mathbb{R}$ that assigns to every $s\in S$ a single number $F(s)$.

It's a bit of a misnomer to call it a random variable, since it's neither a variable or random. It comes from the English translate of **variabile casuale**.

We still assume that the sample space $S$ is finite. Therefore, given a random variable $F$ from a sample space $S$, the set of numbers $r$ that are values of $F$ is finite as well.

>If you look at [[Lecture 15 - Set Cardinality Continued and Intro to Functions]], you will notice that the set of $r$ is the same as the **range** of the random variable $F$.

The event that $F$ takes the value $r$, the event $\{s\;|\;F(s)=r\}$, is denoted by $(F=r)$. The probability of the event $(F=r)$ is then $$P(F=r)=P(\{s\;|\;F(s)=r\})$$
### Example 1
Problem "Let $(S,P)$ be a uniform probability space with $$S=\{car, train,plane,ship\}$$
Then the function $F:S\to \mathbb{R}$ defined by $$F(car)=1,\;F(train)=1,\;F(plane)=2\;,F(ship)=2$$is a random variable.

What is the probability of $(F=1)?$"

To answer this question, the first thing we need to do is define determine the event $(F=1)$. $$
(F=1)=\{s\;|\;F(s)=1\}=\{car,train\}
$$
Since we know that $(S,P)$ is a uniform probability space we know that $$P(car)=P(train)=P(plane)=P(ship)=\frac14$$and so we know
$$
P(\{car,train\})=P(car)+P(train)=\frac14+\frac14=\frac12
$$
Therefore $$P(F=1)=P(\{car,train\})=\frac12$$
### Example 2
Problem "Suppose that I roll two dice. So the sample space is $$S = {1, 2, 3, 4, 5, 6}^2$$ and $P(ab) = \frac1{36}$ for every $ab ∈ S$. 

Let $$F(ab) = a + b$$F is a random variable.

What is the probability that $(F=12)$?"

To do this we first need to find the event $(F=12)$ which can be done by listing all the pairs of numbers from $1\to6$ that sum to 12. Which is only 1 pair, six and six. So$$(F=12)=\{66\}$$
Since $(F=12)$ only contains one element, and rolling two dice gives a uniform sample space we know that $$P(F=12)=P(\{ab\;|\;F(ab)=12\})=P(66)=\frac{1}{36}$$
## Probability Distributions
When defining a probability distribution $P$ for a random variable $F$, we usually don't specify the sample space $S$ but directly assign a probability to the event that $F$ takes a certain value.

So we directly assign $$P(F=r)$$of the event that $F$ has value $r$.

Observe that:
- $0\leq P(F=r)\leq 1$
- $\sum_{r\in \mathbb{R}}P(F=r)=1$

And so the events $(F=r)$ behave in the same way as outcomes of a random experiment.

We will discuss probability distributions of random variables more in [[Lecture 21 - Random Variables Continued]]
## Notation and Rules
**We write $\lnot(F=r)$ for the event $\{s\;|\;F(s)\neq r\}$.

For example, assume the random variable $Die$ can take values $\{1,2,3,4,5,6\}$ and $$P(Die=n)=\frac16$$for all $n\in \{1,2,3,4,5,6\}$ meaning the die is fair.

In this case $\lnot (Die=1)$ denotes $(Die = 2)$ or $(Die = 3)$ or $(Die = 4)$ or $(Die = 5)$ or $(Die = 6)$. We know from the complement rule that $$P(\lnot(F=r))=1-P(F=r)$$and so $$P(\lnot (Die=1))=1-\frac16=\frac56$$
**We write $(F_1 = r_1, F_2 = r_2)$ for "$(F_1=r_1)$ and $(F_2=r_2)$".**

**We write $(F_1 = r_1)\lor (F_2 = r_2)$ for "$(F_1=r_1)$ or $(F_2=r_2)$".**

**Conditional probability rules still apply.** 

So $$P(F_1 = r_1| F_2 = r_2)=\frac{P(F_1 = r_1, F_2 = r_2)}{P(F_2=r_2)}$$
**The multiplication rule still applies.**

So $$P(F_1 = r_1, F_2 = r_2)=P(F_1 = r_1| F_2 = r_2)P(F_2=r_2)$$
**We will sometimes use symbols distinct from numbers to denote values of random variables.**

So, for example, if we have a random variable $Weather$ we could use the values $$sunny,rain,cloudy,snow$$instead of 1, 2, 3, 4. Therefore $$(Weather=sunny)$$denotes that it is sunny.

**We can use multiple random variables for the same domain.**

For example, consider a visit to the dentist. We could use random variables Toothache, Cavity, and Catch (the dentist's probe catches in the tooth) which all take values $0$ and $1$ representing true and false.

For example, (Toothache = 1) states that the person has toothache and (Toothache = 0) states that the person does not have toothache.
## Probabilistic Models
In order to model a domain using probability theory, you first must introduce the relevant random variables. We have seen 2 basic examples:
- The weather domain, modelled with a single random variable that can take the values $sunny,rain,cloudy,snow$
- The dentist domain, modelled using the 3 random variables Toothache, Cavity, and Catch, which all take values 0 and 1.

We will now discuss a few more domain's, including ways of modelling them.
### Student Exam Domain
To get a basic model of the performance of a student in an exam we could use the following random variables:
- $Grade$ - which takes as values the possible grades of a student in the exam, say $\{A,B,C,D,E,F\}$
- $Answers$ - which takes as values the answers given by the student in the exam, not really possible to list here.
- $Background$ - which takes as a value the school visited before coming to university, say $\{Comprehensive, Academy, Public\}$
- $WorksHard$ - which takes as a value the degree to which the student works hard, say $\{0,1\}$

We could be interested in $$
P(Grade=A\; |\; WorksHard=1,Background=Comprehensive,)
$$
### Fire Alarm Domain
A basic model of a fire alarm system and reporting about it could be given by the following random variables (all take value 0 or 1): 
- $Fire$: there is fire;
- $Alarm$: the alarm goes off;
- $Tampering$: there is tampering with the alarm system;
- $Smoke$: there is smoke (no smoke detector used);
- $Leaving$: people leave the building;
- $Report$: it is reported that people leave the building (reporting not always correct). 

We might be interested in $$P(Fire = 1\;|\;Report = 1)$$