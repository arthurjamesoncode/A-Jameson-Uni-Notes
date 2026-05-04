## Transmitting Information
Often in computer science we have a need to send data to other people. 

Consider sending an email. We **type** a sequence of characters into a text editor. This information is **stored** before it is sent through a **channel**, like 5G or fibre-optic. When the message arrives at the correct place it is **processed**, and the **content** is extracted. The message would then be displayed on the screen of the receiving party.

There are a number of questions about how we should do this and what will happen:
- How should we encode the characters (in binary)?
- How much time will it take to transfer it through a channel?
- What happens if there is interference?
- etc.

**Information Theory** is the area of computer science which studies questions like this.
## Information Theory
"Information" is technically defined as the reduction of uncertainty. 

Information theory offers solutions that address:
- Defining content and uncertainty in information
- The limits of speed of transfer and data compression
- If data can be reliably sent went there is noise
- What we can do to get correct data reception

The **Shannon Paradigm for Communication** is the origin of Information Theory as a scientific discipline. This paradigm is shown in [C. E. Shannon. A Mathematical Theory of Communication. Bell Systems Technical Journal, 27:379–423,623–656, July, October 1948](https://people.math.harvard.edu/~ctm/home/text/others/shannon/entropy/entropy.pdf).

It outlines the following model: 
![[shanon_pardigm.png]]

A message comes from some **source**, it is **encoded** into something that can be sent over a **channel**, the channel sends the information to the **recipient**. The message received may be different to the one sent because of **noise**. The received message is then **decoded** and finally arrives at it's destination.

As C. E. Shannon puts it: "The fundamental problem of communication is that of reproducing at one point either exactly or approximately a message selected at another point."
### What is Information & Communication
As stated above, information is defined as the reduction of uncertainty. Essentially, every word spoken to you in a conversation reduces the uncertainty of what your conversation partner wants to tell you, and therefore they are transmitting information. 

>There is a difference here from **semantics** which means the meaning of information. We will touch more on this later, but information theory is only concerned with the representation of information as sequences of symbols/tokens. 
>
>The "uncertainty reduced" just refers to the uncertainty about what the next symbol would be, not uncertainty about the **meaning** of what they want to say.

When we communicate, whether over text, speech, written letters, sign-language, etc. The basic units of this language are **words**. A word is just a sequence of **symbols** from some **alphabet**.

So really, communication is the **sending** and **receiving** of information and the **information** is provided as a **sequence of symbols**. This means that, in order to effectively communicate, the receiver must be able to recognise individual symbols in the stream of symbols that are being sent.

When a receiver views a stream of symbols, some will be more common than others and some symbols are quite rare. For example, "E" and "T" are common in English words, while "Z" and "J" are rarer. What this means is that the receiver would be "more surprised" to see "Z" in a stream than "E". 

Similarly, the appearance of some symbols imply a greater chance of the appearance of other symbols. The letter "Q" for example is almost always followed by the letter "U". This means that if a receiver saw the letter "Q" in a stream they would expect the next letter to be "U", and be very surprised if it was not.
## Messages as Sequences of Events
Given an alphabet $S$ of $n$ symbols
$$
S=\{s_1,s_2,...,s_n\}
$$
and the knowledge that a message is a **sequence of symbols** from this alphabet we are left with a couple of questions:
- How do we measure the uncertainty (degree of surprise) of this system?
- How do we encode messages (in binary) with desirable surprise properties? (We will see exactly what this means later)

When receiving a stream of symbols, we may expect to see some symbols frequently and others rarely. If we attach a probability $P_i$ to each symbol $s_i$ where $P_i$ is the chance of $s_i$ appearing in the stream of symbols, we can then understand the stream of symbols as a sequence of random events.

When a receiver sees $s_i$ appear in the stream, **information** has been gained because the receiver is no longer **unsure** about what the next symbol would be, and therefore the **uncertainty** has decreased.
### Probability
We have covered probability in some detail in the COMP111 module. If you want a more detailed refresher I recommend going to [[Lecture 16 - Reasoning Under Uncertainty]] and it's successive lectures.

The basics of probability you need to understand for this course is:
- Any probability $P(x)$ of an event $x$ happening lies in the following range $0 \leq P(x)\leq 1$.
- If $P(x)=1$ then $x$ is certain to happen, and if $P(x)=0$ the event is impossible.
- If events $A$ and $B$ are independent then $P(A\cap B)=P(A)\cdot P(B)$.
- For discrete probability spaces containing events $n$ events $\{e_1, e_2,...,e_n\}$ where $P(e_i)$ is the probability of event $e_i$ happening, it must be the case that one of the events occur. Formally:
$$\sum_{i=1}^nP(e_i)=1$$

>All of the above is relatively simple and has been covered before. There is one thing off of the slides that, while simple, I haven't seen before, and therefore it got more detail than the bullet points.

If $P(x)$ is the probability of event $x$ occurring, then $\frac1{P(x)}$ is the **rarity factor** of $x$. If you think of probability as "how likely" something is to happen then the rarity factor is "how rare" an event is. These two things are inverses of each other.

Rare events **surprise** us more and, as a result, **carry more information** then common ones. The rarity factor assists us is measuring this.
### Reducing Uncertainty/Gaining Information
When we see a specific symbol $s_i$ in a stream of symbols we gain information. 

We call the "information gained by seeing $s_i$" the **self-information** of $s_i$ and we denote it by $I(s_i)$. This is the same as saying the "decrease in uncertainty when $s_i$ is seen", which is denoted by $s_u$.

This is a numeric value which is the same as the number of yes/no questions (or binary bits) which is needed to identify $s_i$. This is the same as $-\log_2P(s_i)$ since $\log_2$ shows us the number of binary questions. We must take the negative since $0< P(s_i)\leq1$, meaning that $\log_2P(s_i)\leq0$.

So formally
$$
u_i=I(s_i)=-\log_2P(s_i)
$$

Note that if $P(s_i)=0$ then $s_i$ can never happen and we can never gain information. Trying to substitute $P(s_i)=0$ into this gives an error as you cannot take the $\log$ of 0, hence the bounds of $0< P(s_i)\leq1$.

On the other hand if $P(s_i)=1$ then $I(s_i)=-\log_2(1)=0$. This means that if an event is **certain** no uncertainty is reduced by seeing it and therefore we gain no information. Although this won't break our formula like impossible events do.
## Source Coding & Deriving Uncertainty
When we send messages electronically, we cannot send the symbols these messages contain directly. We must first **encode** them as binary sequences. There are various standards we use to do this, such as ASCII or UNICODE.

When it comes to the problem of source coding, there are some big questions such as:
- How many bits do we need?
- Is it possible to compress the number of bits, and are there good algorithms to do so?

To determine the number of bits needed we need to consider the **uncertainty of the source**. This is also called the **entropy of the source**. This is derived from the alphabet $S$ (and it's associated probability distribution) which the source communicates with.

For simplicity, we assume that the probability of any symbol appearing is independent of the symbols that came before. In actuality this is obviously false, certain letters and words are more likely to appear together.

The **entropy** of a source using alphabet $S$ is denoted by $H(S)$ and given by the formula
$$
H(S) = -\sum_{i=1}^nP(s_i)\log_2P(s_i)
$$

We now can use the **source coding theorem** to determine the number of bits needed to represent this alphabet.

>You don't need to know the source coding theorem's proof for this module. You just need to know the following property.

The **source coding theorem** states that the **expected length** $L(S)$ is greater than or equal to the entropy of the source. The expected length refers to the **average number of bits** needed to encode a symbol. So formally
$$
L(S) \geq H(S)
$$

>Note that "average number of bits needed to encode a symbol" means the average over a message using the alphabet $S$. Essentially $H(S)\cdot |S|$ is the average amount of bits needed for a message of length $|S|$ and not the total space required to store the coding scheme.  
### Examples
Lets look at the following alphabet which has a uniform probability distribution
$$
S=\{A,B,C,D\}
$$
Since every symbol is equally likely then $P(s_i)=\frac14$.

>Note that in the slides Olga uses decimals to represent the probabilities. If possible, representing them as fractions makes the arithmetic much easier. 
>
>This is especially since you will (probably) be asked to find the $\log_2$ of these probabilities.

This lets us calculate $H(S)$ like so
$$
\begin{split}
H(S) 
&= -\sum_{i=1}^nP(s_i)\log_2P(s_i) \\
&= -4(\frac14\log_2\frac14)\\
&= -\log_2\frac14 \\
&= 2
\end{split}
$$

By the source coding theorem we know that we need (at least) 2 bits for some symbol. We could then encode this as
$$
A=00,\;B=01,\;C=10,\;D=11
$$
Using this encoding, we know that a stream of $n$ characters needs $2n$ bits at minimum to communicate it. The encoding itself is 8 bits long.

What about if the probability distribution **isn't uniform**. Let's take the following distribution as an example:
$$
P(A)=\frac12,\;P(B)=\frac14,\;P(C)=P(D)=\frac18
$$

The alphabet hasn't changed, and so we *could* still use the same number of bits to encode the information, but let's see if we can decrease it a little bit.

First lets recompute the entropy
$$
\begin{split}
H(S) 
&= -\sum_{i=1}^nP(s_i)\log_2P(s_i) \\
&= -\frac12\log_2\frac12-\frac14\log_2\frac14-2(\frac18\log_2\frac18)\\
&= -\frac12\cdot-1-\frac14\cdot-2-\frac14\cdot-3\\
&= \frac12 + \frac12+\frac34 \\
&= 1.75
\end{split}
$$
We know, from the **source coding theorem**, that we can use 1.75 bits on average to represent each symbol in a message from this alphabet.

So how do we compress this? Well we could assign **shorter** bit-strings to the more common symbols and longer bit strings to the more rare symbols. The optimal way to do this is the [Huffman Coding](https://en.wikipedia.org/wiki/Huffman_coding) algorithm. (There is an explanation of this [[Lecture 25 - Information Theory Intro#Huffman Coding Algorithm|below]], but you don't need to understand it fully).

Using this algorithm we can derive the following **coding scheme** for our alphabet:
- $A: 1$
- $B: 01$
- $C: 000$
- $D: 001$

In a message consisting of $104,857,600$ symbols we expect to see:
- $104,857,600/2=52,428,800$ occurrences of $A$
- $104,857,600/4=26,214,400$ occurrences of $B$
- $104,857,600/8=13,107,200$ occurrences of $C$
- $104,857,600/8=13,107,200$ occurrences of $D$

If we multiply these values by the number of bits it takes to encode each symbol and sum the results, we get the expected number of bits needed to store the whole message.

We need:
- $\approx50$ Megabits to store occurrences of $A$
- $\approx50$ Megabits to store occurrences of $B$
- $\approx37.5$ Megabits to store occurrences of $C$
- $\approx37.5$ Megabits to store occurrences of $D$ 

Totalling $\approx175$ Megabits. This is less than $\approx200$ Megabits
### Huffman Coding Algorithm
You don't need to understand the Huffman coding algorithm, but the way it works is actually quite intuitive so I will go over an oversimplified version now. 

It is optimal when all probabilities are powers of two ($\frac12, \frac14$, etc.), so for simplicities sake assume all probabilities are. If this is not the case there are other **entropy coding algorithms** which are more optimal. 

We call the string of bits which represents each symbol the **codeword**, and use $Code(s_i)$ to denote the codeword of $s_i$.

Essentially the numbers of bits to represent $s_i$ is equal to $I(s_i)$. The bits are selected such that no symbol requiring $k$ bits is a prefix of a symbol requiring $>k$ bits. This prefix restriction removes the uncertainty that would come from having codewords of multiple lengths.

In the example above, the number of bits to represent $A$ is
$$
I(A)=-\log_2\frac12=1
$$
$A$ is the only symbol for which the probability is $\frac12$ and so it is the only number which requires 1 bit. As a result, we can choose the highest number from our selection (0 or 1) which is 1.

So 1 maps to $A$.

Now that we have selected $1$ to map to $A$. We look to the outcome with the next highest probability $B$ which has $P(B)=\frac14$. This means the number of bits needed to represent $B$ is
$$
I(B)=-\log_2\frac14=2
$$
In order for us to unambiguously decode a message that uses this alphabet, we must ensure that the codeword for $A$ is not a prefix of the codeword for $B$. 

This means that the codeword for $B$ is restricted to 2 letter bit strings which don't start with 1, and so $Code(B)\in\{00, 01\}$.

Since $B$ is the only symbol for which the probability is $\frac14$, we select the maximum of its possible codewords, and so 01 maps to $B$.

Finally, the number of bits needed to represent $C$ and $D$ is 
$$
I(C)=I(D)=-\log_2\frac18=-3
$$
And so 3 bits are required to represent both $C$ and $D$.

We cannot use a codeword with the prefix 1, or 01 meaning that $Code(C),Code(D)\in\{000,001\}$. There are two symbols and 2 possible codewords, therefore we can assign one codeword to each and we have found the Huffman coding for this alphabet.

The specifics of how this algorithm work are more complicated, but this run through should at least give you an idea of **why** we can use these **variable length codewords**.