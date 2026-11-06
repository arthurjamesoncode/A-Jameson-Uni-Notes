## Bad Targets
Goodhart's Law states that: "When a measure becomes a target, it ceases to be a good measure."

This is known as a [perverse incentive]((https://en.wikipedia.org/wiki/Perverse_incentive) or **the cobra effect** which got it's name from when a bounty for cobra's heads, offered with the incentive of reducing the snake population, led to people cobra farming for money.

Other examples include things like:
- Arrest quotas resulting in bad arrests in policing
- Local bonuses leading to branches of a business stealing each others customers, resulting in a lower overall profit

During the Vietnam war, Robert McNamara, the US Secretary of Defence, decided that enemy body counts would be a good measure of success. This was both evil and wrong. The US eventually had to withdraw.

This is all to say that it is often difficult to find precise ways to measure targets. Meaningful quantitative measures don't always exist, and forcing them can lead to bad conlcusions and worse outcomes.

>The rest of this lecture is mostly a recap lecture for COMP109 and COMP116. As a result it will be very brief and include a lot of links back to them.
## Functions & Relations
A **function** is something which maps values from one set, called the **domain**, to values of another set, called the **co-domain**. This essentially forms a set of ordered pairs, but this is usually described through an equation.

>Revisit [[Lecture 15 - Set Cardinality Continued and Intro to Functions]] and the successive lectures from COMP109 for more detailed notes.

If a function maps every real number, to another real number it is said to have both a domain and co-domain of $\mathbb R$ denoted by
$$
f: \mathbb R\to\mathbb R
$$

Functions only describe relations for which there is a single outcome for any given input.

For example the unit circle defined as
$$
\{(x, y) ∈ \mathbb R^2 : x^2 + y^2 = 1\}
$$
doesn't define a function since for every $x$ value there is 2 $y$ values.

A **relation** is a generalisation of functions that drops the requirement that an input can only map to one output. 

>Revisit [[Lecture 20 - Relations]] and the successive lectures from COMP109 for more detail.

We can denote that two items $x$ and $y$ are related in a number of ways:
- $(x,y)$
- $xRy$
- $x\sim y$

$x$ would be from 1 fixed set and $y$ would be from another. The set could be the same or distinct.

A **surjective** function describes a function for which every item in the co-domain, there is a item in the domain which maps to it.

An **injective** function describes a function for which each item in the co-domain is only mapped to once. 

A **bijective** function is both surjective and bijective. 

For example:
- $2x$ is bijective
- $x^3+3x+1$ is surjective, but not injective
- $\frac1x$ is injective, but not surjective

## Equivalence Relations
Equivalence relations are a specific type of relation that satisfy 3 axioms:
1. **Reflexivity** - Any item $x$ is equivalent to itself
2. **Symmetry** - If an item $x$ is equivalent to $y$ then $y$ is equivalent to $x$
3. **Transitivity** - If an item $x$ is equivalent to $y$ and $y$ is equivalent to $z$ then $x$ is equivalent to $z$

>Revisit [[Lecture 23 - Transitive Closures and Equivalence Relations]] and its successive lectures from COMP109

For example $=$ is an equivalence relation (the most obvious one) because:
1. $x=x$ is always true
2. $x=y\implies y=x$ is always true
3. $x=y \land y=z\implies x=z$ is always true

Another equivalence relation on $\mathbb Z$ is $xRy$ if they are both even or both odd. We know this because
1. Any even number is even, and any odd number is odd.
2. If one number is the even/odd and another is even/odd they are both related to each other.
3. This also satisfies transitivity.

$x<y$ is not an equivalence relation because $x<x$ is false (fails reflexivity).
$x\leq y$ is not an equivalence relation because if $x\leq y$ then $y \leq x$ is false except for $x=y$ (fails symmetry).
$|x-y|\leq 1$ is false because $|2-3|\leq 1$ and $|4-3|\leq 1$ but $|4-2|>1$ (fails transitivity).

There is an example in the slide showing that $\frac23$ of voters preferring $A$ to $B$ and $B$ to $C$, then that does not necessarily mean that $\frac23$ of voters prefer $A$ to $C$. 
![[voting_transitivity.png]]

Hence, this relation fails transitivity.

For any equivalence relation, all objects can be classified into well defined classes that each consist of objects which are pairwise equivalent to each other, called **equivalence classes**.

If you take any object, the equivalence class will be the set of items equivalent to that object.
## Vectors
Fixed vectors are directed lines from a point $A\in\mathbb R^n$ to another point $B\in\mathbb R^n$. These points are represented as lists of $n$ numbers $A=(a_0,...,a_n)$.

They are denoted $\overrightarrow{AB}$, and two fixed $\overrightarrow{AB}$ and $\overrightarrow{CD}$ are considered equivalent if
$$
b_i-a_i = d_i - c_i
$$
For all $0\leq i \leq n$. This is an example of an equivalence relation.

Free vectors represent the equivalence classes for this equivalence relation. 

The corresponding free vector for $\overrightarrow{AB}$ is represented by the list of numbers $n$ numbers
$$
A=(b_0-a_0,...,b_n-a_n)
$$

>Revisit [[Lecture 4 - Vectors and Operations]] and it's successive lectures from COMP116 for more detail.

The length of a fixed vector can be given by varying norms, but the most common is the **Euclidean distance** given by
$$
|AB| = \sqrt{(b_1-a_1)^2,...,(b_n-a_n)^2}
$$

The length of a free vector is called it's magnitude and is calculated in the same way.

The angle $\angle(\vec u, \vec v)$ between free vectors $\vec u$ and $\vec v$ is measured by making them start from the same place and taking the anticlockwise turn from $\vec u$ to $\vec v$. 

Free vectors are called **parallel** or **colinear** if the angle between them is 0 or $\pi$.

## Closing Problem
Problem "Friendship relations (on Facebook or in real life): we write (A, B) if a person A knows a person B. 

Is this an equivalence relation on people?"

No, transitivity is not satisfied. If someone is friends with someone else, it doesn't mean they are friends with all of their friends.



