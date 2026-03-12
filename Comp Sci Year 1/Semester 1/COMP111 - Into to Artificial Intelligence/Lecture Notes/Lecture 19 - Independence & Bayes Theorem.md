## Independence
In normal language, if we talk about events as being independent, we are talking about events that don't affect each other. In probability theory, when we say independent, we mean something very similar.

Two events, $A$ and $B$, are independent if, and only if$$P(A\cap B)=P(A)\times P(B)$$
Also if they are independent and $P(A)\neq 0$ and $P(B)\neq 0$ then we know:
- $P(B)=P(B|A)$
- $P(A)=P(A|B)$

If you recall that $$P(A|B)=\frac{P(A\cap B)}{P(B)}$$
You can see that if we rearrange $P(A\cap B)=P(A)\times P(B)$ to get either $A$ or $B$ we can see that clearly.
## Examples
The following examples use rules established in [[Lecture 17 - Computing Event Probabilities]], and [[Lecture 18 - Conditional Probability]].
### Example 1
Problem "Consider the following probability space $(S,P)$ with$$S=\{red, green, yellow, black\}$$and$$P(red)=0.1,P(green)=0.2,P(yellow)=0.2,P(black)=0.5$$
1. What is $P(\{red, green\})$
2. What is $P(\{red\}\cap\{green\})$
3. What is $P(\lnot\{green\})$
4. What is $P(\{red\}|\{green\})$
5. Are $\{red\}$ and $\{green\}$ independent
6. What is $P(\{red\}|\{red, green\})$
7. Are $\{red\}$ and $\{red,green\}$ independent
"

So this example helps illustrate a lot of the concepts we have done so far.

Firstly, question 1 is simple. We are asked to find $P(\{red, green\})$, which is the probability of either red or green happening. To do this, since they are both elementary events, all we need to do is calculate $P(red)+P(green)=0.3$. 

