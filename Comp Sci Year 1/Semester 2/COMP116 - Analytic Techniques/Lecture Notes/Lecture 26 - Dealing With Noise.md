## Noisy Channel Model
Consider the figure below:
![[noisy_channel_model.png]]

This shows a model of how information is transferred. The goal of transferring information is that the information sent by the source $U$ is the same as the information received at the destination $Z$.

In practice this is not always the case
- Bit's can get corrupted as they are transferred over the internet
- You may mishear someone because you're speaking in a loud restaurant
Both of these things cause $U\neq Z$.

The "Noisy Channel" in the middle captures this difference, but just modelling it isn't enough by itself. We still need to be able to transmit information accurately, so how can we get around this "noisy channel"?

## Binary Symmetric Channel
Consider the same figure above again
![[noisy_channel_model.png]]
Lets assume $U=X$ and $Y=Z$.

Let's say $U$ is a message made up of $m$ bits. Now suppose that the noisy channel has a chance to flip each bit of the message it receives with probability $q$. This means that there is a $1-q$ probability that each bit message transmits correctly. Let's also assume that sending sequential bits correctly are independent events.

Now, if we send a message with $m$ bits we expect $mq$ errors. For our message to be correct that would mean there are no errors at all. Meaning it must be correct every single time. Therefore
$$
P(correct)=(1-q)^m
$$
So now let's assume there is a $q=0.01$ (very small). From this we can see that, for a message of 50 bits (very small),
$$
\begin{split}
P(correct)
&=(1-0.01)^{50} \\
&=0.99^{50} \\
&\approx0.61
\end{split}
$$
So even when we have a very small chance of error, and only a 50 bit message, the chance of it getting there correctly is only 61%, which is really big.

If you increase $q$ to $0.1$, the chance drops to about a 0.5% chance of transmitting 50 symbols correctly.

This is obviously not acceptable, so how can we increase $P(correct)$?
## Introducing Redundancy
Imagine now, that instead of $X=U$ we use $X=enc(U)$, where $enc(U)$ is a function which repeats the value of each bit of $U$ $x$ times. This results in a message of length $n=xm$ being sent instead.

For example if we take $U=101$ and $x=3$ then
$$
enc(U)=111000111
$$

Now instead of $Z=Y$ we use $Z=dec(Y)$ where $dec(Y)$ is a function where the $i^{th}$ bit is the majority of the $x$ bits $\{y_{xi},y_{xi+1},...,y_{xi+x-1}\}$.

For example for $Y=101010110$ and $x=3$ then
$$
dec(Y)=101
$$
since 1 is the majority of $101$, 0 is the majority of $010$, and $1$ is the majority of $110$.

You can probably already see the benefit of this. Using $x=3$,  If $U=101$, then 
$$
X=enc(U)=111000111
$$
Imagine this gets sent through the noisy channel and two bits get flipped resulting in
$$
Y=101010110
$$
Applying $dec$ to $Y$ we get
$$
Z=dec(Y)=101
$$
and so, even though 2 bits were flipped by the noisy channel, we end up with $U=Z$.
### Revisiting Probability
Let's say that the probability of a flip stays the same at $q$.

Now the probability that a bit gets decoded wrong by $dec$ is the same as the probability that $\geq\frac x2$ bits get flipped.

For simplicity we will only consider $x=3$, this means that 
$$
P(error)=3(1-q)^2+q^3
$$
>Olga really skims over how to calculate this, so I am assuming we won't need to calculate something like this in the exam. Thus, I am being lazy and not typesetting it.

Since $q$ is less than 1
$$
3(1-q)^2+q^3 < q
$$
and so our chance of error on a single bit is decreased.

Let's look at our new chances of error for $p=0.1$:
- When $m=1$, $P(correct)=0.9$ for $X=U$ and $P(correct)=0.972$ when using 3 times repetition.
- When $m=50$, $P(correct)=0.005$ for $X=U$ and $P(correct)=0.241$ when using 3 times repetition.

