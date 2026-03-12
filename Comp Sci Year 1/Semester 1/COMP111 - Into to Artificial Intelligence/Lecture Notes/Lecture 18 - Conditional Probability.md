Often, we are only interested in part of the sample space. Conditional probability gives us a means of handling these cases.
### Normalisation and Conditioning
"Consider a family chosen at random from a set of families with 2 children who are not twins. What is the probability that both children are boys?"

To answer this question we need to define a probability space:
- $S=\{BB,GB,BG,GG\}$
- $\forall x\in S,\; P(x)=\frac{1}{4}$

In this case the chance that they have 2 boys $P(BB)$ is $\frac{1}{4}$.

"You find out that the set of families they were chosen from have at least one child in an all boys school. Now what is the probability that both children are boys?"

If we make a sample space $S'$ for this problem now we get:
- $S'=\{BB,GB,BG\}$

Since $S'\subseteq S$, we can look at $S'$ as an event in $S$.

What we are now looking for is the probability of two boys given that we know there is at least one boy. We can also say that we want the probability of two boys given that we know one of the outcomes in $S'$ is true.

We can denote this as $P(BB\;|\;S')$. The line is read "given". So this is read as $P(BB\; given\; S)$.

To find $P(BB\; |\; S')$ we need to **normalise** the probability. You can think of normalisation as finding the probability of an event, given a different event is the entire sample space.

To normalise, we divide the $P(x)$ by the probability that the given event occurs. In this case we would be dividing $P(BB)$ by $P(S')$. And so $$P(BB)=\frac{P(BB)}{P(S')}=\frac{\frac{1}{4}}{\frac{3}{4}}=\frac{1}{3}$$
Assume we have events $A$ and $B$ from some probability space. If we know $B$ happens, and we want to know the likelihood of $A$ happening, we condition on $B$. Thus we want to know$$P(A\;|\;B)$$ or the probability that $A$ happens given we know that $B$ happens.

This means that we want to know $P(A\cap B)$ as this is the only chance $A$ has to happen since we know that $B$ will happen. Obviously we can't take $P(A\cap B)$ but we need to normalise by dividing the probability by the probability of this new sample space $P(B)$. So we get $$P(A\;|\;B)=\frac{P(A\cap B)}{P(B)}$$
In the first example, since $\{BB\}\subseteq S'$, we know that $P(BB)=P(BB\cap S')$. This is why we could just compute $\frac{P(BB)}{P(S')}$.

And so we get our formula: "Let $A$ and $B$ be events with $P(B)>0$. The conditional probability $P(A\;|\;B)$ is given by $P(A\;|\;B)=\frac{P(A\cap B)}{P(B)}$."

For example consider the following problem:

"I choose a sweet uniformly at random from a jar of 30 sweets. The quantities of the sweets are given by the following table.

|              | red | blue | green |
| ------------ | --- | ---- | ----- |
| **circular** | 2   | 4    | 3     |
| **square**   | 6   | 7    | 8     |
What is the probability that it is red conditioned on that it is circular?"

Here we are looking for the chance that it is red given that it is circular and so we need to calculate $$P(R\;|\;C)=\frac{P(R\cap C)}{P(C)}$$
From the table we know:
- There are $2+4+3=9$ circular sweets, and so $P(C)=\frac{9}{30}$
- There are $2$ red and circular sweets, and so $P(R\cap C)=\frac{2}{30}$

And so the probability that it is red given that it is circular is given by$$P(R\;|\;C)=\frac{P(R\cap C)}{P(C)}=\frac{\frac{2}{30}}{\frac{9}{30}}=\frac{2}{9}$$
## Multiplication Rule
Since the conditional probability $P(A|B)$ of $A$ given $B$ is given by $$
P(A\;|\;B)=\frac{P(A\cap B)}{P(B)}
$$we also know that $$P(A\cap B)=P(A\;|\;B)P(B)$$
This is called the multiplication rule, and you can use it to find the probability of the intersection of 2 events.

It can also be extended to more events for example$$P(A∩B∩C) = P(C | A∩B)P(A∩B) = P(C | A∩B)P(B | A)P(A)$$
Consider the following problem:

"Consider choosing a family from a set of families with just one pair of twins (and thus no other children).

What is the probability P(BB) that both twins are boys?

Recall that twins are either identical (I) or fraternal (F). We know that a third of human twins are identical."

In order to calculate the probability that both twins are boys, we need to consider both the probability that both twins are boys and that they are identical, and the probability that both twins are boys and that they are fraternal.

So we get $$P(BB)=P(I\cap BB)+P(F\cap BB)$$
From the question, we know that $$P(I)=\frac{1}{3},\;P(F)=\frac{2}{3}$$
By the multiplication rule we know:
- $P(I\cap BB)=P(BB\;|\;I)P(I)$
- $P(F\cap BB)=P(BB\;|\;F)P(F)$

We know that if the twins are identical they will both have the same sex, so the sample space given that they are identical $S'_I$ is given by$$S'_I=\{BB,GG\}$$We also know that the sample space given that they are fraternal $S'_F$ should look the same as any other 2 child family, and so is given by$$S'_F=\{BB,BG,GB,GG\}$$
Both of these sample spaces are uniform and so we know that$$P(BB\;|\;I)=\frac{1}{2},\;P(BB\;|\;F)=\frac{1}{4}$$
And so we know $$P(BB)=P(BB\;|\;I)P(I)+P(BB\;|\;F)P(F)=(\frac{1}{2}\times \frac{1}{3})+(\frac{1}{4}\times \frac{2}{3})=\frac16+\frac2{12}=\frac26$$

