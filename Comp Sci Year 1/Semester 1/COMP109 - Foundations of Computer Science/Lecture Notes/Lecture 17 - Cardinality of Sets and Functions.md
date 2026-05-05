## Finite Sets
The cardinality of a finite set, $A$, is the number of elements in $A$.

For finite sets $A$ and $B$:
- $|A|\geq |B| \iff$ there is a surjective function from $A\to B$.
- $|A|\leq |B| \iff$ there is an injective function from $A\to B$.
- $|A|=|B| \iff$ there is a bijection from $A\to B$.

>Reminder: $\iff$ means "if, and only if".

This is because if a function is surjective, it means that every element in $B$ is mapped to **at least once**. This means that the smallest possible cardinality of $A$ is equal to the cardinality of $B$. In this case each element of $A$ maps to exactly one element of $B$, so the function would be also injective and therefore bijective.

If a function is injective, however, it means that every element in $B$, that is part of the range, $f(A)$, is only mapped to by one element of $A$. Since $f(A)$ is a subset of $B$ it means that the largest possible cardinality of $A$ is equal to the cardinality of $B$. In this case each element of $B$ is mapped to by an element of $A$, making the function surjective and therefore bijective.

## The Pigeonhole Principle
Take $f: A\to B$ to be a function where $A$ and $B$ are finite sets.

The pigeonhole principle states that is $|A|>|B|$ then at least one value of $f$ occurs more than once. In other words, $\exists\; a,b\in A$ such that $a\neq b$ and $f(a)=f(b)$.

>Reminder: $\exists$ means "there exists". The statement above in plain English reads "There exists values a and b in A such that a and b are different and f(a)=f(b)".

Simply: **If (N+1) pigeons occupy N holes, then some hole must have at least 2 pigeons**.

### Using the Pigeon Hole Principle:
The following are examples of problems that can solved using the pigeon hole principle, and the method for solving them.

The steps for solving these problems all start the same way. We start by defining a function, $f: A\to B$, where $A$ and $B$ are the sets of things we are comparing.

Sometimes, we will only be able to compute the cardinality of $B$, and be asked to be given the minimal, or maximal, possible value of $|A|$ such that some property holds, but again this is done the same. 

"There are 15 people on a bus. Show that at least two of them have a
birthday in the same month of the year.":
	Let $A= \{people\; on\; the\; bus\},\; B=\{months\}$.
	Define $f: A\to B$ given by $f\{person\}=The\; month\; they\; were\; born\; in$
	$|A|=15, |B|=12$
	Observe that as there are more people on the bus then there are months since, $|A| > |B|$.
	Therefore by the pigeonhole principle, $\exists\;p_1,p_2,\;$such that $f(p_1)=f(p_2)$ and $p1\neq p_2$,
	Or, in plain English, there are at least 2 distinct people on the bus with the same birth month.

The steps for this first problem are as follows:
- We start by defining a function, $f: A\to B$, where $A$ is the set of all the people on the bus and $B$ is the set of all months in the year.
- We then compare the cardinality of $A$ and $B$.
- Since $|A|>|B|$ we know the pigeonhole principle applies, and then write our conclusion.

"How many different surnames must appear in a telephone directory to
guarantee that at least two of the surnames begin with the same letter of the
alphabet and end with the same letter of the alphabet?":
	Let $A=\{surnames\;in\;directory\},\; B=\{pairs\;of\;characters\}$
	Define $f: A\to B$ given by $f(surname)=(first\;character,\; last\;character)$.
	Observe that $|B|=26\cdot26=676$.
	For the pigeonhole principle to apply, it must be the case that $|A|>|B|$.
	Therefore, to guarantee that at least two surnames begin with the same letter of the alphabet and end with the same letter of the alphabet, the directory must contain at least $676+1$ or $677$ surnames.

The steps for this second problem are as follows:
- We start by defining a function, $f: A\to B$, where $A$ is the set of all the surnames in the directory and $B$ is the set of all pairs of characters.
- In this problem, we have 1 set without a fixed cardinality, $A$, and 1 with a fixed cardinality, $B$. We have to calculate the fixed cardinality, which is given by $26\cdot 26$ or $676$.
- We know from the question that the pigeonhole principle must apply, so we take the minimum value of $|A|$ that makes it apply and write our conclusion.  

"Five numbers are selected from the numbers 1, 2, 3, 4, 5, 6, 7 and 8.
Show that there will always be two of the numbers that sum to 9."
	Let $A=\{chosen\;numbers\},\;B = \{pairs\;of\;numbers\;from\;1\;to\;8\;which\;sum\;to\;nine\}$.
	Observe $B=\{\{1,8\},\; \{2,7\},\; \{3,6\},\; \{4,5\}\}$ and $|B|=4$
	Define $f: A\to B$ given by $f(n)= the\; set\; S\in B\; such\; that\; n\in S$.
	Since $|A|=5$ then $|A|>|B|$.
	Therefore, by the pigeonhole principle, $\exists\; a_1, a_2\in A$ such that $f(a_1)=f(a_2)$ and $a_1\neq a_2$.
	This guarantees that if 5 distinct numbers are chosen from the numbers 1 to 8, there will be at least 2 numbers chosen that sum to 9.

The steps for this third problem are as follows:
- We start by defining a function, $f: A\to B$, where $A$ is the set of chosen numbers and $B$ is the set of all pairs of number from 1 to 8 which sum to 9.
- The tricky thing with this problem is recognising what $A$ and $B$ should be, and finding the cardinality of B. The rest is the same as the first problem.
- Since $|A|>|B|$ we know the pigeonhole principle must apply, and we write our conclusion.

