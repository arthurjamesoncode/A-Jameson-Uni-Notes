## Basics of Counting
The most basic part of combinatorics comes down to our ability to count more complex spaces, based on individual events.

A quick note to say that "permutations" refer to number of ways something can be chosen when order matters, and "combinations" refer to the number of ways something can be chosen when order does not matter. 

Be careful when applying these rules to make sure they are possible.
## The Product Rule
The product states that: "If there is a sequence of $k$ independent events with $n_1,...,n_k$ possible outcomes then the total number of outcomes for the sequence of $k$ events is $n_1\cdot n_2\;\cdot ... \cdot\; n_k$"

You must be careful to make sure that the events are independent of other in order to use the product rule.

This may start to make more sense as we go through some examples.
#### Problem 1
Problem: "All chairs in a room are labelled with a single digit followed by a lower-case letter. What is the largest number of differently numbered chairs?"

In this problem we are being asked how many total outcomes are there from a series of 2 events. Choosing a digit, and then choosing a lower-case letter.

We know, from the product rule, that the total number of outcomes is the same as the product of the number of outcomes for each event. Since there are 10 digits $(0\to 9)$ and 26 lower-case letters $(a\to z)$, we know, by the product rule, the total number of **combinations** of these outcomes is $10\cdot 26$ or $260$.
#### Problem 2
Problem: "How many different bit strings of length 8 are there?"

In this problem we are being asked how many total outcomes there are from a series of 8 events. Choosing either 1 or 0 eight times.

We know, from the product rule, that the total number of outcomes is the same as the product of the number of outcomes for each event. Since we are choosing from 2 outcomes each time, this is the same as $2\cdot 2\cdot 2\cdot 2\cdot 2\cdot 2\cdot 2\cdot 2$ or $2^8$.

So there are $2^8=256$ possible bit strings of length 8.
#### Problem 3
Problem: "In how many ways can we select 3 students for a prospectus photograph (order matters) from a group of 5?"

We are being asked how many total outcomes are there from series of 3 events. Choosing a student 3 times.

We know, from the product rule, that the total number of outcomes is the same as the product of the number of outcomes for each event, but the difference between this problem and the other problems is that the number of outcomes for each event changes, since they are all drawing from the same group.
- When we select our 1st student, we have 5 possible choices, and so we have 5 outcomes. 
- When we select our 2nd student however, we have 4 possible choices since, we have already chosen 1 student and only have 4 left to choose from. 
- When we select our last student, we only have 3 possible choices since 2 have been chosen already.

So we know that, by the product rule, the total possible **permutations** of 3 of the 5 students is $5\cdot 4\cdot 3=60$.
#### Problem 4
Problem: "How many distinct car licence plates are there consisting of six characters, the first three of which are upper-case letters and the last three of which are digits?"

In this problem we are being asked how many total outcomes there are from a series of 6 events. Choosing an upper case letter 3 times and choosing a digit 3 times.

We know that there are 26 upper case letters and 10 digits so, by the product rule, we know that there are $26\cdot 26\cdot 26\cdot 10\cdot 10\cdot 10=26^3\cdot10^3=17,576,000$ license plates that fit the description.
## Sum Rule
The sum rule states that: "If A and B are disjoint events and there are $n_1$ possible outcomes for event A and $n_2$ possible outcomes for event B then there are $n_1 + n_2$ possible outcomes for the event “either A or B".

Disjoint events, or mutually exclusive events, mean that they can't occur simultaneously. You must be sure that the events you are looking at are disjoint when using the sum rule.

This might start to make more sense if we look at some specific examples.
#### Problem 1
Problem: "How many ways there are to select a male and a female student for a prospectus photograph (order matters) from a group of 2 male and 3 female students?"

This problem is asking us to give the total number of outcomes of a series of 2 events, choosing a male student and choosing a female student.

Since the order matters, we need to look at both the number of outcomes when a male student is chosen first, and when female student is chosen first.

When a male student is chosen first, by the product rule, there are $2\cdot 3$ possible outcomes.
When a female student is chosen first, by the product rule, there are $3\cdot 2$ possible outcomes.

Since it is not possible to choose both a male student first and a female student first these 2 events are disjoint.

Therefore, by the sum rule, we know the total number of outcomes is $2\cdot 3 + 3\cdot 2= 12$.
#### Problem 2
Problem: "How many three-digit numbers begin with 3 or 4?"

We know that a number cannot begin with both 3 and 4 at the same time so these events are disjoint.

The question "How many three-digit numbers begin with $x$" is the same as asking us how many outcomes there are for choosing a digit twice.

Therefore, by the product rule, we know that there are $10\cdot 10=100$ possible three-digit numbers beginning with 3 and there are $10\cdot 10=100$ possible three-digit numbers beginning with 4.

Therefore by the sum rule we know that there are $100+100=200$ three-digit numbers that begin with 3 or 4.
#### Problem 3
Problem: "I wish to take two pieces of fruit with me for lunch. I have three bananas, four apples and two pears. How many ways can I select two pieces of fruit of different type?"

There are 3 ways to select 2 different types of fruit. He either selects a banana and a pear, banana and an apple, or an apple and a pair. He cannot select any of these combinations at the same time so we know these are disjoint events.

To calculate how many ways he can select these fruits we use the product rule:
- Banana & Pear: $3\cdot 2=6$
- Banana & Apple: $3\cdot 4=12$
- Apple & Pear: $4\cdot 2$ = 8

Since these events are disjoint, by the sum rule, we can find the total possible combinations by adding them. So the total number of fruit combinations is $6+12+8=26$.
## Set Theory Parallels
We can understand the product and sum rules through set theory.

Imagine we have a sequence of $k$ independent events and $A_1,...,A_k$ are the sets of outcomes for each event. Any individual sequence of events can be represented by the cartesian product $A_1\times ...\times A_k$. Since $|A_1\times ...\times A_k|=|A_1|\cdot ... \cdot |A_k|$, you can see, through set theory, why the product rule is true.

If $A$ and $B$ are disjoint sets, meaning that $A\cap B=\emptyset$, then $|A\cup B|=|A|+|B|$. So you can see that if 2 events are disjoint the sets of their outcomes are disjoint, and therefore the total number of outcomes must be the same as the number of outcomes of $A$ plus the number of outcomes of $B$.

## Final Example
Problem: "A computer password is a string of 8 characters, where each character is an uppercase letter or a digit. Each password must contain at least one digit.

How many different passwords are there?"

This problem asks something slightly different to the others. It's asking how many possible outcomes of choosing either an uppercase character or a letter 8 times, but you must always choose a digit at least once. That condition is what makes this problem harder,

So first we use the product rule to figure out how many possible passwords there are, ignoring the at least one digit rule. The total is $(26+10)^8=36^8$. 

We also know that all the digits which only contain letters are invalid, and we can use the product rule to figure out how many invalid passwords there are. The total invalids is $26^8$.

So the total number of valid passwords is $36^8-26^8=2,612,282,842,880$


