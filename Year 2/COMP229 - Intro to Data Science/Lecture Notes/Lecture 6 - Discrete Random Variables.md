## Elementary Events
The **elementary events** of a probability space are events containing only one outcome from the sample space $\Omega$, i.e. the possible outcomes of running the model one time. 

The **event space** $E$ is more interesting. This is often the power set of $\Omega$ since it can account for individual events as well as one of any number of events occurring. 

For example if we take 1 flip of a coin as our model, there are 2 possible outcomes: $\Omega=\{H,T\}$, but the event space is 
$$
E=\{\emptyset, \{H\}, \{T\}, \{H, T\}\}
$$

Where $\emptyset$ is nothing happening and $\{H, T\}$ meaning that the coin lands on either heads or tails.

If we took 3 flips of the coin we would get
$$
Ω = \{HHH, HHT, HTH, HTT, THH, THT, TTH, TTT\},
$$
with the number of possible events in $E$ being $2^8=256$
## Discrete Random Variables
A random variable is simply a function which assigns a real number to each elementary event in the sample space.

When the sample space $\Omega$ is **finite** or **countable** we call the random variable discrete. This is the focus of this lecture.

Formally, a real valued random variable $X$ on a probability space $(\Omega, E, P)$ is a function $X:\Omega\to\mathbb R$.

Now for any number $v\in\mathbb R$, you can define
$$
P(X=v)=P(\{w\in\Omega|X(w)=V\})
$$
We have defined random variables in $\mathbb R$ but they can be in any other space such as $\mathbb N$ or $\mathbb R^2$ etc.

For example if we were flipping a coin with $\Omega=\{H, T\}$ and we wanted to count the number of heads with a random variable $X$ we can encode $X(H)=1$ and $X(T)=0$.

Given a fair coin, we then have:
$$
P(X=1)=0.5=P(X=0)
$$
This gives us more freedom, as now we can compute probabilities such as:
- $P(X<v)$
- $P(X> v)$
- etc.
## Encodings
There are a number of different ways to encode discrete random variables. Here we will go over some of the common ways and their advantages/disadvantages.
### Label Encoding
Label encoding is the simplest way to encode a random variable. It assigns numbers to labels.

The problem is that this is only good for ordinal values, i.e. ones that can be naturally ranked. This is because otherwise values will be ranked as **greater than** or **less than** others where this makes very little sense (e.g green vs black)

![[label_ordinal_encoding.png]]
### One-Hot Encoding
One-hot encoding assigns one variable to each level, in which the outcome being that level gives a value of 1, and being any other level gives a value of 0.

This creates a problem where all the variables sum to one. This creates a perfect dependence between the variables (multicollinearity) which causes multiple issues.

>The exact issues are not explained here, and therefore I assume we don't need to know about this in detail.

![[one-hot_encoding.png]]
### Dummy Encoding
Dummy encoding modifies one-hot encoding by dropping one variable. This level is then represented by 0s in all other variables, and treated as a reference group or base level.

This stops multicollinearity but then means that the level can be mixed up with absent values.
![[dummy_encoding.png]]

### Effect Encoding
Effect encoding modifies dummy encoding by changing the base level to another number, for example -1.

This can limit the problems with the dummy encoding.
![[effect_encoding.png]]
### Choosing an Encoding
In machine learning, one-hot encoding is often used. This is because ML often deals with a different type of "linearity" from linear regression.

In reality, any of these encodings may be suitable, it simply depends on your use case.
## Probability Mass Function
Let a discrete random variable $X$ take only the values
$$
v_1,...,v_n\in\mathbb R
$$
with $P(x=v_i)=p_i$.

This means that $\Omega$ can be divided into into $n$ elementary events $w_i$ where $X(w_i)=v_i$, and the probabilities $p_i=P(X=v_i)$ which can define the **probability mass function (pmf)**
$$
pmf: \Omega\to[0,1]
$$
where $pmf(w_i)=p_i$.

Often $\Omega$ isn't mentioned at all and the discrete random variable will be defined in terms of the pairs
$$
(v_i, p_i)\text{ where } i=1,...,n
$$
which is called a **discrete probability distribution**.

For example using this format we could give a far coin the distribution:
$$
(0,\frac12),(1,\frac12)
$$
## Expectation of a Random Variable
The **expected value** $E(X)$ of a random variable $X$ is essentially the mean of all outcomes of the random variable. Since some outcomes occur more often than others (due to having higher or lower $p_i$) we can find this by summing the outcomes weighted by their probabilities.

