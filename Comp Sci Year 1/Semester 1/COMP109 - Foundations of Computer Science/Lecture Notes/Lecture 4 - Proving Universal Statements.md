## Universal Statements:
Most statements to be proven in maths are "Universal Statements". 

These take the form of "*$\forall$x if P(x) then Q(x)".

>$\forall$ means "for all". It is called the universal quantifier. 

An example of this is *"if a and b are integers then 6a$^2$b is even"* which can be written like "*$\forall$ a, b, if a, b $\in$ $\mathbb{Z}$ then 6a$^2$b is even"

We generally refer to *P(x)* as the *Premise* and *Q(x)* as the *Conclusion*.  

>You may have noticed that a lot of the statements that we proved the last time were actually universal statements that contained an existential statement, but they were written in a different way without the $\forall$ quantifier.

## Proving by Example
Some theorems can be proved by examining a relatively small number of examples.

For example the statement *"(n + 1)$^3$ $\geq$ 3$^n$* if *n* is a positive integer with *n* $\leq$ 4" can be proved like so:
	 *let x = (n + 1)$^3$ 
	 when n = 1, x = 8 $\geq$ 3
	 when n = 2, x = 27 $\geq$ 9
	 when n = 3, x = 64 $\geq$ 27
	 when n = 4, x = 125 $\geq$ 64

Since the input to these functions are so restricted we can just compute the values for each possible input and compare.

You can do this with any finite domain, but for larger finite domains it's not practical and for infinite domains it's impossible.
## Generalising from the Generic Particular
Generalising from the generic particular is a fancy way to describe what we have already been doing. 

It is a technique in which we show that for any fixed but arbitrary value some property holds.

For example, take our proof from [[Lecture 2 - Proof Techniques]] for the statement "*The sum of any 2 odd numbers is an even number*":
	*Let n and m be arbitrary odd integers.
	By definition: n = 2k+1, k $\in$ $\mathbb{Z}$, m=2l+1, l $\in$ $\mathbb{Z}$.
	2k + 2l = 2(k + l).
	As k and l are both integers, "k + l" is an integer.
	Therefore, by definition, 2(k+l) is even and so the sum of any 2 arbitrary odd integers is even

In the first line of this proof we write "*let n and m be arbitrary odd integers*" and then we show in the rest of the proof that this statement works for these arbitrary integers and therefore works for any fixed integer that you plug into it.

Here is the step by step method of proving using this technique:
- Express the statement to be proved in the form  “∀x , if P(x ) then Q(x ).”
- Start the proof by supposing x is a particular but arbitrarily chosen element for which the hypothesis P(x) is true. Written as “Suppose P(x).” 
- Show that the conclusion Q(x ) is true by using definitions, previously established results, and the rules for logical inference.

We have done this many times by now, so I'm not going to go through more examples here.
## Disproving by Counter Example
Some universal statements obviously cannot be proven, as they are false. In the case of these statements the easiest way to disprove them is by showing a counter example.

For example, the statement "*For every positive integer n, n$^2$ $\geq$ 2n*" is false and we can show this by providing a counter example of *1*. *1* satisfies the premise, by being a positive integer, but *1$^2$ < 2(1)* so the conclusion does not hold.

You might have noticed from the fact that we can disprove this universal statement with an example that we are actually proving a different existential statement.

Disproving a statement of the form:
	*$\forall$x if P(x) then Q(x)*

Is the same as proving the negation of the statement which has the form:
	*$\exists$x such that P(x) and not Q(x)*

As another example consider the statement "*For all integers m and n, if m$^2$ = n$^2$ then m = n*". We can disprove this with any example where *m = -n*, for example:
	*m = 2, n = -2
	m$^2$ = 4, n$^2$ = 4 but m $\neq$ n.
