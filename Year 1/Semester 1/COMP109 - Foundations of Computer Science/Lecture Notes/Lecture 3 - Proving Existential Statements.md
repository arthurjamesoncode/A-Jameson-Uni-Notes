## Existential Statements 
Statements of the form *"$\exists$x Q(x)"* are existential statements. 

The easiest way to prove an existential statement is to find an *x* that makes *Q(x)* true.

For example, the statement *"$\exists$ an even integer that can be written in two ways as a sum of 2 prime numbers* can be proved with the following examples:
	*10 = 5+5 and 10 = 7 + 3 
	16 = 5 + 11 and 16 = 13 + 3
	 And more...*

I gave 2 examples, and more certainly exist, but only 1 is necessary to prove an existential statement such as this.

>Notice how the wording of the statement does not specify 2 different prime numbers so the first example is sufficient. However even if it did there are clearly other examples that are valid, such as the second.

## Constructive Proof
The above proof is an example of a constructive proof. A constructive proof is a proof where you provide an explicit example, or a formula/algorithm with which you can build a specific example.

As another example take the statement "*For 2 integers, r and s, $\exists$ an integer k such that 22r + 18s = 2k"*. We can prove this like so:
	 *Let k = 11r + 9s
	 Since r and s are integers, 11r and 9s must also be an integers as they are the products of 2 integers. 
	 Therefore k is an integer as it is the sum of 2 integers.
	 For this value of k, 2k = 22r + 18s.
	 Therefore, for integers r and s, there must exist an integer k for which 2k = 22r + 18s.

This example is more general since *r* and *s* are not specific integers, but for this problem we just find a value for k in terms of *r* and *s*. Since the product of 2 integers and must be an integer and the sum of 2 integers must be an integer, we can still show this number to be an integer and therefore prove the statement.

So given any 2 specific integers *r* and *s* computing *11r+2s* gives you an example for which the statement is true.

As a final example take the statement "*$\exists$ integers m and n such that m > 1, n > 1 and $\frac{1}{m}$+$\frac{1}{n}$ is an integer*". We can prove this with the following examples
	*m=2 and n=2 since  $\frac{1}{2}$+$\frac{1}{2}$=1
	m=-n since  $\frac{1}{m}$+$\frac{1}{-m}$=0 

For this example we can give both specific examples and a formula. The first example obviously shows an integer result. The second example again shows an integer result but it does this generally. It also proves the same statement above but with the added constraint of *"m $\neq$ n"*

>Its important to recognise that using a general statement like that one is not necessary for an existential statement such as this. Even if there was the added constraint of "*m$\neq$n" since simply giving the example of "m=2 and n=-2*" also proves that statement. That being said, finding these general proofs are a good way to bolster your understanding of a problem.
### More Involved Example
Now we are going to try and prove the following claim, write our proof in a formal way, and then use this proof to then prove the final statement from Lecture 2s examples.

>Let *a, b* $\in$ $\mathbb{Z}$, where b $\neq$ 0. $\exists$ *q, r* $\in$ $\mathbb{Z}$ such that *a = bq + r, r < b and r >= 0* .

The above statement written in plain English instead of with maths notation is "*For any 2 integers a and b, there exists 2 integers q and r such that a = bq + r, r < |b| and r >= 0*". 

We will start by proving a weaker statement.

>Let *a, b* $\in$ $\mathbb{N}$, where b $\neq$ 0. $\exists$ *q, r* $\in$ $\mathbb{N}$ such that *a = bq + r and r < b*.

The above statement written in plain English instead of with maths notation is "*For any 2 natural numbers a and b, there exists 2 natural numbers q and r such that a = bq + r and r < b*". 

To prove this claim we say:
	*Let q be the largest number such that bq <= a
	Let r = a - bq 
	If r >= b then q is not the largest natural number such that bq <= a
	Therefore $\exists$ q, r $\in$ $\mathbb{N}$ such that a = bq + r and r < b

To prove the first, stronger claim we can split this into multiple cases.
- Case 1: a >= 0 and b > 0
- Case 2: a >= 0 and b < 0
- Case 3: a < 0 and b > 0
- Case 4: a < 0 and b < 0

Case 1 we proved already, as natural numbers are a subset of integers.

For Case 2 we can prove it like so:
	*Let q be the smallest number such that bq <= a
	Let r = a - bq 
	If r >= |b| then q is not the smallest integer such that bq <= a
	Since bq <= a, a - bq >= 0
	Therefore $\exists$ q, r $\in$ $\mathbb{N}$ such that a = bq + r, r < |b| and r >= 0

For Case 3 we can prove it like so:
	*Let q be the largest integer such that bq <= a
	Let r = a - bq 
	If r >= |b| then q is not the largest integer such that bq <= a
	Since bq <= a, a - bq >= 0
	Therefore $\exists$ q, r $\in$ $\mathbb{N}$ such that a = bq + r, r < |b| and r >= 0

For Case 4 we can prove it like so:
	*Let q be the smallest integer such that bq <= a
	Let r = a - bq 
	If r >= |b| then q is not the smallest integer such that bq <= a
	Since bq <= a, a - bq >= 0
	Therefore $\exists$ q, r $\in$ $\mathbb{N}$ such that a = bq + r, r < |b| and r >= 0

This list of cases is exhaustive and so since each one has been proved true the statement must be true.

The only thing that changes about these cases is the first line, and you could simplify it so that case 1 and 3 are together and case 2 and 4 are together, but this is sufficient to prove the statement.

Now we can prove the statements "*Every integer is either even or odd*" using this proof:
	*Let a $\in$ $\mathbb{Z}$, choose b = 2
	(From our last proof we know that) 
	$\exists$ q, r such that a = 2q + r, r < 2 and r >= 0
	The only possible values for r are 0 or 1.
	Therefore a = 2q or a = 2q + 1.
	By definition of even and odd a must be either even, or odd.

 


 
