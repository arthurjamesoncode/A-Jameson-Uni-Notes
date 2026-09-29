## Countable Sets
A set which is either finite, or has the same cardinality as $\mathbb{N}$ is considered countable. While this is simple for finite sets, it may be less clear for infinite sets.
## The Integers, $\mathbb{Z}$
For example, take $\mathbb{Z}$. Which set is bigger, $\mathbb{N}$ or $\mathbb{Z}$? You may be tempted to answer $\mathbb{Z}$ as it is a super set of $\mathbb{N}$ also containing the negative numbers. 

However this is wrong. There actually exists a bijection from $\mathbb{N}\to\mathbb{Z}$ which means that both of these sets are actually the same size.

When I think of bijections between the naturals and other infinite sets, I think of ways to **count** the set, guaranteeing that you miss no numbers.

For example, if I just started counting the integers starting at $0$ and incrementing by $1$, I would get "$0,1,2,3,4,5,6,7,8,9,10,...$". This wouldn't work since I would never finish counting the positive integers and therefore would never count $-1$.

So in order to actually **count** the set of integers without missing any I would need to alternate between positive and negative integers to get "$0,1,-1,2,-2,3,-3,4,-4,...$". The fact that I can count the integers in this way shows that there is a bijection from $\mathbb{Z}\to\mathbb{N}$. 

One way we can define this bijection is like so:
	Define $f:\mathbb{Z}\to\mathbb{N}$ given by $f(n)=2n-1\;if\;n>0\;and\;-2n\;otherwise$
This obviously also implies the existence of an inverse function defined like so:
	Define $f^{-1}:\mathbb{N}\to\mathbb{Z}$ given by $f(n) = -\frac{1}{2}n\;if\;n\;is\;even\; and\; \frac{n+1}{2}\;if\;not$
### The Positive Rationals, $\mathbb{Q^+}$
Sometimes the easiest way to show a bijection is visually.

Take the figure below:
![[rational countable.png]]
You can see above that all the rational numbers have been laid out in a grid format. This snake like path moves in a way that can account for every rational without missing a single one. This proves that there is a bijection from $\mathbb{N}\to\mathbb{Q^+}$.

>You may notice that some values are redundant, $\frac{2}{2},\frac{2}{6}$ etc, as these are just the same as $1,\frac{1}{3}$ etc.
>
>In order to be stricter about this you can just skip any entry that is not in its most reduced form.

### Pairs of integers, $\{(a, b)\; |\; a,b\in\mathbb{Z}\}$.
The following is a proof shows that pairs of numbers are in fact countable. Again it is visual, and you can extend this proof to show that $\mathbb{Q}$ and not just $\mathbb{Q^+}$ is in fact countable as each value in $\mathbb{Q}$ is just defined by a pair of integers. 

The proof is as follows:
![[xy-pairs-order.png]]
From the above proof we can see that pairs of numbers can counted similar to how we counted other sets, by using this pattern.

This implies that there is a bijection between $\{(a, b)\; |\; a,b\in\mathbb{Z}\}$ and $\mathbb{N}$.

>This is not the only way to count pairs of numbers, but this does show a repeatable spiral pattern that can be used.
## Uncountable Sets
If a set is not countable it is called uncountable.

For example the set $\{x\;|\;x\in\mathbb{R},0<x<1\}$ is uncountable.
### Cantor's Diagonal Argument
It is sometimes difficult to know whether a set is countable or not. 

Cantor's diagonal argument is a proof that $\mathbb{R}$ is uncountable and it goes as follows.
	Let $S=\{x\;|\;x\in\mathbb{R},0<x<1\}$.
	Suppose for a proof by contradiction that there exists a bijection $f : \mathbb{N^+} \to S$. 
	Consider a list of all decimal representations of $f(n)$, for $n\in\mathbb{N^+}$: 
		$f(1) =0.a_{11}\;a_{12}\;a_{13}\;...a_{1n}\;...$ 
		$f(2) =0.a_{21}\;a_{22}\;a_{23}\;...a_{2n}\;...$ 
		$f(3) =0.a_{31}\;a_{32}\;a_{33}\;...a_{3n}\;...$
		. . . 
		$f(n)=0.a_{n1}\;a_{n2}\;a_{n3}\;...a_{nn}\;...$ 
		. . . 	
	We then show that $\exists\; d\in S$ such that $\forall\; i\in\mathbb{N^+}$ we have $f(i)\neq d$.
	Let $d=0.d_{1}\;d_{2}\;d_{3}\;...d_{n}\;...$ where $d_i = 2\; if\; a_{ii} = 1\;$ and $d_i= 1\; if\; a_{ii} \neq 1$.
	From this definition we know that $\forall\; i\in\mathbb{N^+},\; d$ is different at position $i$ from $f(i)$. 
	So, for no $i\in\mathbb{N^+}$ we have $f(i) = d$, so $f$ is not surjective. 
	This is a contradiction as $f$ is bijection from $\mathbb{N^+}\to S$, therefore a bijection between $\mathbb{N^+}$ and $S$ must not be possible, meaning that $|\mathbb{N^+}|\neq|S|$.

