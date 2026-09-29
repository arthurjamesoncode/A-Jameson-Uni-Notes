## Another Example
Problem: "How many different 8-character passwords can be obtained by combining 3-letter word, a 4-letter word and a digit? 

(According to [scrabblefinder.com](http://www.scrabblefinder.com) there are 1015 3-letter and 4030 4-letter English words."

Since order matters, we need to separate the possible orders.

Let 3 be 3 letter word, D be digit and 4 be 4 letter word :
- 3,4,D
- 3,D,4
- D,3,4
- D,4,3
- 4,D,3
- 4,3,D

There are 6 permutations of the order in which these things could be combined. Since no two of these orders can be achieved at the same time, these orders must be disjoint events.

The total permutations of any of these orders, by the product rule, $1015\cdot4030\cdot10=40,904,500$, so in order to get the total possible passwords we do $6\cdot40,904,500=245,427,000$
## The Subtraction Rule
The subtraction rule states that: "If there are $n_1$ possible outcomes for event $A$, $n_2$ possible outcomes for event $B$, and $n_3$ of these outcomes are shared between $A$ and $B$ then there are $n_1 + n_2 -n_3$ possible outcomes for the event $A$ or $B$.

If you look back at [[Lecture 14 - The Cardinality of Sets]] and [[Lecture 15 - Set Cardinality Continued and Intro to Functions]], you can see similar formulas for the union of 2 sets. Think about this again parallels set theory.

Let's look at some examples.
### Example
Problem: "How many bit strings of length 8 start with 1 or finish with 00?"

The first part of this problem is to figure out how many bit strings of length 8 start with 1. Since 1 is fixed, we are essentially asking how many ways can we choose between 2 options 7 times, which, by the product rule, is $2^7$. You can think of this as $n_1$ from the rule above.

We can so the same to find out how many bit strings of length 8 end with 00. Now, since 2 spaces are fixed we are seeing how many ways we can choose between 2 options 6 times, which, by the product rule, is $2^6$. This is $n^2$ from the rule above.

Lastly we need to find out how many both start with 1 and end with 00. We again do this with the product rule, but this time 3 spaces are fixed so we just get $2^5$. This is $n_3$ from the rule above.

So to find out the answer here we can just do $2^7+2^6-2^5=160$.
## The Division Rule
The division rule states that: "Given $n$ possible outcomes, if some of the $n$ outcomes are the same and every group of indistinguishable outcomes contains exactly $d$ elements, then there are $\frac{n}{d}$ different outcomes."

This rule is mainly used to separate permutations and combinations.

It should make sense as you go through the example.
### Example
Problem: "How many ways there are to select 3 representatives from a group of 5 students?"

Important to note here that order does not matter.

This can be generalised to there are $n!$ possible permutations of any $n$ objects.

We can find the total number of permutations of 3 students when choosing from 5 by using the product rule. The total permutations of 3 students when choosing from 5 is $5\cdot 4\cdot 3=60$,

If we go from looking at permutations to combinations, we now that many of these 60 outcomes are indistinguishable from each other, due to order not mattering. These groups of indistinguishable outcomes are all the same size, since they are all just the set of permutations for 3 objects.

There are $n!$ possible permutations of any $n$ objects, so these groups must all be of size $3!$ or $6$

So then by the division rule we know there are $\frac{60}{6}=10$ possible combinations of student.

When we did this in [[Lecture 28 - Combinatorics]] we counted each unordered trio **6** times since order didn't matter. Now we are only meant to count them once.
## Sum and Product Notation
Given a sequence of numbers $$
...,a_1,a_2,a_3,...,a_m,a_{m+1},...,a_n,..,
$$
We use the notation: $$\sum_{i=m}^{n}a_i\text{ to represent }a_m+a_{m+1}+...+a_n$$$$\prod_{i=m}^n a_i\text{ to represent } a_m\times a_{m+1}\times...\times a_n$$
For example:$$
\sum_{i=1}^{5}i=1+2+3+4+5=15
$$$$\prod_{i=0}^3 i^2=0^2\times 1^2\times 2^2\times 3^2=0$$
I is just an index, so:$$\sum_{i=1}^{5}i=\sum_{j=1}^{5}j=\sum_{i=k}^{5}k=1+2+3+4+5=15$$
When $m=n$: $$\sum_{i=m}^{n}a_m=a_m$$
For example:$$
\sum_{i=3}^{3}i=3
$$
### Sums and Products Over Sets
We can also use this notation over sets.

If we have a function $f : D\to \mathbb{R}$ with some domain $D$, then for all $S\subseteq D$:$$
\sum_{i\in S}f(i)\text{ denotes the sum of } f(i) \text{ over all }i\in S
$$$$\prod_{i\in S}f(i)\text{ denotes the product of } f(i) \text{ over all }i\in S$$
### The Factorial Function
$\prod_{i=1}^{n}i$ comes up so often that it has a name and its own notation. This is $n$ factorial written as $n!$.

>This has already been mentioned earlier in the note. Most people should have some understanding of what the factorial function is.

For example:
- $5!=1\cdot 2\cdot 3\cdot 4\cdot 5=120$
- $3! = 1\cdot 2\cdot 3=6$
- $1!=1$
- $0!=1$

>Note that $0!$ is 1 by matter of definition.

## Counting $k$-Permutations
A permutation of a set is just an ordering of it's elements.

For example, the permutations of the set $\{1,2,3\}$ are:
- 1,2,3
- 1,3,2
- 2,1,3
- 2,3,1
- 3,1,2
- 3,2,1

By the product rule the number of permutations in an $n$-element set is $n!$, because there are $n$ choices for the first element, then $n-1$ choices and so on.

A selection of $k$ distinct elements of a set, where order matters, is called a $k$-permutation of the set.

To calculate the number of $k$-permutations on an $n$-element set is:$$
P(n,k)=n\times(n-1)\times ... \times (n-(k-1))=\frac{n!}{(n-k)!}
$$
This is the exact formula we were using in [[Lecture 28 - Combinatorics]], just without knowing it.
### Example 1
Problem: "In how many ways can we select 3 students for a prospectus photograph (order matters) from a group of 5?"

Solution:$$
P(5,3)=\frac{5!}{(5-3)!}=\frac{5!}{2!}=5\times4\times3=60
$$
### Example 2
Problem: "How many length-4 sequences of distinct digits are there?"

Solution:$$
P(10,4)=\frac{10!}{(10-4)!}=\frac{10!}{6!}=10\times9\times8\times7=5040
$$
### Example 3:
Problem: "How many four-letter strings can be made with distinct letters from the list *a, g, m, o, p, r*?"

Solution:$$
P(6,4)=\frac{6!}{(6-4)!}=\frac{6!}{2!}=6\times5\times4\times3=360
$$
### Example 4:
Problem "I have a jar with 20 different sweets. Three children come in, and each take one. How many different outcomes are there?"

Solution:$$
P(20,3)=\frac{20!}{(20-3)!}=\frac{20!}{17!}=20\times19\times18=6840
$$
## Counting $k$-combinations
A size-$k$ subset is called a $k$-combination.

To calculate the number of $k$-combinations of a set of size $n$, we use$$
C(n,k)=\frac{n!}{(n-k)!k!}
$$
You should read $C(n,k)$ as $n$ choose $k$. You may also see this notation which means the same thing$$
n\choose k
$$
We can prove this is true as:
- The number of $k$-permutations on the set is $P(n,k)=\frac{n!}{(n-k)!}$
- A $k$-permutation is an ordering of $k$ distinct elements of the set.
- As each size-$k$ subset has $k!$ orderings by the product rule.
- By the division rule $C(n,k)=\frac{P(n,k)}{k!}=\frac{n!}{(n-k)!k!}$.
### Example 1
Problem: "How many size-2 subsets of {1,2,3,4,5} are there?"

Solution:$$
C(5,2)=\frac{5!}{(5-2)!2!}=\frac{5\times4\times3\times2\times1}{(3\times2\times1)\times(2\times 1)}=10
$$
### Example 2
Problem: "How many size-3 subsets of {1,2,3,4,5} are there?"

Solution:$$
C(5,2)=\frac{5!}{(5-3)!2!}=\frac{5\times4\times3\times2\times1}{(2\times1)\times(3\times2\times1)}=10
$$
## Extended Example
Problem: "Twelve people, including Mary and Peter, are candidates to serve on a committee of five. How many different committees are possible? 

Of these how many
1. Contain both Mary and Peter
2. Contain neither Mary nor Peter
3. Contain either Mary or Peter but not both
"

So this is actually 4 questions. 1st the total number of committees which is $$
C(12,5)=\frac{12!}{(12-5)!5!}=792
$$
Next we need to see how many contain both Mary and Peter, we can do this by fixing both Mary and Peters positions and seeing how many ways there are to choose 3 from the remaining 10.

So the number of committees that contain both Mary and Peter is$$
C(10,3)=\frac{10!}{(10-3)!3!}=\frac{10\times9\times8}{3\times2\times1}=120
$$
Next we need to find out how many contain neither Mary nor Peter. If both Mary and Peter are excluded we are still choosing 5 but from 10 instead of 12 this time.

So the number of committees that contain neither Mary nor Peter is$$
C(10,3)=\frac{10!}{(10-5)!5!}=\frac{10\times9\times8\times7\times6}{5\times4\times3\times2\times1}=252
$$
Next we need to find the number of committees that contain either Mary or Peter but not both. We can get the number of committees that contain Mary but not Peter by by choosing 4 more candidates from the remaining 10. We can do the same to find out the number of committees that contain Peter but not Mary. Since these 2 sets are disjoint, we can add them together to get the total. 

So the number of committees containing Mary or Peter but not both is$$
2\times C(10,4)=2\times\frac{10!}{(10-4)!4!}=2\times\frac{10\times9\times8\times7}{4\times3\times2\times1}=2\times 210 = 420
$$
