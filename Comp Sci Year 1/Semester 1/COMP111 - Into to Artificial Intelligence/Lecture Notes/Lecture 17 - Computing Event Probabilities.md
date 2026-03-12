### Uniform Probability Distributions
In [[Lecture 16 - Reasoning Under Uncertainty]], we gave some examples of probability spaces, namely for flipping a coin, or multiple coins, and rolling a dice, or multiple die. 

Both of these are examples of "uniform probability distributions", which mean that every outcome is equally likely.

For a uniform probability distribution, the probability of an outcome $x$ is 1 divided by the number of of outcomes in $S$ ($|S|$).
## Events
An **event** is a subset $E\subseteq S$ of the sample space $S$.

>It helps to understand the content in [[Lecture 11 - Naïve Set Theory]] and the following lectures from the COMP109.

The probability of the event $E$ is given by $$P(E)=\sum_{x\in E}P(x)$$
Notice that:
- $\forall E\subseteq S,\; 0\leq P(E)\leq 1$ 
- $P(\emptyset)=0$ and $P(S)=1$

For example, if I roll a die three times, the event $E$ of rolling at least one 6 is given by:
- The set of sequences of length 3 over $\{1,...,6\}$ containing at least one 6. This is the same as the number of elements of $\{1,...,6\}^3$ containing at least one 6.
- $P(E)$ is $|E|$ divided by $|\{1,...,6\}^3|$. We know that $|\{1,...,6\}^3|$ is $6^3=216$. We will talk about exactly how to compute this later.

If we roll a fair die, then the event $E$ of rolling an odd number is given by:
- The set $E=\{1,3,5\}$
- $P(E)=P(1)+P(3)+P(5)=\frac{1}{6}+\frac{1}{6}+\frac{1}{6}=\frac{1}{2}$
### Complement of An Event
We call the chance of $E$ not happening under $S$ the complement of $E$ or $E^c$ or $\lnot E$.

You can see a representation of $E$ below.
![[event_complement.png]]

To calculate $P(\lnot E)$, we can do $$
P(\lnot E)=1-P(E)
$$
This is because $\lnot E=S-E$, and so $$1=\sum_{x\in S}P(x)=\sum_{x\in E}P(x)+\sum_{x\in \lnot E}P(x)$$
For example, consider the problem "What is the probability that at least one bit in a randomly generated sequence of 10 bits is 0?"

The probability space $(S,P)$ to consider for this question is given by:
- $S=\{0,1\}^{10}$ (This represents all sequences of length 10 made up by 1s and 0s)
- $\forall x\in S,\; P(x)=(\frac{1}{2})^{10}=\frac{1}{2^{10}}$

We can see that:
- $E=$ all sequences of length 10 made up by 1s and 0s containing at least one 0.
- $\lnot E=\{1111111111\}$

Since $|\lnot E|=1$ we know that $P(\lnot E)=\frac{1}{2^10}$ and therefore:
- $P(E)=1-\frac{1}{2^{10}}$
## The Union of Two Events
Calculating the probability of the union of two events, $E_1$ and $E_2$, happens is the same as calculating the probability that $E_1$ or $E_2$ happens.

We can see that the probability of the union of 2 events is $$
P(E_1\cup E_2)=P(E_1)+P(E_2)-P(E_1\cap E_2)
$$
>$\cup$ is the symbol for union, and $\cap$ is the symbol for intersection.

This is the same as saying that $P(E_1\cup E_2)$ is the same as the sum of the chance of $E_1$ happening and $E_2$ happening minus the chance of them both happening. This is intuitive as $E_1\cap E_2$ is a subset of both $E_1$ and $E_2$, so when we sum both $E_1$ and $E_2$ we count $E_1\cap E_2$ twice.

>If you go read [[Lecture 14 - The Cardinality of Sets]] you can see that the formula for the probability of the union is very similar to the formula for the cardinality of the union of the sets.

For example: consider the following problem:

"Suppose I have a jar of 30 sweets as follows

|              | red | blue | green |
| ------------ | --- | ---- | ----- |
| **circular** | 2   | 4    | 3     |
| **square**   | 6   | 7    | 8     |
The sample space $S$ has 30 elements and has a uniform probability distribution. This means that each individual sweet $x$ has a chance of being chosen at random $P(x)$ of $$
P(x)=\frac{1}{30}$$
For all $x\in S$, what is the probability of choosing a red or circular sweet?"

In this problem the events that we are concerned with are the red sweets $R$ and the circular sweets $C$. We are trying to figure out $P(R\cup C)$, which we can do with the formula outlined above. 

