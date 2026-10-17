## Recap: Location & Spread
Last lecture we looked over a few different measures of location and spread.

Measures of location include:
- Arithmetic Mean
- Geometric Mean
- Mode
- Median
- Quartiles

Measures of spread include:
- Variance
- Standard Deviation
- Interquartile Range
## Probability Spaces
A probability space is defined as
$$
(\Omega, E, P)
$$
where:
- $\Omega$ is the sample space - The set of all possible mutually exclusive outcomes
- $E$ is the event space - The set of all possible combinations of elementary events
- $P$ is a probability function $P: E\to [0,1]$ which must satisfy **Kolmogorov's axioms**

Kolmogorov's axioms are:
1. Positivity: $P(A) \geq 0\; \forall\; A\in E$ 
2. Something always happens: $P(\Omega)=1$
3. Additivity: The probability of the of 2 mutually exclusive events happening is the sum of their individual probabilities.

Formally additivity can be stated as:
$$
P(\bigsqcup_{n=1}^{+\infty}A_n) = \sum_{n=1}^{+\infty}P(A_n)
$$
The symbol $\bigsqcup$ is the symbol for disjoint union from set theory. It is the same as $\bigcup$ but specifies that it's operands are disjoint.

For example when flipping a fair coin we have the probability space $(\Omega, E, P)$ where
- $\Omega=\{H,T\}$ - All elementary events
- $E=\{\emptyset, \{H\}, \{T\}, \{H,T\}\}$ - This is often the power set of $\Omega$. Each event which contains multiple outcomes should be read as $X$ or $Y$. 
- $P$ is a function defined by $P(\{H\})=0.5$ and $P(\{T\})=0.5$

$E$ contains 4 events:
- $\{H\}$ and $\{T\}$ both just mean the coin lands on the given side
- $\emptyset$ represents impossible events
- $\{H,T\}$ represents either that the coin lands on either $H$ or $T$.

If we were to flip a fair coin twice the probability space would become: 
$$
\begin{split}
\Omega = 
&\{HH,HT,TH,TT\} \\
\\
E = 
& \{∅, \{HH\}, \{HT\}, \{TH\}, \{TT\}, \\
& \{HH, HT\}, \{HH, TH\}, \{HH, TT\}, \\
& \{HT, TH\}, \{HT, TT\}, \{TH, TT\}, \\
& \{HH, HT, TH\}, \{HH, HT, TT\}, \\ 
& \{HH, TH, TT\}, \{HT, TH, TT\}, Ω\} \\
\end{split}
$$
With $P$ given by:
- $P(HH)=\frac14$
- $P(HT)=\frac14$
- $P(TH)=\frac14$
- $P(TT)=\frac14$
## Exclusivity
In **axiom 3** of **Kolmogorov's axioms**, we reference **mutually exclusive** or **disjoint** events. Events are considered mutually exclusive/disjoint if it is impossible for both events to happen simultaneously.

There is also the concept of **complementary events**. These are pairs of events where one of them must happen. For example $A$ and $NOT\; A$ are complementary events, as either $A$ must happen or it wont.

The complement of an event $A$ can be notated in a few ways:
- $\Omega - A$
- $\Omega \setminus A$
- $\bar A$
- $A^C$
- $\lnot A$
These all mean the same thing in relation to probabilities and set theory.

If we use the previous example of flipping a coin we can notice that, since there are only two atomic events, that $\{H\}$ and $\{T\}$ are mutually exclusive and complementary to each other. 
### Claim: $P(\emptyset) = 0$
Consider the event $\emptyset$, this is a part of every $E$ from every probability space and represents impossible events. Similarly we also have the event $\Omega$, which just means that something happened.

Theses events are mutually exclusive, and therefore by axiom 3
$$
P(\Omega\cup\emptyset) = P(\Omega)+P(\emptyset)
$$

Knowing this, that $\Omega\cup\emptyset=\Omega$, and knowing that by axiom 2
$$
P(\Omega) = 1
$$

We know that 
$$
P(\Omega) = 1 + P(\emptyset)
$$
and therefore
$$
P(\emptyset) = 0
$$
### Claim: $P(\lnot A) = 1 - P(A)$
Consider the event $A\subseteq \Omega$.

Notice that $(\Omega - A)\cup A = \Omega$. And that A and $\Omega - A$ are mutually exclusive. 

From this, and from A3 and A2, it follows that 
$$
P(\Omega - A) + P(A)=1
$$
and therefore 
$$
P(\Omega - A) = 1 - P(A)
$$
## The Sum Rule
We saw in Axiom 3 that $P(A\cup B)= P(A)+P(B)$ only for disjoint $A$ and $B$.

So how do we generalise this to any $A$ and $B$.

Well the way to do this is to use the **inclusion exclusion principle**, or, put simply we can simply subtract that probability that both events occur.
$$
P(A\cup B)=P(A)+P(B)-P(A\cap B)
$$

>The inclusion exclusion principle was covered in COMP109 [[Lecture 15 - Set Cardinality Continued and Intro to Functions]]

For example, consider the probability space of flipping a fair coin twice. The probability of getting at least 1 head is given by
$$
\begin{split}
P(Head\geq1)
& = P(\{HH, HT\} \cup \{HH, TH\}) \\
& = P(\{HH, HT\}) + P(\{HH, TH\}) - P(\{HH\}) \\
& = 0.5 + 0.5 - 0.25 \\
& = 0.75
\end{split}
$$
We can also get to this same result via a shortcut that relies on the recognising the complement of at least 1 head is 2 tails.