We can see the obvious benefits of this.
### Efficiency-Quality Trade-Off
Transmission depends of the **encode-decode** convention (what $enc(X)$ and $dec(Y)$ actually are). Using $e$ for $enc()$ and $d$ for $dec()$, $(e, d)$ is called a **scheme**.

We measure efficiency by looking at the **Scheme Rate** $R$. This is the ratio of the number input bits $m$, to the number of **transmitted** bits $n$.
$$
R=\frac mn
$$

The goal is to maximise $R$ while also minimising the probability of error.

We looked at two schemes above:
- $X=U$ and $Z=Y$
- (Triple) repetition and majority vote

For the first $m=1$, $n=1$, and so $R=1$. This is perfectly efficient, but doesn't protect against noise.

For the second $m=1$, $n=3$, and so $R=\frac13$. This means only $\frac13$ is the real message, and the rest is used for error correction.

Generally, you want $n>m$ but also for $n$ to be relatively small.
## Redundancy In Natural Language
Similar to how we add redundant bits to protect transmitted data from noise, English (and other languages) already has built in redundancy. Shannon discovered that English is approximately 50% redundant.

For example, at the character level, Q is almost always followed by U, and at the word level hearing "The cat sat on the...", our brains fill in the blank with mat. 

For an example from a different language, in Japanese "arigato gozaimasu" means "thank you very much", but since it's such a commonly used phrase with long words it gets shortened to as little as "ass mass" often, yet people still understand.

This natural redundancy is what allows us to understand garbled text, we've even built games around it like [Mad Gab](https://www.youtube.com/watch?v=1Ds8IbSLe7I&pp=ygUHbWFkIGdhYtIHCQneCgGHKiGM7w%3D%3D).

The rest of the lecture will be spent looking at ways to quantify natural language.
### Zipf's Law
Automated Speech Recognition (ASR) use statistical models to guess what was said. 

The **experimental claim** known as **Zipf's Law** states that: "If you rank words by frequency the $k^{th}$ most common word appears $\frac1k$ times as often as the most common one".

Essentially the most frequent word occurs 5 times as often as the $5^{th}$ most frequent.

This means that a select few words do a lot of heavy lifting for the language, such as "the", "a", "and", etc. This creates the high redundancy base which makes language predictable.
## Predicting Language with N-Grams
To analyse usage frequency of words, we need some kind of **text-corpus**. This would usually be collections some actual written text, like books, posts, poems, etc.

Once we have this, we can use **relative frequencies** of sequences of words as a way to predict or otherwise analyse the text.

An **N-gram** is a sequence $(w_1,...,w_n)$ of $N$ words taken from some **text-corpus**. There may be additional tokens, such as "start sentence" and "end sentence markers", $\{\langle s\rangle,\langle/s\rangle\}$.

Common choices of $N$ are $N=2$ (bigram) and $N=3$ (trigram).

We can use the relative frequency of different words to find the probability that a word will follow a given N-gram.

Essentially
$$
P(W_n|W_{n-N+1}, W_{n-N+2}, ...,W_{n-1})=\frac{\#W_{n-N+1}, W_{n-N+2}, ...,W_{n-1},W_n}{\#W_{n-N+1}, W_{n-N+2}, ...,W_{n-1}}
$$
This looks hefty but is really simple. You simply divide the number of times the sequence
$$
(W_{n-N+1}, W_{n-N+2}, ...,W_{n-1},W_n)
$$
appears by the number of times the sequence
$$
(W_{n-N+1}, W_{n-N+2}, ...,W_{n-1})
$$
appears.

For example take the following sentence: "In the beginning was the Word, and the Word was with God, and the Word was God."

Using this as our text-corpus, we can see the relative frequencies of some N-grams.

For example 
$$
\begin{split}
P(was\; |\; word)
& = \frac{\#word,was}{\#word} \\
& = \frac{2}{3}
\end{split}
$$

So this "model" predicts that "was" will follow "word", $\frac23$ of the time. This is obviously not a great prediction, but it was only built off of one sentence. This short of model would perform much better if given a much larger text-corpus to draw from.


