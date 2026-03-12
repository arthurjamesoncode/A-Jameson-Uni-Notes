## Indirect Proofs Continued
This lecture focus' on 2 more involved examples for proof by contradiction.

Take the statement "There is no greatest prime number". This relies on the definition of prime numbers which is any number that has exactly 2 factors. Since every number has the factors of 1 and itself this means that it is any number $\geq$ 2 which only has factors of it and itself.

An important property to recognise is that any fact that any non prime number has at least 1 distinct prime factor.

We can prove this like so:
	*Assume, for the sake of contradiction, that there exists a greatest prime number n.
	Let $P_1$, $P_2$ , $P_3$ , ... ,  $P_n$ be all the prime numbers where $P_n$ is the greatest prime number.
	Let M = $P_1$ $\cdot$ $P_2$ $\cdot$ $P_3$ $\cdot$ ... $\cdot$ $P_n$ + 1
	Case 1: M is Prime
		If M is Prime there is a contradiction as M > $P_n$
	Case2: M is not Prime
		Some prime number, $P_i$ , must divide M, and so M = $P_i$ $\cdot$ k.
		We know M = $P_{i}$($P_1$ $\cdot$ $P_2$ $\cdot$ ... $\cdot$ $P_{i-1}$ $\cdot$ $P_{i-1}$ $\cdot$ ... $\cdot$ $P_n$) + 1 which is of the form $P_{i}$ $\cdot$ k + 1
		This is a contradiction since M is of the form $P_{i}$ $\cdot$ k + 1, it cannot equal  $P_{i}$ $\cdot$ k.
	These 2 cases are exhaustive and as there is a contradiction in both it means that there cannot be a greatest prime number.

The second statement is "$\sqrt{2}$ is irrational". To prove this statement we need to understand what irrational numbers are.

Real numbers are any numbers used in measuring a one dimensional quantity. They are essentially all the numbers on a number line, including every possible decimal point. 

Rational numbers are numbers that we can express as $\frac{m}{n}$ where *m, n $\in$ $\mathbb{Z}$.*

Irrational numbers are any real numbers that are not rational numbers. So are there any irrational numbers? Yes. The first irrational number discovered was $\sqrt{2}$. One proof for this is:
	*Assume for the sake of contradiction, that $\sqrt{2}$ is rational.
	This means that by definition of rational $\sqrt{2}$ = $\frac{m}{n}$ where m, n $\in$ $\mathbb{Z}$, n $\neq$ 0 and m and n do not share any common factors.
	$\sqrt{2}$ = $\frac{m}{n}$, 2 = $\frac{m^2}{n^2}$, 1 = $\frac{m^2}{2n^2}$, m$^2$ = 2n$^2$
	This means that m$^2$ and therefore also m must be even.
	So m = 2k where k $\in$ $\mathbb{Z}$.
	(2k)$^2$ = 2n$^2$, 4k$^2$ = 2n$^2$, n$^2$ = 2k$^2$. 
	This means that n$^2$ and therefore also n must be even.
	Since m and n are both even this is a contradiction as 2 even numbers share a factor, 2, and the definition of m and n states that they do not share a common factor.
	Therefore $\sqrt{2}$ is irrational.

>Fun fact: Legend says that Pythagoras **murdered** one of his students by drowning him because he discovered the existence of irrational numbers, shattering the belief that all numbers were rational.