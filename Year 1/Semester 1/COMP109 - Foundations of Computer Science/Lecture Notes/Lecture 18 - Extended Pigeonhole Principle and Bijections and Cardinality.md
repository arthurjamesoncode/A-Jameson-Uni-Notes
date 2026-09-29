## Extended Pigeonhole Principle
Consider a function $f: A\to B$ where $A$ and $B$ are finite sets and $|A|>k|B|$ for some $k\in\mathbb{N}$. This means that there is some value of $f$ which occurs at least $k+1$ times.

This is the extended pigeonhole principle. The standard version, the one from last lecture, is simply this same rule but $k=1$.
### Extended Pigeonhole Principle Examples
The following are problems that can be solved using the extended pigeonhole principle.

"How many different surnames must appear in a telephone directory to guarantee that at least five of the surnames begin with the same letter of the alphabet and end with the same letter of the alphabet?":
	Let $A=\{surnames\},\; B=\{pairs\;of\;characters\}$
	Define $f: A\to B$ given by $f(surname)=(first\;character,\; last\;character)$
	Observe $|B|=26\cdot26=676$
	By the extended pigeonhole principle, we know that to guarantee that at least $5$ surnames share the same first and last character it must be the case that $|A|>4\cdot|B|$.
	Therefore $|A|>4\cdot676,|A|>2704$.
	This means that, to guarantee that at least $5$ surnames share the same first and last character, the directory must contain at least $2704+1$ or $2705$ surnames.

This first problem is the same as one of the problems from [[Lecture 17 - Cardinality of Sets and Functions]] except it has a value for k. Because of this I won't explain it further.

This next problem however is very different. We use the extended PHP to show that one of 2 cases must be true, and then we analyse each case to show that the main statement must be true.

"Show that in any group of six people there are either three who all know each other or three complete strangers.":
	Let the six people be $p_1,p_2,p_3,p_4,p_5,p_6$.
	Let $A=\{p_2,p_3,p_4,p_5,p_6\},\; B=\{0,1\}$.
	Define $f: A\to B$ given by $f(p_x)= 0\;if\;p_1\;and\;p_x\;don't\;know\;each\;other,\;and\;1\;otherwise$
	Observe that $|A|=5,\;|B|=2$ and so $|A|>2\cdot |B|$
	By the extended pigeonhole principle, it must be the case that either $3$ people know $p_1$ or $3$ people do not know $p_1$.
	Case 1, $3$ people know $p_1$:
		Three people $a,b,c$ all know $p_1$.
		If any pair of $(a,b),\;(b,c),\; or\; (a,c)$ knows each other then we have 3 people who all know each other.
		Otherwise if none of these pairs know each other then we have 3 people who don't know each other.
	 Case 2, $3$ people don't know $p_1$:
		Three people $a,b,c$ all don't know $p_1$.
		If any pair of $(a,b),\;(b,c),\; or\; (a,c)$ don't know each other then we have 3 people who don't know each other.
		Otherwise if all of these pairs know each other then we have 3 people who know each other.
	As both of these cases show the statement to be true, and we have shown these cases to be exhaustive, it must be the case that in in any group of six people there are either three who all know each other or three complete strangers.
## Bijections and Cardinality
### Finite Sets
Recall from [[Lecture 17 - Cardinality of Sets and Functions]] that the cardinality of a finite set is the number of elements in the set and that $|A|=|B| \iff$ there is a bijection from $A\to B$.

For example take the sets:
- $S=\{s_1,s_2,...,s_n\}$
- $B^n=$ the set of bit strings of length $n$

The function $f: Pow(S)\to B^n$ which assigns each subset $A$ of $S$ to it's characteristic vector is a bijection. 

We used this in [[Lecture 14 - The Cardinality of Sets]] to determine that $|Pow(X)|=2^{|X|}$. 
### Infinite Sets
Similar to finite sets, we can show that 2 infinite sets have the same cardinality by finding a bijection between the 2.

For Example take the figure below:
![[line_segment_bijection.png]]
This figure shows that 2 line segments $AB$ and $AC$ have a bijection between points of $AC$ and points on $AB$.

Essentially if you start on $AC$ and draw a line parallel to $BC$ you will intersect $AB$ at a unique point. Since this is reversible, we can just start on $BC$ and draw the same line in the other direction, we know that this can cover every possible point on $BC$.

Because of this, this function of drawing a line parallel to $BC$ is a bijection between the set of points on $AC$ and the set of points on $AB$.

Essentially the above image shows that any 2 line segments both have the same number of points, despite having different lengths.

As another example look at the following figure:
![[0-1R=R.png]]
This figure is a geometric proof of $|\mathbb{R}|=|\{x\;|\;x\in\mathbb{R},0<x<1\}$. It shows that there are as many real numbers between 0 and 1 and there are real numbers in total.

If you just read that sentence you might be confused as to how that is possible, and it is simply that infinities are incredibly counter intuitive. The statement seems impossible but it is true.

Essentially if we choose any real number on the line at the bottom and draw a line through the center of the circle it will land on a unique point in the top semi circle. The point on this line indicating the real numbers between $0$ and $1$ that reflects the point chosen on that semi circle is our real number between $0$ and $1$. Again since this is reversible we know that it must hit every point on this semi circle, and therefore be a bijection.

>Notice $0$ and $1$ are not included in the inequality as $x$ is strictly between them. This is because the line representing the reals and the bottom of the top semi-circle are parallel. A line drawn from the point on the semi-circle that corresponds to $0$ or $1$ drawn through the center of the circle would never actually meet the line representing the reals, and so it is not part of the proof.
>
>It's also important to recognise that the numbers $0$ and $1$ are arbitrary here. If you substitute them out for $x$ and $y$, this is actually a proof that the number of real numbers in any interval is equal to the number of real numbers.