From the table we know:
- There are $2+6=8$ red sweets, so $|R|=8$ 
- There are $2+4+3=9$ circular sweets, so $|C|=9$
- There are $2$ sweets which are both red and circular, so $|R\cap C|=2$

From this we can get our probabilities:
- $P(R)=\frac{|R|}{|S|}=\frac{8}{30}$
- $P(C)=\frac{|C|}{|S|}=\frac{9}{30}$
- $P(R\cap C)=\frac{|R\cap C|}{|S|}=\frac{2}{30}$

Plugging this into our formula we get $$P(R\cup C)=\frac{8}{30}+\frac{9}{30}-\frac{2}{30}=\frac{15}{30}=\frac{1}{2}$$
We can also do this by finding $|R\cup C|$ as $P(R\cup C)=\frac{|R\cup C|}{|S|}$.

Since $|R\cup C|=2+6+4+3=15$ we know $P(R\cup C)=\frac{15}{30}=\frac{1}{2}$.
### The Union of Three or More Events
To calculate the union of 3 events, we sum the probability of the events, subtract the probability of the two way intersections of the events and add the probability of the three way intersections back again.

This demonstrates the principle of inclusion and exclusion. I won't go into detail here, but you can read more about this in [[Lecture 15 - Set Cardinality Continued and Intro to Functions]]. This talks about it in terms of set cardinality instead of probability but since $P(A)=\frac{|A|}{|S|}$ you can see how the concepts are identical.

So for sets $A$, $B$, and $C$: $$
P(A\cup B\cup C)=P(A)+P(B)+P(C)-P(A\cap B)-P(A\cap C)-P(B\cap C)+P(A\cap B\cap C)
$$
### Disjoint Events
Mutually disjoint, or mutually exclusive, events are events which cannot happen at the same time.

If $E_1,...,E_n$ are mutually disjoint then$$E_i\cap E_j=\emptyset \text { whenever } i\neq j, 1\leq i \leq n,\text{ and }1\leq i \leq n$$$$P(\bigcup_{1\leq i\leq n} E_i)=\sum_{1\leq i\leq n}P(E_i)$$
### Three Dice Example
 Consider the following problem, which was posed earlier:

"Suppose that I roll a fair die three times. Then
- $S$ is the sequences of length three over $\{1,...,6\}$, or $\{1,...,6\}^3$
- $P(x)=\frac{1}{6^3}=\frac{1}{216}$

What is the probability that I roll at least one six?"

We can actually compute this probability a couple different ways. The first is to use the formula for the union of three sets stated above.

The event $E$ we are concerned with is the same as the union of the following events:
- $E_1:$ event that the 1st roll is a 6 
- $E_2:$ event that the 2nd roll is a 6
- $E_3:$ event that the 3rd roll is a 6

So to calculate this we need to find the following probabilities:
- $P(E_1)=\frac{1}{6}=\frac{36}{216}$
- $P(E_2)=\frac{1}{6}=\frac{36}{216}$
- $P(E_3)=\frac{1}{6}=\frac{36}{216}$
- $P(E_1\cap E_2)=\frac{1}{6}\times\frac{1}{6}=\frac{6}{216}$
- $P(E_1\cap E_3)=\frac{1}{6}\times\frac{1}{6}=\frac{6}{216}$
- $P(E_2\cap E_3)=\frac{1}{6}\times\frac{1}{6}=\frac{6}{216}$
- $P(E_1\cap E_2\cap E_3)=\frac{1}{6}\times\frac{1}{6}\times\frac{1}{6}=\frac{1}{216}$

Plugging this into our formula we get $$P(E)=P(E_1\cup E_2\cup E_3)=\frac{36}{216}+\frac{36}{216}+\frac{36}{216}-\frac{6}{216}-\frac{6}{216}-\frac{6}{216}+\frac{1}{216}=\frac{91}{216}$$
And so we know that $P(E)=\frac{91}{216}$.

The other method involves computing the probability of the complement of $E$, $\lnot E$.

Since $E$ is the probability of rolling at least one six, $\lnot E$ is the probability of rolling no sixes. $P(\lnot E)$ is the same as $\frac{|\{1,...,5\}^3|}{\{|1,...,6\}^3|}$. This is because $|\{1,...,5\}^3|$ is the number of sequences of length 3 that contain no 6, and $|\{1,...,6\}^n|$ is the total number of sequences of length 3.

Since $|\{1,...,5\}^3|=125$, and $P(E)=1-P(\lnot E)$ we know that $P(E) = 1 - \frac{125}{216}$ and therefore $P(E)=\frac{91}{216}$