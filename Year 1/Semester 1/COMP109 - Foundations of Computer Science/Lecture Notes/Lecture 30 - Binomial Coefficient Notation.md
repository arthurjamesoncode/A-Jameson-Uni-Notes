The quantity $C(n,k)$, which gives the number of $k$-combinations of a set of size $n$, is called a binomial coefficient.

It is written as $$
\binom{n}{k}=\frac{n!}{k!(n-k)!}
$$
Mathematicians prefer this notation over $C(n,k)$.
## The Binomial Theorem
The binomial theorem states that:$$
\forall n\in\mathbb{N},\;(a+b)^n=\sum_{k=0}^{n}\binom{n}{k}a^{k}b^{n-k}
$$
This might be confusing at first but if I run through an example you may understand.

Take $(a+b)^3$. Lets compute $\sum_{k=0}^{n}\binom{n}{k}a^{k}b^{n-k}$ for $n=3$:
- Before anything else, lets define a running sum, which we'll call $S$, and set $S=0$. 
- First, when $k=0$ we calculate $\binom{3}{0}$, which is $\frac{3!}{0!(3-0)!}=\frac{3!}{3!}=1$
- We now know that the value when $k=0$ is $1a^0b^{3-0}$ or just $b^3$
- Adding it to our running sum we get $S=b^3$
- Next when $k=1$ we calculate $\binom{3}{1}$, which is $\frac{3!}{1!(3-1)!}=\frac{3!}{2!}=3$
- We now know that the value when $k=1$ is $3a^{1}b^{3-1}$ or $3ab^2$.
- Adding it to our running sum we get $S=b^3+3ab^2$
- Next when $k=2$ we calculate $\binom{3}{2}$, which is $\frac{3!}{2!(3-2)!}=\frac{3!}{2!}=3$
- We now know that the value when $k=2$ is $3a^{2}b^{3-2}$ or $3a^2b$
- Adding it to our running sum we get $S=b^3+3ab^2+3a^2b$
- Finally when $k=3$ we calculate $\binom{3}{3}$, which is $\frac{3!}{3!(3-3)!}=\frac{3!}{3!}=1$
- We now know that the value when $k=3$ is $1a^{3}b^{3-3}$ or $a^3$
- Adding it to our running sum we get $S=b^3+3ab^2+3a^2b+a^3$

You can compute $(a+b)^3$ a different way and you can see that this method does in fact work.

This is why $\binom{n}{k}$ is called the binomial coefficient notation, because it gives us a binomial coefficient.

It works because if $$
(a+b)^n=(a+b)_1\times(a+b)_2\times ... \times (a+b)_n
$$
then $\binom{3}{2}$ sees how many ways there are to choose $a$ twice out of 3 brackets.
## Pascal's Triangle
Below is an image of pascal's triangle.
![[pascals triangle.png]]
As you can see the numbers in the non-edge spaces are gotten by adding together the 2 numbers above it that it sits between.

As you can see, by the equations to its left that the values that pascals triangle creates, are the same as the binomial coefficients.

### Binomial Coefficient Identity
The binomial coefficient identity states that: $$
\binom{n+1}{r+1}=\binom{n}{r}+\binom{n}{r+1}
$$
We can prove this like so:
	Observe that $\binom{n+1}{r+1}$ is the number of ways to choose a subset of size $r+1$ from a set of size $n+1$.
	Suppose the set is $\{x_1,x_2,...,x_n,x_{n+1}\}$
	To find out how many subsets of size $r+1$ include $x_{n+1}$ we can choose a subset of size-r from $\{x_1,x_2,...,x_n\}$, so there are $\binom{n}{r}$ subsets of size $r+1$ that include $x_{n+1}$.
	Next we need to find out how many subsets of size $r+1$ exclude $x_{n+1}$.
	To do this we can just choose a size $r+1$ subset from $\{x_1,x_2,...,x_n\}$, so there are $\binom{n}{r+1}$ subsets of size $r+1$ that exclude $x_{n+1}$
	Since these outcomes are disjoint, by the sum rule we can say that $\binom{n+1}{r+1}=\binom{n}{r}+\binom{n}{r+1}$
	