Formally 
$$
E(X) = \sum^n_{i=1}p_iv_i
$$

It is essentially the average value of $X$ that we can expect to see over many independent experiments measuring $X$.

Expectation has one important property. **Linearity**. Essentially
$$
E(X+Y)=E(X)+E(Y),\;\;\;E(aX)=aE(X)
$$
for any random variables $X$ and $Y$ and any constant $a$.

This can also be denoted by:
- $EX$
- $E[X]$

The **variance** can also be expressed as a function of expected value
$$
\begin{split}
Var(X)
&=E[(X-E(X))^2] \\
&=E(X^2)-(E(X))^2
\end{split}
$$

This states that variance is the expected value of the squared deviation from the mean.

For example consider the problem below.

"Imagine we had a box with 36 tickets in the box. Drawing 5 of these tickets will give us a prize of £6, while drawing any of the other 31 tickets will give us nothing.

The game costs £1 to play, is it worth it to play?"

We can model this game using a random variable. There are 36 items in the sample space, 5 of the give us £6, while 31 of them lose us £1 so we can set.

$v_1=6$ with $P(v_1)=\frac5{36}$, 

$v_2=-1$ with $P(v_2)=\frac{31}{36}$.

Since we have the variable expressed as:
$$
(6, \frac{5}{36}), (-1,\frac{31}{36})
$$
We can find
$$
\begin{split}
E(X)
&=6\cdot\frac5{36} - 1\cdot \frac{31}{36} \\
&=\frac{30}{36}-\frac{31}{36} \\
&=-\frac1{36}
\end{split}
$$

Since we have gotten a negative expectation, we know that this game will lose us money long term if we play it long enough, and therefore it is not worth playing.
## Cumulative Distribution Function
The **cumulative distribution function** (cdf) of a random variable X is 
$$
F_x(v)=P(X\leq v)
$$

You can see below the difference between a pmf (left) and a cdf (right)
![[pmf_vs_cmf.png]]

## Uniform Discrete Variable
A uniform discrete variable is a discrete random variable in which each outcome is equally likely.

Examples can be:
- Rolling a die
- Flipping a coin
- Choosing a card

The graphs above used to illustrate pdf and cdf both are for a unique random variable with 4 outcomes.
## Bernoulli Distribution
A Bernoulli variable $X$ is defined by 
$$
P(X=1)=p=1-P(X=0)=1-q
$$
where
$$
p\in[0,1]\;\text{and}\;q=1-p
$$
Bernoulli distributions could be uniform:
- E.g. flipping a coin (p=0.5 & q = 0.5)
But they don't have to be
- E.g. choosing a heart from a deck of cards (p=0.25 & q = 0.75)

The pmf of a Bernoulli variable is given by:
$$
f(k)=P(X=k)=\cases{p & if k=1 \\ q & if k=0}
$$
which can also be written as
$$
f(k)=p^k(1-p)^{1-k}
$$
for $k\in\{0,1\}$

The expectation of a Bernoulli variable $X$ is
$$
\begin{split}
E(X) = 1p + 0q = p
\end{split}
$$
## Binomial Distribution
A **binomial variable** $X=B(n, p)$ is the number of successes in a sequence of $n$ independent Bernoulli trials with parameter $p\in[0,1]$.

It's probability mass function is:
$$
f(k)=P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}
$$
for $k=0,...,n$.

The **binomial coefficient** is 
$$
\binom{n}{k}=\frac{n!}{k!(n-k)!}
$$
which is where this distribution gets it's name from.

Since expectation satisfies linearity, and the expectation of a Bernoulli variable is $p$, we know that the expectation of a binomial variable $X$ is
$$
E(X) = np
$$

You can see some example pmfs and cdfs below. 
![[binomial_pmf_cdf.png]]

## Closing Problem
"How much would you pay to play this game, if you can play as many times as you like? 

You keep flipping a fair coin until the first head, and then the game is over. If you are lucky on the n-th flip, you win £${2^n}$ . (For example, if you get a tail on the 1st flip and a head on the 2nd, you win £4.)"

To find this we need to find the expectation of this variable $X$. First we need to encode it. If we encode the number of flips until head as the amount you win you get we get an encoding of
$$
X(n)=2^n
$$
for all $n\in\mathbb N$

To take the expectation of this we take
$$
E(X)=\sum^{\infty}_{i=1}2^i
$$
Since this diverges, it will be greater than any finite amount we pay to play. Therefore this game is worth paying at literally any price.

