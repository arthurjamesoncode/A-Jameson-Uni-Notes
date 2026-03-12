## Unproven Statements
The examples we saw at the end of the last lecture were fairly easy to disprove. This is not always the case. Sometimes, finding a proof or counter example is very difficult.

A conjecture is a statement that has been neither proven or disproven, there are some famous examples of conjectures that are considered open problems in mathematics.

For example, take "Goldbach's conjecture". Goldbach's conjecture states that "*Every even integer greater than 2 is the sum of 2 primes*". 

This property holds for all at least all n up to 10$^{17}$. Probably much higher. A counter example has not been found yet, and a proof has not been devised. Something that might be surprising considering how simple the statement is.

An example of a theorem, which remained a conjecture for a long time before someone proved it, is "Fermat's last theorem". This states that "*No three positive integers satisfy the equation a$^n$+b$^n$=c$^n$ for any integer value of n greater than 2*".

This was conjectured in 1637 by Pierre de Fermat, and proved in 1995 by Andrew Wiles.

The proof is here [[http://www.scienzamedia.uniroma2.it/~eal/Wiles-Fermat.pdf]], and is 109 pages long. It is far too complicated for someone just taking COMP109 to understand, but goes to show that relatively simple statements can have proofs that take centuries to actually find.

>What I find personally interesting about this proof is that the theorem itself is not used ever. It's basically useless, but the techniques developed (partially) to prove it have been incredibly useful and opened up whole new mathematical fields.

## More Examples of Direct Proof

**Every integer is rational:**
	*Suppose n $\in$ $\mathbb{Z}$.
	n = $\frac{n}{1}$
	n $\in$ $\mathbb{Z}$ and 1 $\in$ $\mathbb{Z}$.
	Therefore, by the definition of rational, n is rational.*

**The sum of any 2 rational numbers is rational:**
	*Suppose m, n $\in$ $\mathbb{Q}$.
	By definition m = $\frac{a}{b}$, n = $\frac{c}{d}$, where a, b, c, d $\in$ $\mathbb{Z}$.
	m + n = $\frac{a}{b}$ + $\frac{c}{d}$ = $\frac{ad + cb}{bd}$
	Since the product of 2 integers is an integer and the sum of 2 integers is an integer, ab + cd is an integer and bd is an integer.
	Therefore by definition of rational, m + n is rational.*

**The product of any 2 rational numbers is rational:**
	*Suppose m, n $\in$ $\mathbb{Q}$.
	By definition m = $\frac{a}{b}$, n = $\frac{c}{d}$, where a, b, c, d $\in$ $\mathbb{Z}$.
	mn = $\frac{a}{b}$ + $\frac{c}{d}$ = $\frac{ac}{bd}$
	Since the product of 2 integers is an integer ac is an integer and bd is an integer.
	Therefore by definition of rational, mn is rational.*

**The double of a rational number is rational:**
	*Suppose n $\in$ $\mathbb{Q}$.
	By definition n = $\frac{a}{b}$ where a, b $\in$ $\mathbb{Z}$.
	2n = $\frac{2a}{b}$ 
	Since the product of 2 integers is an integer 2a is an integer.
	Therefore by definition of rational, 2n is rational.*
## Proof By Cases
For some problems, there is not a finite about examples we can show to prove it, but there may be a finite number of cases.

For example take the statement "*$\forall$n where n $\in$ $\mathbb{Z}$, n$^2$ + n is even*". We cannot write down every integer and check this statement against all of them, but we can look at 2 distinct cases that every integer falls into. Even and odd.

The way to prove this statement is this:
	*Assume n $\in$ $\mathbb{Z}$,
	Case 1: n is even
		By definition of even n = 2k, where k $\in$ $\mathbb{Z}$.
		n$^2$ + n = (2k)$^2$+2k = 4k$^2$ + 2k = 2(2k$^2$ + k)
		Since the sum of any 2 integers is an integer and the product of any 2 integers is an integer 2k$^2$ + k must be an integer.
		Therefore by definition of even, n$^2$ + n must be even.
	Case 2: n is odd
		By definition of odd n = 2k + 1, where k $\in$ $\mathbb{Z}$.
		n$^2$ + n = (2k + 1)$^2$+2k + 1 = 4k$^2$ + 4k + 1 + 2k + 1 = 4k$^2$ + 6k + 2 = 2(2k$^2$ + 3k + 1)
		Since the sum of any 2 integers is an integer and the product of any 2 integers is an integer 2k$^2$ + 3k + 1 must be an integer.
		Therefore by definition of even, n$^2$ + n must be even. 
	As all numbers are either even or odd, and in both case n$^2$ + n is even, n$^2$ + n must be even for all integers n.*

This is a combination of generic particulars and case exhaustion.

We saw an example of case exhaustion when we proved that all integers were either even or odd in [[Lecture 3 - Proving Existential Statements]].

>If you had already proved that the sum of 2 even integers is even, that the square of ab even integer is even, that the sum of 2 odd integers is even, and that the square of an odd integer is odd, then you could use these facts to show the truth of each case instead of the way we did it.

When using case exhaustion as part of a proof, you have to be certain that the cases you list are exhaustive. This will usually require its own proof. In this example it is obviously true, and you would not be expected to prove it. Although we did write a formal proof of this, as stated above, in Lecture 3.

As another example take the statement "*The product of any 2 consecutive integers is even*". It can be proved like so:
	*Assume n $\in$ $\mathbb{Z}$,
	Case 1: n is even
		By definition of even n = 2j, where j $\in$ $\mathbb{Z}$.
		n(n + 1) = 2j(2j + 1) = 4j + 2j = 2(2j$^2$ + j)
		Since the product of 2 integers is an integer and the sum of 2 integers is an integer we know that 2j$^2$ + j is an integer.
		Therefore by definition of even, n(n+1) is even. 
	Case 2: n is odd
		By definition of odd n = 2j + 1, where k $\in$ $\mathbb{Z}$.
		n(n + 1) = (2j + 1)(2j + 2) = 4j$^2$ + 6j + 2 = 2(2j$^2$ + 3j + 1)
		Since the product of 2 integers is an integer and the sum of 2 integers is an integer we know that 2j$^2$ + 3j + 1 is an integer.
		Therefore by definition of even, n(n+1) is even.
	As both cases are even and these cases are exhaustive we know that the product of any 2 consecutive integers is even*

You can make this proof a bit more elegant by recognising that 1 of the 2 consecutive integers must be even.

>When done this way you can get the result *2(k(m+1))* and 2(km) for the even and odd cases respectively. Both of these cases show that it is true.

As another example take the statement "*The square of any integer is of the form 3k or 3k + 1*". If we try to solve it using the same cases as above we will get something like this:

*Assume n $\in$ $\mathbb{Z}$,
	Case 1: n is even
		By definition of even n = 2j, where j $\in$ $\mathbb{Z}$.
		n$^2$ = (2j)$^2$ = 4j$^2$
	Case 2: n is odd
		By definition of odd n = 2j + 1, where k $\in$ $\mathbb{Z}$.
		n$^2$ = (2j + 1)$^2$ = 4j$^2$ + 4j + 1

For this proof I am using *j* instead of *k* to avoid confusion as the statement itself uses *k*.

As you can see there isn't really a way to prove the statement when looking at these 2 cases. In order to prove the statement we need to look at a different, but still exhaustive, set of cases.

In order to realise which set of cases you should be using you can write down a bunch of examples:
	*1$^2$ = 1 =3(0) + 1
	2$^2$  = 4 = 3(1) + 1
	3$^2$  = 9 = 3(3)
	4$^2$  = 16 = 3(5) + 1
	5$^2$  = 25 = 3(8) + 1
	6$^2$  = 36 = 3(12)

If it wasn't obvious from the existence of *3k* in the statement, there is some pattern here around multiples of threes, so whey don't we use them as our cases? Instead of using *2k* and *2k + 1*, we can use *3k, 3k + 1,* and *3k+2*. This is exhaustive for same reason that *2k* and *2k + 1* are.

*Assume n $\in$ $\mathbb{Z}$,
	Case 1: n = 3j, where j $\in$ $\mathbb{Z}$.
		n$^2$ = (3j)$^2$ = 9j$^2$ = 3(3j$^2$)
		This is of the form 3k
	Case 2: n = 3j + 1
		n$^2$ = (3k + 1)$^2$ = 3j$^2$ + 6j + 1 = 3(j$^2$ + 2) + 1
		This is of the form 3k + 1
	Case 3: n = 3j + 2
		n$^2$ = (3k + 2)$^2$ = 3j$^2$ + 12j + 4 = 3j$^2$ + 12j + 3 + 1 = 3(j$^2$ + 6 + 1) + 1
		This is of the form 3k + 1
	We can prove these cases are exhaustive like so:
		Let n $\in$ $\mathbb{Z}$, choose m = 3 
		$\exists$ q, r $\in$ $\mathbb{Z}$, such that m = 3q + r, r < 3 and r >= 0
		The only possible values for r are 0, 1, or 2.
		Therefore m = 3q or m = 3q + 1 or m = 3q + 2
		Therefore our list of cases is exhaustive.

This is another case in which its obvious enough that you wouldn't really need to prove that the cases are exhaustive, but its good to anyway.

