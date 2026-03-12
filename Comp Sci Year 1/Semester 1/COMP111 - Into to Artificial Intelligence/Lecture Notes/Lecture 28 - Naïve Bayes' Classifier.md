## Supervised Learning of Classifiers
When given:
- A set $X$ of possible instances to be classified (emails, hand-written digits, image windows, etc.)
- A finite set $Y$ of classes ({spam, not-spam}, etc.)
- Training data $(x_1, L(x_1)),...,(x_n,L(x_n))\in X\times Y$, where $L(x_i)$ is the label of $x_i$
- A class of function $F$ from $X\to Y$ from which the classifier $f$ is selected.

Our aim is compute classifier $f\in F$ such that $$f(x_i)\approx L(x_i)$$for all training data $(x_i,L(x_i))$ so that for new $x\in X$ $$f(x)=y$$is a good prediction for the class of $x$.

The important thing to recognize that we are only aiming for a prediction, this means that if we have a random variable $Z$ that takes values in $Y$, which we can think about as the real class of as the real class of $x$, we simply need to determine if $$P(Z=y|x)\geq P(Z=y'|x)$$for all $y'\in Y$ such that $y\neq y'$.

What this means is that we take the class that is **most** likely to be correct, or in other words the maximally probable hypothesis. 

As that is all we can really do, the question becomes "How do we determine the most likely class given $x$?"

We make the assumption of our training data that each $x\in X$ is given by values $e_1,...,e_n$ of features $E_1,...,E_n$. We model these features as random variables as well. This means that $$P(Z\;|\;x)=P(Z\;|\;E_1=e_1,...,E_n=e_n)$$and that our training data takes the form$$(e_1^1,...,e_n^1),...,(e_1^m,...,e_n^m)$$
For example, consider an agent who has the task of predicting whether Peter plays tennis on a particular day. Our agent knows:
- The weather on the day in question.
- How the weather was on previous days, and whether Peter played tennis on each day (our training data).

The weather is represented as a list of features:
- $outlook$ - with values $sunny$, $overcast$, and $rainy$
- $temp$ - with values $hot$, $mild$, $cool$
- $humidity$ - with values $high$, $normal$
- $wind$ - with values $weak$, $strong$

Our training data can then be represented as the table below:
![[tennis_training.png]]

And then the day on which we want to predict whether Peter will play tennis can be given by the following features:
- $outlook=sunny$
- $temp=cool$
- $humidity=high$
- $wind=strong$

We will go over a way to generate a classifier for this data. From now on when we write $$P(sunny\;|\;Yes)$$it stands for $$P(outlook=sunny\;|\;PlaysTennis=Yes)$$
### Naïve Bayes Classifier
We want to determine if $$P(Z=y\;|\;E_1=e_1,...,E_n=e_n)$$is maximal. In our example this is $$P(Yes\;|\;sunny,cool,high,strong)$$The problem is that no days exist on which the outlook is sunny, the temperature is cool, the humidity is high, and the wind is strong. So how can we estimate this?

We know, by Bayes' Theorem, that $$
P(Z=z\;|\;E_1=e_1,...,E_n=e_n) = \frac{P(E_1=e_1,...,E_n=e_n)P(Z=y)}{P(E_1=e_1,...,E_n=e_n)}
$$
Since we are only comparing we can ignore the denominator and estimate$$
P(E_1=e_1,...,E_n=e_n)P(Z=y)
$$for all $y\in Y$. This is something we can calculate using the training data, given one extra assumption which we will cover in a bit.

So in our example, we want to estimate $$P(sunny,cool,high,strong\;|\;Yes)P(Yes)$$and$$P(sunny,cool,high,strong\;|\;No)P(No)$$
We can estimate $P(Yes)$ by diving the number of days on which peter plays tennis by the total number of days and we can estimate $P(No)$ by dividing the total number of days on which Peter does not play tennis by the total number of days.

However as there are no entries for days on which the outlook is sunny, the temperature is cool, the humidity is high, and the wind is strong, how can we estimate $P(sunny,cool,high,strong\;|\;Yes)P(Yes)$?

In order to estimate this, we must assume conditional independence. This is way we call this the "Naïve Bayes' Classifier", since this assumption clearly is not true for many sets of training data, however it still offers reasonably powerful results.

This assumption allows us to estimate$$P(sunny,cool,high,strong\;|\;Yes)P(Yes)$$by calculating $$V_{Yes}=P(sunny\;|\;Yes)P(cool\;|\;Yes)P(high\;|\;Yes)P(strong\;|\;Yes)P(Yes)$$and estimate $$P(sunny,cool,high,strong\;|\;No)P(No)$$by calculate$$V_{No}=P(sunny\;|\;No)P(cool\;|\;No)P(high\;|\;No)P(strong\;|\;No)P(No)$$
Comparing $V_{Yes}$ and $V_{No}$ allows us to decide which is more likely, $Yes$ or $No$.

We can estimate probabilities like $P(sunny\;|\; Yes)$ by dividing the number of days on which Peter plays tennis and it's sunny by the total number of days on which peter plays tennis.

Using the training data we can calculate:
- $P(Yes)=\frac9{14}$
- $P(sunny|Yes)=\frac29$
- $P(cool|Yes)=\frac39$
- $P(high|Yes)=\frac39$
- $P(strong|Yes)=\frac39$

Which allows us to calculate $$
\begin{equation}
\begin{split}
V_{yes} 
& = \frac29 \times \frac39 \times \frac39 \times\frac39 \times \frac{9}{14} \\
& = \frac{1}{189} \\
& = 0.0053
\end{split}
\end{equation}
$$
We can also calculate:
- $P(No)=\frac5{14}$
- $P(sunny|No)=\frac45$
- $P(cool|No)=\frac15$
- $P(high|No)=\frac45$
- $P(strong|No)=\frac35$

Which allows us to calculate $$\begin{equation}
\begin{split}
V_{No} 
& = \frac45 \times \frac15 \times \frac45 \times\frac35 \times \frac{5}{14} \\
& = \frac{24}{875} \\
& = 0.0274
\end{split}
\end{equation}$$
And so our **Naïve Bayes' Classifier** predicts that Peter will not play tennis.

>Note that the actual $P(Yes\;|\;sunny,cool,high,strong)$ and $P(No\;|\;sunny,cool,high,strong)$ would have to sum to 1. 
>
>Since we haven't got a way to find $P(sunny,cool,high,strong)$ we don't normalise $V_{yes}$ and $V_{no}$ by dividing by it. This is fine, since all we want to do is compare them but it does cause them to much smaller than the actual probabilities.
### General Formula
Suppose we want to predict the class of the instance with features $(e_1,...,e_n)$.

We assume $E_1,...,E_n$ are independent given $Z$ and estimate $$
V_y=P(Z=y)\prod_{i=1}^nP(E_i=e_i\;|\;Z=y)
$$for all $y\in Y$ as follows:
- We estimate $P(Z=y)$ by dividing the number of instances labelled with $y$ in the training data by the total number of instances.
- We estimate $P(E_i=e_i\;|\;Z=y)$ by dividing the number of instances with feature $e_i$ labelled as $y$ by the number of instances labelled with $y$ in the training data.

We then set $$f(e_1,...,e_n)=y$$for the $y$ for which $V_y$ is maximal.

### Spam Filter Example
We want to learn a classifier$$f : \{emails\} → \{\text{spam, not spam}\}$$And so in this case $$X=\{emails\},\;\; Y=\{\text{spam, not spam}\}$$
We have training data $$
(email_1,spam),(email_2, not\; spam), . . .
$$
We can represent every email $x$ by the words from the English dictionary that occur in it. Assuming the English dictionary has 50,000 words and we have an enumeration of these words, we introduce random variables $E_1,...,E_{50,000}$ which take values $\{0,1\}$ with 0 indicating that a given word is not in the email, and 1 indicating that it appears.

The email $x$ we want to classify is then given by the sequence $$x=e_1 ... e_{50,000}\in \{0,1\}^{50,000}$$ stating which words occur in $x$.

To estimate $$V_{Yes} = P(Spam = 1) \prod_{i=1}^{50000}P(E_i = e_i | Spam = 1) $$and$$V_{No} = P(Spam = 0) \prod_{i=1}^{50000}P(E_i = e_i | Spam = 0) $$we estimate:
- $P(Spam = 1)$ by dividing the total number of emails in the training data by the number of spam emails;
- $P(E_i = 1 | Spam = 1)$ by dividing the number of spam emails containing the word number $i$ by the number of spam emails.
- $P(Ei = 0 | Spam = 0)$ by dividing the number of non-spam emails containing the word number $i$ by the number of non-spam emails. 

We then classify the email as spam if $V_{Yes} ≥ V_{No}$.

### Summary
- The "Naïve Bayes' Classifier" is a supervised learning algorithm based on Bayes' Theorem. 
- We call it naïve because we assume that all the features are independent of each other given the classification. 
- This works surprisingly well in practice even if the features are obviously not independent given the classification.