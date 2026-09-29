## Proof by Cases Continued
Take the statement, "*The square of any integer is of the form 3k or 3k + 1*". If we try to solve it using the same cases as above we will get something like this:

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

This is another problem for which the exhaustive nature of the cases is obvious enough that you wouldn't really need to prove it, but its good to anyway.

## Indirect Proofs
In a direct proof you start with the hypothesis of a statement and make one deduction after another until you reach the conclusion. 

Indirect proofs are more roundabout. One kind of indirect proof, argument by contradiction, is based on the fact that either a statement is true or it is false but not both. Proof by contradiction is the only indirect proof technique that will be covered in this module.

So if you can show that the assumption that a given statement is not true leads logically to a contradiction, impossibility, or absurdity, then that assumption must be false: and, hence, the given statement must be true.

For example take the statement "*There is no greatest integer*", we can prove this statement like so:
	Assume, for the sake of contradiction that there is a greatest integer n.
	n + 1 exists, n + 1 $\in$ $\mathbb{Z}$ and n + 1 $\geq$ n
	This contradicts that n is the greatest integer. 
	Therefore there must not be a greatest integer.

In this method of proof the first thing we assume is that the negation is true. We can then do something with that assumption. If this eventually contradicts a known fact or this assumption itself then we know that the negation is false, and thus the statement must be true.

### More Examples

**No Integer can be both even and odd:**
	*Suppose, for the sake of contradiction, that $\exists$ n $\in$ $\mathbb{Z}$, such that n is even and n is odd.
	By definition n = 2k and n = 2l + 1 where k, l $\in$ $\mathbb{Z}$.
	2k = 2l + 1, k = l + $\frac{1}{2}$
	As l is an integer and $\frac{1}{2}$ is not, this shows us that k is not an integer.
	This is a contradictions as k $\in$ $\mathbb{Z}$ so therefore no integer can be both even and odd.*

**$\forall$m $\in$ $\mathbb{Z}$ if m$^2$ is even then m is even:**
	*Suppose for the sake of contradiction that m$^2$ is even and m is odd.
	By definition of odd m = 2k + 1
	m$^2$ = (2k + 1)$^2$ = 4k$^2$ + 2k + 1 = 2(2k$^2$ + k) + 1
	Since 2k$^2$ + k is an integer, by definition m$^2$ is odd. 
	This is a contradiction so therefore is m$^2$ is even then m is even.

### Proof By Contraposition
When trying to prove "*$\forall$x if P(x) then Q(x)*" it suffices to prove "*$\forall$x if not P(x) then not Q(x)*".

"*$\forall$x if not P(x) then not Q(x)*" is the contrapositive of "*$\forall$x if P(x) then Q(x)".
