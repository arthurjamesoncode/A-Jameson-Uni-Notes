### What are Numbers
Numbers are what we use to count, measure and label. 
- "How many students registered on a course?"
- "What order did people come in a race?"
- etc.

We know many different types of numbers such as:
- $\mathbb{N}=$ The set of all **natural numbers**
- $\mathbb{Z^+}=$ The set of all **positive integers**
- $\mathbb{Z}=$ The set of all **integers**
- $\mathbb{Q}=$ The set of all **rational numbers**
- $\mathbb{R}=$ The set of all **real numbers**

The **natural numbers** are loosely defined as the numbers we use to count, that is $$**\mathbb{N}=\{0,1,2,3,...\}$$0 may or may not be included, but for the purposes of this module, it is included.

If you want a proper definition you need to look to [Peano Axioms](https://en.wikipedia.org/wiki/Peano_axioms). However [Godel's incompleteness theorems](https://en.wikipedia.org/wiki/G%C3%B6del%27s_incompleteness_theorems) state that:
- No consistent system of axioms, whose theorems can be proven by an algorithm, is capable to prove all truths about the arithmetic of natural numbers: there will be statements that are true (or false), but that are unprovable within the system.
- The system cannot demonstrate its own consistency.

Essentially, defining this stuff at the most basic level is extremely difficult, and any system of axioms we do define is inherently incomplete. We don't need to deal with this as part of this module, instead we just use the standard definitions.
  
The **integers** is defined as the set of natural numbers (including 0) and their negations. So$$
\mathbb{Z}=\{\cdot\cdot\cdot,-2,-1,0,1,2,\cdot\cdot\cdot\}$$
The **rational numbers** is defined as the set of all numbers $x$ which can be represented as $$x=\frac{p}{q}$$where $p,q\in\mathbb{Z}$ and $q\neq0$.

>$\in$ means "in" or "is a member of". So $p,q\in\mathbb{Z}$ means that $p$ and $q$ are integers. Notation will not be explained after this. You should be familiar with it from COMP109.

The **real numbers** are any numbers which are used to measure some kind of 1 dimensional quantity.

All of these numbers can be represented by a number line. This is because $\mathbb{R}$ can be represented as an infinite number line, and all the other sets are a subset of $\mathbb{R}$. In fact, each set in this list is a subset of the set following it. Or formally:$$\mathbb{N\subseteq Z^+\subseteq Z \subseteq Q \subseteq R}$$
Lastly we have **irrational numbers** these are all the real numbers which are not rational. Irrational numbers don't have their own symbol and are represented by $\mathbb{R\setminus Q}$.

Examples include:
- $\sqrt{2}$
- $2\sqrt{2}$
- $\sqrt{3}$
- $\sqrt{6}$
- $\pi$
- $e$

You can see a proof that $\sqrt{2}$ is irrational in [[Lecture 7 - Two Classic Results]] from the COMP109 module. The same method can be used to prove the next 3 examples aswell.

Irrational numbers are subset of $\mathbb{R}$ but don't fit into the subset chain shown above. If we represent all numbers as a Venn diagram we can show all numbers like so:
![[all_number_venn.png]]
@
This diagram treats natural numbers as not including 0 and introduces a new concept "Whole Numbers" which is what we call natural numbers on this module. Whole numbers could also just mean integers, so what they mean exactly depends on context, and who is saying it.

**UPDATED** - So now, we know that the definition of **whole numbers** does matter for tests but only if the question makes it clear that it uses the concept. This is, frankly, stupid and unnecessarily confusing and feels like Olga wants to use $\mathbb N=\{0,1,2,...\}$ but also wants to reuse material from the old lecturer who used $\mathbb N=\{1,2,...\}$ and $\mathbb W = \{0,1,2,...\}$.

**UPDATED AGAIN** - She labelled natural numbers as the "Non-negative integer numbers" during the test, so I think we're good to assume that they do include 0, and she understood that she was being too confusing.
## Why Can't We Divide by 0?
In our definition for **rational numbers** we specified that $q\neq 0$, why did we do this?

It is a commonly know fact that you cannot divide by 0. It gives an error on pretty much all calculators and there is not an agreed upon definition of what it could even be.

What we do know is that if we could divide by 0 our whole system of maths would fall apart and every number would collapse into one number. You can see a proof of this below.

We know that $\forall a\in\mathbb{R}$, that $0\cdot a=0$. 

Assume for the sake of contradiction, that we can divide by 0. If this is true then we can rearrange the $0\cdot a = 0$ like so:$$
\begin{split}
0 & = 0 \cdot a \\
\frac00 & = a
\end{split}
$$Since $\forall a\in\mathbb{R},\; 0=0\cdot a$, this would mean that $$\forall a\in\mathbb{R},\; a=\frac00$$This implies that $$1 = \frac00,\; 2=\frac00$$which implies $1=2$. This is obviously a contradiction as we know $1\neq 2$. Therefore we cannot divide by 0. More so than this, this proof shows that every real number becomes indistinguishable if we allow division by 0.
## Properties of Rational Numbers
What happens when we perform operations on rational numbers? 

We know that, $\forall x,y\in\mathbb{Q}$:
- $x + y\in\mathbb{Q}$
- $x-y\in\mathbb{Q}$
- $x\cdot y\in\mathbb{Q}$
- $\frac{x}{y}\in\mathbb{Q}$

You can see proofs for all of these properties below.
### Rational + Rational 
Let $x, y\in\mathbb{Q}$
By definition of rational $x = \frac{a}{b}$ and $y = \frac{c}{d}$ where $a,b,c,d\in\mathbb{Z},\; b\neq0,d\neq0$ $$ 
\begin{split}
x + y 
& = \frac{a}{b} + \frac{c}{d} \\
& = \frac{ad}{bd} + \frac{bc}{bd} \\
& = \frac{ad + bc}{bd}
\end{split}
$$Observe that as $a,b,c,d\in\mathbb{Z}$ it must be the case that $ad+bc\in\mathbb{Z}$ and $bd\in\mathbb{Z}$. Also observe that as $b\neq0$ and $d\neq0$ it must be the case that $bd\neq0$.

Therefore $x+y$ is of the form $\frac{m}{n}$ where $m,n\in\mathbb{Z}$ and $n\neq0$ when $x$ and $y$ are any arbitrary rational number. This proves that the sum of any 2 rational numbers is rational.
### Rational - Rational
As we have just proved that the sum of any two rational numbers is rational, we know that the difference of any two rational numbers is also rational. This is because $a-b=a+(-b)$ and if $b\in\mathbb{Q}$ then $-b\in\mathbb{Q}$ and thus $a-b$ where $a,b\in\mathbb{Q}$ is also the sum of 2 rational numbers.
### Rational $\times$ Rational
Let $x, y\in\mathbb{Q}$
By definition of rational $x = \frac{a}{b}$ and $y = \frac{c}{d}$ where $a,b,c,d\in\mathbb{Z},\; b\neq0,d\neq0$ $$ 
\begin{split}
xy 
& = \frac{a}{b} \times \frac{c}{d} \\
& = \frac{ac}{bd}
\end{split}
$$Observe that as $a,b,c,d\in\mathbb{Z}$ it must be the case that $ac\in\mathbb{Z}$ and $bd\in\mathbb{Z}$. Also observe that as $b\neq0$ and $d\neq0$ it must be the case that $bd\neq0$.

Therefore $xy$ is of the form $\frac{m}{n}$ where $m,n\in\mathbb{Z}$ and $n\neq0$ when $x$ and $y$ are any arbitrary rational number. This proves that the product of any 2 rational numbers is rational.
### Rational / Rational
Let $x, y\in\mathbb{Q}$
By definition of rational $x = \frac{a}{b}$ and $y = \frac{c}{d}$ where $a,b,c,d\in\mathbb{Z},\; y\neq0,b\neq0,d\neq0$.
Observe that as $y\neq0$ it must be that $c\neq0$ $$ 
\begin{split}
\frac{x}{y} 
& = \frac{\frac{a}{b}}{\frac{c}{d}}\\
& = \frac{a}{b} \times \frac{d}{c} \\
& = \frac{ad}{bc}
\end{split}
$$Observe that as $a,b,c,d\in\mathbb{Z}$ it must be the case that $ad\in\mathbb{Z}$ and $bc\in\mathbb{Z}$. Also observe that as $b\neq0$ and $c\neq0$ it must be the case that $bc\neq0$.

Therefore $xy$ is of the form $\frac{m}{n}$ where $m,n\in\mathbb{Z}$ and $n\neq0$ when $x$ and $y$ are any arbitrary rational number. This proves that the division of any 2 rational numbers is rational.
### Properties of Irrational Numbers
What happens when we perform operations on rational numbers? 

We know that, $\forall x,y\in\mathbb{R\setminus Q}$:
- $x + y\in\mathbb{R}$
- $x-y\in\mathbb{R}$
- $x\cdot y\in\mathbb{R}$
- $\frac{x}{y}\in\mathbb{R}$

These results being in the reals, means that the results can be both rational and irrational numbers. You can see examples that prove this below.
### Irrational + Irrational
As we know that $\sqrt{2} + (-\sqrt{2})=0$ we know that the sum of 2 irrational numbers can be rational.

If you want to use an example that does not use a negation, you can use the one below. It does require a proof from a later section of this note.

We know that $1-\sqrt{2}\in\mathbb{R\setminus Q}$ because the difference of a rational number and an irrational number is always irrational (You can see a proof for this below).

Observe that $$\sqrt{2} + 1 - \sqrt{2} = 1$$and therefore we know that the sum of two irrational numbers can be rational.

As we know that $\sqrt{2} + \sqrt{2}=2\sqrt{2}$ we know that the sum of 2 irrational numbers can be irrational.

As we know that $\sqrt{2} + 2\sqrt{2}=3\sqrt{2}$ we know that the sum of 2 distinct irrational numbers can be irrational.
### Irrational - Irrational
We know that $1+\sqrt{2}\in\mathbb{R\setminus Q}$ because the sum of a rational number and an irrational number is always irrational (You can see a proof for this below).

Observe that $$1 + \sqrt{2} -\sqrt{2} = 1$$and therefore we know that the difference of two irrational numbers can be rational.

As we know that $2\sqrt{2}-\sqrt{2}=\sqrt{2}$ we know that the difference of 2 irrational numbers can be irrational.
### Irrational $\times$ Irrational
We know that as $\sqrt{2}\cdot \sqrt{2}=2$ that the product of 2 irrational numbers can be rational. 

We also know that as $\sqrt{2}\cdot 2\sqrt{2}=4$ that the product of 2 distinct irrational numbers can be rational.

We can also see that as $\sqrt2\cdot\sqrt3=\sqrt6$ that the product of 2 irrational numbers can be irrational.
### Irrational / Irrational
We know that as $\frac{\sqrt2}{\sqrt2}=1$ that the division of 2 irrational numbers can be rational.

We know that as $\frac{\sqrt6}{\sqrt3}=\sqrt2$ that the division of 2 irrational numbers can be irrational.
## Interactions of Rationals and Irrationals
What happens when we perform operations using a rational and irrational number.

We know that, $\forall x\in\mathbb{Q},y\in\mathbb{R\setminus Q},x\neq0$:
- $x + y\in\mathbb{R\setminus Q}$
- $x-y\in\mathbb{R\setminus Q}$
- $x\cdot y\in\mathbb{R\setminus Q}$
- $\frac{x}{y}\in\mathbb{R\setminus Q}$

It is worth noting that if $x=0$ then $x\cdot y = 0$ and $\frac{x}{y}=0$.

You can see proofs of these properties below:
### Rational + Irrational
Assume, for the sake of contradiction, that $$
\exists x\in\mathbb{Q}
$$such that $$x=y+z$$where $z\in\mathbb{R\setminus Q},\; y\in\mathbb{Q}$.

As we know $z=x - y$, $x,y\in\mathbb{Q}$, and the difference of any two rational numbers is also rational, it must be the case that $z\in\mathbb{Q}$. This is a contradiction since $z\in\mathbb{R\setminus Q}$.

Therefore the sum of a rational number and an irrational number can not be rational, and must be irrational.
### Rational - Irrational
As shown above the sum of an irrational number and a rational number must be irrational. As $a-b=a+(-b)$ and if $b\in\mathbb{R\setminus Q}$ then $-b\in\mathbb{R\setminus Q}$, the difference of a rational number and an irrational number must also be irrational.
### Rational $\times$ Irrational
Assume, for the sake of contradiction, that $$
\exists x\in\mathbb{Q}
$$such that $$x=yz$$where $x\neq0,z\in\mathbb{R\setminus Q},\; y\in\mathbb{Q}$.

As we know $z=\frac{x}{y}$, $x,y\in\mathbb{Q}$, and the division of any two rational numbers is also rational, it must be the case that $z\in\mathbb{Q}$. This is a contradiction since $z\in\mathbb{R\setminus Q}$.

Therefore the product of a rational number and an irrational number can not be rational, and must be irrational.
### Rational / Irrational
Assume, for the sake of contradiction, that $$
\exists x\in\mathbb{Q}
$$such that $$x=\frac{y}{z}$$where $x\neq0,z\in\mathbb{R\setminus Q},\; y\in\mathbb{Q}$.

As we know $z=\frac{y}{x}$, $x,y\in\mathbb{Q}$, and the division of any two rational numbers is also rational, it must be the case that $z\in\mathbb{Q}$. This is a contradiction since $z\in\mathbb{R\setminus Q}$.

Therefore the division of a rational number by an irrational number can not be rational, and must be irrational.
### Decimal
A decimal is a decimal fraction, i.e. fraction with 10𝑛 in the denominator. Hence they are from $\mathbb{Q}$.

We know that:
- $\forall x\in\mathbb{Q},\; x=$ a terminating OR non-terminating recurring decimal 
- $\forall x\in\mathbb{R\setminus Q},\; x=$ a non-terminating AND non-recurring decimal