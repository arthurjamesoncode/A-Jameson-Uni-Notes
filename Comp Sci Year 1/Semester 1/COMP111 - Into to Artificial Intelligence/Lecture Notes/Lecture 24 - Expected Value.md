## Expected Value
Consider a random variable $F$ with values from the real numbers $x_1, . . . , x_n$.

If we assume $P(F = x_i) = \frac1n$ for all $x_i$ then the **expected value**, or **EV** of $F$ is the average over the possible values $x_1, . . . , x_n$ of $F$: $$\frac{x_1 + · · · + x_n}{n} = x_1\frac1n + · · · + x_n\frac1n = \sum_{i=1}^nx_iP(F = x_i)$$
We denote the $EV$ of $F$ by $E[F]$.

In our example, we are dealing with a uniform probability distribution. If we don't have a uniform distribution, we take a probability weighted average. 

What this means is that instead of multiplying each value $x_i$ by $\frac1n$ we multiply each value by $P(F=x_i)$. This is the same thing we just did except the values of $P(F=x_i)$ are no longer all $\frac1n$.

The general form for the $EV$ formula is $$E[F]= x_1P(F=x_1) + · · · + x_nP(F=x_n) = \sum_{i=1}^nx_iP(F = x_i)$$
We call $E[F]$ the expectation of $F$ or mean of $F$.
### Example 1
Suppose you roll a fair die, and model this with a random variable $F$ which takes the values $$\{1,2,3,4,5,6\}$$
and set $P(F=x)=\frac16$ for all $x\in \{1,2,3,4,5,6\}$.

We can calculate the $EV$ of $F$, $E[F]$, using our formula:$$
\begin{equation}
\begin{split}
E[F] 
& = \sum_{i=1}^6 x_iP(F = x_i) = 1P(F = 1) + 2P(F = 2) + 3P(F = 3) +4P(F = 4) + 5P(F = 5) + 6P(F = 6) \\
& = \frac16 + \frac26 + \frac36 + \frac46 + \frac56 + \frac66 \\
& = \frac72
\end{split}
\end{equation}
$$
In this case using our formula is the same as calculating $$\frac{1+2+3+4+5+6}{6}=\frac{21}{6}=\frac72$$
### Example 2
Problem "Suppose I pay, in pence, the face value of a fair die if it comes up odd and earn the face value if it comes up even. What are my expectations?"

To calculate this we first need to define our random variable. Since we pay when it's odd, and earn when it's even the values of our random variable $F$ are: $$F(1)=-1, F(2)=2,F(3)=(-3),F(4)=F(4),F(5)=-5,F(6)=F(6)$$ and so our random variable $F$ takes the values $\{-1,-3,-5,2,4,6\}$ and $P(F=x)=\frac16$ for all $x\in \{-1,-3,-5,2,4,6\}$.

Now we can calculate $E[F]$ like so:$$
\begin{equation}
\begin{split}
E[F] 
& = \sum_{i=1}^6 x_iP(F = x_i) \\
& = -1P(F = -1) + 2P(F = 2) - 3P(F = -3) +4P(F = 4) - 5P(F = -5) + 6P(F = 6) \\
& = -\frac16 + \frac26 - \frac36 + \frac46 - \frac56 + \frac66 = \frac12
\end{split}
\end{equation}
$$
And so we know that the expected value of this bet is 0.5 pence, meaning that, on average, we will win 0.5p every time we play.

## Another Way to Compute $E[F]$
We don't necessarily need to have a defined probability distribution for our random variable $F$. We can also calculate $E[F]$ directly from a probability space $(S,P)$.

Let $F$ be a random variable from the probability space $(S,P)$. $$E[F]=\sum_{s\in S}F(s)P(s)$$
We can see this is true because, if $F$ takes the values $\{x_1,...,x_n\}$ then$$
\begin{equation}
\begin{split}

\sum_{s\in S}F(s)P(s) & = \sum_{F(s)=x_1}F(s)P(s)+...+\sum_{F(s)=x_n}F(s)P(s) \\ 
& = x_1\times \sum_{F(s)=x_1}P(s) + ... + x_2 \times \sum_{F(s)=x_n}P(s) \\
& = x_1P(F=x_1)+...+x_nP(F=x_n) \\
& = E[F]

\end{split}
\end{equation}
$$
## Linearity of Expectations
Once we know the expected value of a random variable we can see how it is affected by combining it with other variables or repeating it multiple times.

Let $F$ and $G$ be random variables from the same probability space $(S, P)$ and let $λ$ be a real number. 

If we define new random variables $F + G$ and $λF$ by setting: $$
(F+G)(s)=F(s)+G(s),\;\; (\lambda{F})(s)=\lambda{F}(s)
$$Then we know:$$E[F+G]=E[F]+E[G],\;\;E[\lambda F]=\lambda{E}[F]$$
Essentially this means 2 things:
- The EV of adding two random variables together is the same as the sum of their individual EVs
- The EV of repeating a random variable $\lambda$ times is the same as multiplying the EV of that variable by $\lambda$.

