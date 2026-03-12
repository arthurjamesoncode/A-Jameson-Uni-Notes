 C## Indirect Proof of an Existential Statement
We can prove some existential statements indirectly as well.

For example we can prove the statement "*${\exists  p, q \in \mathbb{R} \setminus \mathbb{Q}\; such\; that\; p^q \in \mathbb{Q}}$ "

>$\mathbb{R} \setminus \mathbb{Q}$ means the set difference of $\mathbb{R}$ and $\mathbb{Q}$. This means all the elements in the set of reals that are not in the set of rationals. So the full statement in plain English reads: "There exists irrational numbers p and q such that p$^q$ is rational."

To prove an existential statement we simply need to prove that the statement is true for example. Our proof for this can be indirect.

One way to prove this statement is this:
	${Every\; real\; number\; must\; be\; rational\; or\; irrational.}$
	${Therefore\; \sqrt{2}^{\sqrt2}\; must\; be\; rational\; or\; irrational.}$
	${Case\; 1:\; \sqrt{2}^{\sqrt2}\; is\; rational}$
		${In\; this\; case\; p=\sqrt{2}, q=\sqrt{2},\; and\; the\; claim\; is\; clearly\; true!}$
	${Case 2:\; \sqrt{2}^{\sqrt2}\; is\; irrational}$
		${Let\; p =  \sqrt{2}^{\sqrt2}\; and\; q= \sqrt{2}.}$
		${Then\; p^q={(\sqrt{2}^{\sqrt2})}^{\sqrt2}=\sqrt{2}^{2}=2}$
		${Since\; 2\; is\; rational,\; the\; claim\; is\; true!}$
	${As\; the\; claim\; is\; true\; is\; both\; cases,\; and\; the\; cases\; are\; exhaustive,\; the\; claim\; must\; be\; true}$

## When to use Indirect Proof
Many theorems can be proved indirectly or directly, however direct proof is usually preferable since indirect proofs tend to be clumsier.

In the absence of obvious clues suggesting that indirect argument is the way to go, try to prove a statement directly. If that does not succeed, then look for a counterexample, to the truth of the statement.

If a counterexample can not be found, then start to look for a proof by contradiction.

Essentially, proof by contradiction should be a last resort when going about proving a statement.
## Proof By Induction
Mathematical induction is one of the more recently developed techniques of proof in the history of mathematics, about 1000 years old, which is recent in terms of maths.

It is used to check conjectures about the outcomes of processes that occur repeatedly and according to definite patterns.

In general, mathematical induction is a method for proving that a property defined for integers n is true for all values of n that are greater than or equal to some initial integer. 

For example take a row of dominos, if I can show that for every natural number *m*, if the *m*th domino falls then the (m+1)th domino will fall. Then I can conclude that all the dominos will fall.

For generalisation from the generic particular, we are showing that if a property holds for some arbitrary value *x* then it holds for all possible values x.

For induction we are showing that if it holds for 1 possible value in a set, it will hold for the next possible value in a set, and therefore that it holds for all possible values in that set, after our initial case.

For example take the statement: "${\forall{n} \in \mathbb{N}, 0+1+...+n=\frac{n(n+1)}{2}}$". 

>The $...$ is called an iterator, and is used to imply the existence of an arbitrarily long sequence. When writing an equation with an iterator you include the operations on either side. For example, "$+1+...+n$" and not "$+1{...}n$".  More formal notation for this would use the sum symbol, $\sum$, however this notation is fine.
>
>In plain English this statement says "*For all natural numbers n, the sum of all the numbers from 0 to n inclusive is equal to $\frac{n(n+1)}{2}$".

To prove this statement we first need to show that it holds for the base case, 0, and then we show, generally, that if it holds for n then it holds for n+1.

So we can prove this by doing:
	*Base Case 0: *
		${\frac{0(0+1)}{2}=\frac{0}{2}=0}$ 
		*This property holds for 0*
	*Inductive step:*
		${Assume\;0+1+...+k=\frac{k(k+1)}{2}}$
		${Then\; \;0+1+...+k+(k+1) = \frac{k(k+1)}{2} + (k+1) = \frac{k^2+k}{2} + \frac{2k+2}{2} = \frac{k^2 + 3k + 2}{2} = \frac{(k+1)(k+2)}{2}}$
		${As\; \frac{(k+1)(k+2)}{2}\; is\; of\; the\; form\; \frac{n(n+1)}{2}\; this\; must\; true\; for\; n+1\; if\; it\; is\; true\; for\; n}$
	*Since it is true for n+1 if it is true for n, and it is true for our base case of 0, we know that it must be true for all n $\geq$ 0.*		

Notice first step here is to show that is is true for a specific example, but the second is more general. 

In the second step, we assume the statement to be true for all values up to *k*, and using this assumption we show that the next step can take the same form but substituting in *k+1*, instead.

As another example take the statement "${\forall{n}\in \mathbb{N},\; 1+3+...+(2n+1)=(n+1)^2}$". This statement is the same as "*The sum of the first n odd numbers is the same as the nth natural square.*"

To prove this we can do:
	*Base Case. 0:*
		${(n+1)^2=(0+1)^2=1}$
		*The statement holds for the base case*
	*Inductive Step:*
		 ${Assume\; 1+3+...+(2k+1)=(k+1)^2}$
		 ${Then\;  1+3+...+(2k+1)+(2(k+1)+1)=(k+1)^2 + (2(k+1)+1)}$
		 ${=(k+1)^2+2k+3=k^2+2k+1+2k+3=k^2+4k+4=(k+2)^2=((k+1)+1)^2}$
		 ${As\; ((k+1)+1)^2\; is\; of\; the\; form\; (n+1)^2\; this\; must\; true\; for\; n+1\; if\; it\; is\; true\; for\; n}$
	*Since it is true for n+ 1 if it is true for n, and it is true for our base case of 0 we know it must be true for all n $\geq$ 0*