We know that 
- $P(Head\geq 1) = 1 - P(\{TT\}$
- $P(\{TT\})=0.25$ 

And therefore we can do
$$
P(Head\geq 1) = 1-0.25=0.75
$$
## Independent Events & The Product Rule
Events $A$ and $B$ are called independent if 
$$
P(A\cap B)=P(A)P(B)
$$
To show that events are independent we can show that they satisfy this formula.

This is called the product rule, because it can be used to find $P(A\cap B)$ while assuming that they are independent.

**Can an event be independent of itself?**

Well lets plug this into the formula and find out
$$
\begin{split}
P(A\cap A) & = P(A)^2 \\
P(A) & = P(A)^2 
\end{split}
$$
We can observe that this is only true when:
- $P(A)=1$
- $P(A)= 0$
Therefore an event can be independent of itself, but this is only true when the event is certain or impossible.

**Are mutually exclusive events independent?**

Well by the definition of mutually exclusive events, if $A$ and $B$ are mutually exclusive
$$
P(A\cap B) = P(\emptyset)=0
$$
Which we can now plug into our formula
$$
0 = P(A)P(B)
$$

Observe that this is only true when either:
- $P(A)=0$
- or $P(B) = 0$
Therefore two mutually exclusive events can be independent if 1 or both of them is impossible.
## Mutual and Pairwise Independence
We call a set of events $\{A_1,...,A_n\}$ **pairwise independent** if every pair of events is independent.

Formally
$$
\forall i,j\; \text{ such that } i\neq j,\; P(A_i\cap A_j)=P(A_i)P(A_j)
$$

We call a set of events $A=\{A_1,...,A_n\}$ **mutually independent** if 
$$
P(\bigcap^k_{i=1}B_i) = \prod^k_{i=1}P(B_i)
$$
For every subset $\{B_1,...,B_k\}\subseteq A$

For $n=3$ mutual independence would show that:
$$
\begin{split}
P(A_1\cap A_2)&=P(A_1)P(A_2) \\
P(A_2\cap A_3)&=P(A_2)P(A_3) \\
P(A_1\cap A_3)&=P(A_1)P(A_3) \\
P(A_1\cap A_2 \cap A_3)&=P(A_1)P(A_2)P(A_3)
\end{split}
$$

Any set of mutually independent events must be pairwise independent, but pairwise independence doesn't imply mutual independence.

Look at the image below:
![[independent-rings.png]]

You can observe that:
- The blue ring is completely behind the green ring
- The red ring is completely behind the blue ring
- The green ring is completely behind the red ring
Essentially, no two of these rings are linked (pairwise independent) but the group as a whole is, and therefore they are not mutually independent.

As another example consider the following three possible events that can occur when flipping a fair coin twice:
- $A=\{HH,HT\}$
- $B=\{HH,TH\}$
- $C=\{HH,TT\}$
All events contain 2 atomic events out of a sample space of 4 and therefore they all have probability of $\frac12$.

We can see that any two of these events are independent since they all share 1 possibility
$$
P(A\cap B)=P(A\cap C)=P(A\cap B) = P(\{HH\}) = \frac14
$$
Which satisfies:
$$
\frac14 = \frac12\cdot\frac12
$$

However we can see that this breaks when looking at all three rings.
$$
P(A\cap B\cap C)=P(\{HH\})=\frac14 \neq \frac18 =(\frac12)^3
$$
If we didn't know the outcome but knew that it satisfied any one of these events, the chance of it satisfying the others wouldn't change.

However if we knew whether it satisfied any two of these events we would be able to determine whether the third was satisfied.
## Closing Problem
The lecture closes on the following problem: "What is the minimal number of students we should consider to claim that the probability of finding two students born on the same day of the year is more than 50%?"

I'm going to ignore leap years.

We can rephrase this problem to look for the complement, how many people until the chance that all their birthdays are unique is less than 50%, which we can do through a sequence.

The chance that 1 persons birthday is unique is 1 or $\frac{365}{365}$. 

If we add a second person they can now have any birthday except for the birthday that the first person has. 

We can get the chance that it's unique by multiplying the chance that the first persons birthday was unique with the chance that the second persons is given that theirs is.
$$
2\;People:\frac{365}{365} \cdot \frac{364}{365}=\frac{364}{365}
$$

If we add a third person then there are now 2 unique birthdays which are already taken, so the chance that their birthday is not one of those two is $\frac{363}{365}$. Again we multiply this chance by the chance that the first two is unique
$$
3\; People : \frac{364}{365}\cdot\frac{363}{365}
$$
We can continue this sequence until our result is less than 50%. The first value for which is the answer to our problem.

So the probability that $n$ people all have unique birthdays is given by:
$$
\prod_{k=0}^{n-1}\frac{365-k}{365}
$$
and therefore the probability that at least 2 of $n$ people share a birthday is 
$$
1 - \prod_{k=0}^{n-1}\frac{365-k}{365}
$$
We just need to find the smallest n for which this is greater than 0.5.

Actually computing this is tedious so I just wrote the following program in Haskell which computes it
```haskell
minimum_students :: Float -> Float -> Float
minimum_students p n
  | p < 0.5 = n
  | otherwise = minimum_students new_p (n + 1)
  where
    new_p = p * ((365 - n)/365)
```
When given the initial parameters 1 and 1 this program outputs 23, and so this is our answer.