We can see a proof of the first claim using the alternate way of computing EV from the last section:$$
\begin{equation}
\begin{split}
E[F+G] & = \sum_{s\in S}(F+G)(s)P(s) \\
       & = \sum_{s\in S}(F(s)P(s)+G(s)P(s)) \\
       & = \sum_{s\in S}(F(s)P(s)+\sum_{s\in S}(G(s)P(s)) \\
       & = E[F]+E[G]

\end{split}
\end{equation}
$$
This intuitively proves the second claim since $2F$ is the same as doing $F+F$.

### Example
Problem "What is the expected value of the random variable $F$ with $F(ab) = a + b$ from $$S = \{1, 2, 3, 4, 5, 6\}^2$$where $P(ab) = \frac1{36}$ for every $ab ∈ S$?"

This is asking about a sample space representing rolling a dice twice.

Since we have $F(ab)=a+b$ we can represent $F(ab)$ as the sum of 2 separate random variables $$F(ab)=F_1(ab)+F_2(ab)$$Where
$$
\begin{equation}
\begin{split}
F_1(ab) & = a, \\ 
F_2(ab) & = b,
\end{split}
\end{equation}
$$
Essentially the value of $F_1$ is the value of rolling the first dice and the value of $F_2$ is the value of rolling the second dice.

We computed the $EV$ of rolling a fair dice earlier, and so we know that $$\begin{equation}
\begin{split}
E[F_1](ab) & = \frac72, \\ 
E[F_2](ab) & = \frac72,
\end{split}
\end{equation}
$$
Using the rule we established above we know that $$
\begin{equation}
\begin{split}
E[F] & = E[F_1+F_2], \\ 
     & = E[F_1]+E[F_2], \\
     & = \frac72 + \frac72 \\
     & = 7
\end{split}
\end{equation}
$$
## EV and Multiplication
EV does **NOT** distribute over multiplication the same way it does over addition.

If $F$ and $G$ are random variables from the same sample space $$
E[F\times G] \text{ does not always equal } E[F]\times E[G]
$$
Consider the sample space $(S,P)$ with $$S=\{H,T\}, P(H)=P(T)=\frac12$$
Now we define define random variables $F_h$ and $F_t$ by setting$$F_h=1,\;\; F_h(T)=0,\;\; F_t(H)=0,\;\;F_t(T)=1$$and define the random variable $F$ by setting $F(s)=F_h(s)\times F_t$.

We can use our formula to find $$
\begin{equation}
\begin{split}
E[F] & = 0 \\
E[F_h] & = \frac12 \\
E[F_t] & = \frac12
\end{split}
\end{equation}
$$and so we know $$E[F]=0\neq\frac14=\frac12\times\frac12=E[F_h]\times E[F_t]$$
### Expectation and Decision Making
Now we'll go through an example of how an agent might make a decision using EV.

"Consider an agent who has to deliver a piece of mail. There is a short way and a long way to deliver it. 
- On the short way, it is more likely that the agent will have an accident. 
- Suppose the agent can get protectors that will not change the probability of an accident but will make one less severe. The protectors are expensive, however. 
- Going the long way reduces the probability of an accident, but takes much longer.

Assume the probability distribution is given by:
- $P(Accident = 1 | WhichWay = short) = 0.2$ 
- $P(Accident = 0 | WhichWay = short) = 0.8$
- $P(Accident = 1 | WhichWay = long) = 0.01$
- $P(Accident = 0 | WhichWay = long) = 0.99$

Problem: the agent has to decide whether to wear protectors and which way to go."

We can model this situation using 
- Two decision variables, $WhichWay$ and $Protector$. The agent gets to choose the value for each decision variable.
- A random variable, $Accident$, which represents whether an accident happens.
- A utility function that gives the utility of every possible outcome.

We have the full probability distribution given since the probability of an accident only depends on the variable $WhichWay$.

The utility of the outcome depends on whether a short or long way is chosen, whether the agent wears protectors, and whether the agent has an accident. We assume the utility values for each combination of variables can be given by the following table. (Ignore the difference in the case of $WhichWay$).
![[utility_table.png]]

Now the agent must choose whether to buy protectors and which way to take. That is choose values $r$, and $s$ such that $$E[Utility\;|\;Protector=r,\;WhichWay=s]$$is maximal.

The agent has 4 possible decisions:
- $WhichWay=short$ and $Protector=1$
- $WhichWay=short$ and $Protector = 0$
- $WhichWay=long$ and $Protector = 1$
-  $WhichWay=long$ and $Protector = 0$

We can compute the expected utility for each combination by multiplying the utility of an outcome by the probability of it happening or not. Like so:$$
\begin{equation}
\begin{split}
E[Utility\; |\; WhichWay = short, Protector = 1] 
& = 35 \times P(Accident = 1\;|\; WhichWay = short) \\ 
& + 95 \times P(Accident = 0\; |\; WhichWay = short) \\
& = 83 \\\\

E[Utility\; |\; WhichWay = long, Protector = 1] 
& = 30 \times P(Accident = 1\;|\; WhichWay = long) \\ 
& + 75 \times P(Accident = 0\; |\; WhichWay = long) \\
& = 74.55 \\\\

E[Utility\; |\; WhichWay = short, Protector = 0] 
& = 3 \times P(Accident = 1\; |\; WhichWay = short) \\ 
& + 100 \times P(Accident = 0\; |\; WhichWay = short) \\
& = 80.6 \\\\

E[Utility\; |\; WhichWay = long, Protector = 0] 
& = 0 \times P(Accident = 1\; | \; WhichWay=long) \\ 
& + 80 \times P(Accident = 0\; | \; WhichWay = long) \\ 
& = 79.2

\end{split}
\end{equation}
$$
As $E[Utility\; |\; WhichWay = short, Protector = 1]$ is maximal, the agent would decide to wear protectors and take the short way.

19-11-25 Finish Slides