You can think of this as finding $P(\{red\}\cup\{green\})=P(\{red\})+P(\{green\})-P(\{red\}\cap \{green\}$.  Since red and green are both elementary events in this sample space, they cannot happen at the same time. Therefore $P(\{red\}\cap \{green\}$ is 0. This is also the answer question 2.

For question 3, we need to recall our complement rule. Since we know $P(\{green\})=0.2$ we know that $$P(\lnot\{green\})=1-P(green)=1-0.2=0.8$$
For question 4, we use our formula for conditional probability conditioning on green. We already know what $P(\{red\}\cap\{green\})$ is from question 2. Plugging in our probabilities we get $$P(\{red\}|\{green\})=\frac{P(\{red\}\cap\{green\})}{P(\{green\})}=\frac{0}{0.2}=0$$
For question 5, recall that we know that two events $A$ and $B$ are independent if, and only if, $$P(A)\times P(B)=P(A\cap B)$$
If we use this formula, we can check independence $$P(\{red\})\times P(\{green\})=0.1\times 0.2\neq 0 = P(\{red\}\cap \{green\})$$and so we know that $\{red\}$ and $\{green\}$ are not independent.

We can also check by just comparing $P(\{red\}|\{green\})$ and $P(\{red\})$. Since $$P(\{red\})=0.1\neq 0=P(\{red\}|\{green\})$$we know that they're not independent. 

For question 6, we must first find $P(\{red\}\cap \{red, green\})$, since $$\{red\}\cap \{red, green\}=\{red\}$$we know that $$P(\{red\}\cap \{red, green\})=P(\{red\})=0.1$$
Now we can plug this into or formula for conditional probability $$P(\{red\}|\{red, green\})=\frac{P(\{red\}\cap \{red, green\})}{P(\{red, green\})}=\frac{0.1}{0.3}=\frac13$$
For question 7 we need to check using our definition of independence. We can see that $$P(\{red\})=0.1\neq \frac13=P(\{red\}|\{red, green\})$$which means we know that $\{red\}$ and $\{red, green\}$ are not independent. We can also see this as $$P(\{red\})\times P(\{red, green\})=0.1\times 0.3=0.03\neq=0.1=P(\{red\}\cap \{red, green\})$$This also shows us that they are not independent.
### Example 2
Problem "If you roll two dice, then the rolls are independent. So the event $A$ of rolling a 1 with the first die is independent of the event $B$ of rolling a 1 with the second die. So the probability that both of these happen is $$P(A ∩ B) = P(A) × P(B) = \frac16 × \frac16 = \frac1{36}$$ This holds for all $ab ∈ \{1, 2, 3, 4, 5, 6\}^2$ : $$P(ab) = \frac1{36} = P(a) × P(b)$$
- Let $A$ be the event of rolling a 1 with the first die
- Let $C$ be the event of rolling a 1 with the first or second die
- Let $B$ be the event of rolling an even sum

1. Are events $A$ and $B$ independent?
2. Are events $C$ and $B$ independent?"

For this problem we need to work out some probabilities related to these events, we will then check if the events are independent using our definition of independence.

Focusing on question 1, our sample space is small enough that we can define our events explicitly$$A=\{11,12,13,14,15,16\}, P(A)=\frac{6}{36}=\frac16$$$$B=\{11,13,15,22,24,26,31,33,35,42,44,46,51,53,55,62,64,66\}, P(B)=\frac{18}{36}=\frac12$$We can then define $A\cap B$ like so$$A\cap B=\{11,13,15\}$$Which lets us verify $$P(A\cap B)=\frac3{36}=\frac1{12}=\frac16\times\frac12=P(A)\times P(B)$$And so we can conclude that events $A$ and $B$ are independent.

You can understand this intuitively as $B$ contains half the outcomes of $S$. If we know that the first dice is odd (as we do when the first dice is 1), then the chance of $B$ occurring is the same as the chance of the second dice being odd, since the sum of 2 odd numbers is even. This is half, which is the same as the chance of $B$ happening at all.

For question 2 we need to define our event $C$ $$C=\{11,12,13,14,15,16,21,31,41,51,61\},P(C)=\frac{11}{36}$$We can then find $B\cap C$ which is$$B\cap C=\{11,13,15,31,51\}$$So we can verify$$P(B\cap C)=\frac{5}{36}\neq \frac{11}{72}=\frac12\times\frac{11}{36}=P(B)\times P(C)$$and conclude that $B$ and $C$ are **not** independent.
## Independence For More Than Two Events
Consider a finite set of events $A=\{A_1,...,A_n\}$. We call $A$ **pairwise independent** if every pair of events is independent. So for all distinct $k$ and $m$ such that $A_m,A_k\in A$ $$P(A_m\cap A_k)=P(A_m)P(A_k)$$
We call $A$ mutually independent if every event is independent of any intersection of the other events. So for all distinct $k_1,...,k_m$ such that $A_{k_1},...,A_{k_m}\in A$ $$P(A_{k_1})\times ... \times P(A_{k_m})=P(A_{k_1}\cap ... \cap A_{k_m})$$
Mutual independence is the more important of these two notions. Pairwise independence isn't a particularly important one.

It's also important to recognise that **pairwise independence does not imply mutual independence.**

Consider the random experiment of flipping a coin twice. So the probability space $(S,P)$ is given by:
- $S=\{HH,HT,TH,TT\}$
- $P(HH)=P(HT)=P(TH)=P(TT)=\frac14$

If we define the following events:
- $H_1=\{HT,HH\}$, then $P(H_1)=\frac12$
- $H_2=\{HH,TH\}$, then $P(H_2)=\frac12$
- $H*=\{HH,TT\}$, then $P(H*)=\frac12$

We can see that these events are pairwise independent as $$H_1\cap H_2=H_1\cap H*=H_2\cap H*=\{HH\},P(HH)=\frac14=\frac12\times \frac12$$They are not, however, mutually independent. $$P(H_1\cap H_2\cap H*)=P(HH)=\frac14\neq\frac18=P(H_1)P(H_2)P(H*)$$
For an example of events which are mutually independent, consider the random experiment of rolling a dice $n$ times. The probability space $(S,P)$ is given as follows:
- $S=\{1,...,6\}^n$
- $P(x)=\frac1{6^n}$ for all $x\in S$.

Let $E_i$ be the event of getting a 6 the $i^{th}$ time the die is rolled for $1\leq i\leq n$.

We know that $E_1,...,E_n$ are mutually independent since each dice roll is independent from the others.
## Bayes' Theorem
Bayes' theorem states that if $P(A)>0$ then$$P(B|A)=\frac{P(A|B)\times P(B)}{P(A)}$$
We can see this is true because$$P(A\cap B)=P(A|B)P(B),\; P(A\cap B)=P(B|A)P(A)$$which means that $$P(A|B)P(B)=P(B|A)P(A)$$and so by dividing by $P(A)$ we get$$P(B|A)=\frac{P(A|B)\times P(B)}{P(A)}$$
Consider the problem below.

"Assume a patient walks into a doctor’s office complaining of a stiff neck. 

The doctor knows: 
- meningitis may cause a patient to have a stiff neck 50% of the time (causal knowledge); 
- the probability of having meningitis if $\frac1{50000}$
- the probability of having a stiff neck is $\frac1{20}$. 
 
What is the probability that the patient has meningitis?"

Here we can define some events:
- $A$ is the event that the patient has a stiff neck
- $B$ is the event that the patient has meningitis

We want to find out the chance that the patient has meningitis knowing that they have a stiff neck. So we want to calculate $$P(B|A)=\frac{P(B\cap A)}{P(A)}$$The problem is that we don't know what $P(B\cap A)$ is. But we do know:
- $P(B)=\frac1{50000}$
- $P(A)=\frac1{20}$
- $P(A|B)=\frac12$
So we can plug these in to Bayes' formula to calculate $$P(B|A)=\frac{P(A|B)P(B)}{P(A)}=\frac{\frac12\times\frac{1}{50000}}{\frac1{20}}=\frac{1}{5000}$$
And so the doctor can conclude there is a 1 in 5000 chance that this patient has meningitis.
## Alternate Form of Bayes' Theorem
The alternate form of Bayes' theorem states that if $P(A)>0$ then $$
P(B|A)=\frac{P(A|B)\times P(B)}{P(A|B)\times P(B) + P(A|\lnot B)\times P(\lnot B)}$$
Since we already proved Bayes' theorem, to show this all we need to do is show that $$P(A)=P(A|B)\times P(B) + P(A|\lnot B)\times P(\lnot B)$$
Which we can do like so$$P(A)=P((A\cap B)\cup (A\cap\lnot B))=P(A\cap B)+P(A\cap\lnot B)=P(A|B)\times P(B) + P(A|\lnot B)\times P(\lnot B)$$
This form of Bayes' theorem allows us to find $P(B|A)$ when $P(A)$ is not known but $P(A|B)$ and $P(A|\lnot B)$ is known.

For example, consider the problem below:

"If we assume a drug test is:
- Positive for users 99% of the time;
- Negative for non-users 99% of the time

and that 0.5% take the drug, what is the probability that a person whose test is positive takes the drug?"

Here we can define our events:
- $A$ is that the test is positive
- $B$ is that they take the drug

We are trying to calculate $P(B|A)$, and we have been given:
- $P(A|B)=0.99$
- $P(A|\lnot B)=0.01$
- $P(B)=0.005$

First we use the complement rule to recognise that $P(\lnot B)=1-0.005=0.995$.

We can then plug in our values into bayes alternate theorem$$P(B|A)=\frac{P(A|B)\times P(B)}{P(A|B)\times P(B) + P(A|\lnot B)\times P(\lnot B)}=\frac{0.99\times0.995}{0.99\times0.005+0.01\times0.005}=\frac{99}{298}=0.33$$

