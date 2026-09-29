## Laws
There are many laws with which we can perform algebra on expressions containing sets. For the following laws suppose that $A,\;B,\;C,\;U$ are sets with $A\subseteq U,\; B\subseteq U,\; C \subseteq U$. QQ
### Commutative Laws
If an operation, $O$,  is commutative it means that the order of the operands does not matter.  Essentially stating $x\;O\;y=y\;O\;x$.

Examples of some commutative operations are sum, $+$, and product, $\cdot$. You should know this intuitively, as $5+3=3+5$ and $5\cdot 3 = 3\cdot 5$.

With regard to sets the commutative operations we know are:
- Union, $\cup$
- Intersection, $\cap$
- Symmetric Difference, $\triangle$

So the commutative laws with regards to set algebra are:
- $A\cup B = B\cup A$
- $A \cap B = B \cap A$
- $A \triangle B = B \triangle A$
### Associative Laws
If an operation $O$ is associative it means that the way in which multiple operations are grouped does not matter. Essentially it means that $(x\;O\;y)\;O\;z=x\;O\;(y\;O\;z)$.

Again examples of some associative operations are sum, $+$, and product, $\cdot$. You should know this intuitively as $(5+3)+2=5+(3+2)$ and $(5\cdot3)\cdot2=5\cdot(3\cdot2)$.

With regard to sets the associative operations we know are:
- Union, $\cup$
- Intersection, $\cap$
- Symmetric Difference, $\triangle$

So the associative laws with regards to set algebra are:
- $(A\cup B)\cup C = A\cup (B\cup C)$
- $(A\cap B)\cap C = A\cap (B\cap C)$
- $(A\triangle B)\triangle C = A\triangle (B\triangle C)$
### Distributive Laws
The distributive property relates 2 operations, $O_1$ and $O_2$. It essentially means that if $O_1$ is applied to a group combined by $O_2$ the operation can be spread, or distributed, to each member of the group. Essentially this states that $x\;O_1\;(y\;O_2\;z)=(x\;O_1\;y)\;O_2\;(x\;O_1\;z)$. When this is true we say that $O_1$ is distributive over $O_2$

>Strictly speaking "$x\;O_1\;(y\;O_2\;z)=(x\;O_1\;y)\;O_2\;(x\;O_1\;z)$" is the left distributive law and "$(y\;O_2\;z)\;O_1\;x=(y\;O_1\;x)\;O_2\;(z\;O_1\;x)$" is the right distributive law. 
>
>For a property to be distributive both of these must hold, however most operations you will encounter in this module will either hold for both laws or neither so knowing this distinction is somewhat unnecessary. There is one exception to this which is that $-$ over $U$. This relation is only right distributive.

We know, from our ability to factorise, that product, $\cdot$ is distributive over sum, $+$. We can see this in $2 \cdot (5+3)=(2\cdot 5) + (2\cdot 3)$. 

The following are distributive relationships in regard to the set operations we know:
- $\cup$ is distributive over $\cap$
- $\cap$ is distributive over $\cup$
- $\cap$ is distributive over $\triangle$
- $\cap$ is distributive over $-$
- $-$ is right distributive over $\cup$ 

So the distributive laws with regards to the set operations we have covered are:
- $A \cup (B\cap C)=(A\cup B) \cap (A\cup C)$
- $A \cap (B\cup C)=(A\cap B) \cup (A\cap C)$
- $A \cap (B\triangle C)=(A\cap B) \triangle (A\cap C)$
- $A \cap (B-C)=(A\cap B) - (A\cap C)$
- $(B\cup C) - A = (B-A)\cup (C-A)$
### Identity Laws
Identity laws are relatively simple. They essentially are just used to simplify operations between  a set, A, and the empty set, $\emptyset$, or the universal set, $U$. The result of these operations is always the set A. This is what makes them identity laws.

The identity laws in set theory are this:
- $A\cup \emptyset=A$
- $A\cap U=A$
- $A-\emptyset = A$ 
- $A \triangle \emptyset=A$

You can understand why these are true intuitively.
### Complement Laws
Complement laws show the results of certain operations of a set with it's complement. 

The complement laws are as follows:
- $A\cup A^c=U$
- $A \cap A^c=\emptyset$
- $A-A^c=A$
- $A\triangle A^c=U$
### Double Complement Law
The double complement law simply states that the complement of the complement of a set is the set itself. 

So $(A^c)^c=A$.
### Idempotent Laws
The idempotent laws are laws that show when an operation on a set is applied to itself it always results in the original set.

The idempotent laws in set theory are:
- $A\cup A$ = A
- $A \cap A = A$
### Universal Bound Laws
Universal bound laws are like the identity laws, in that they describe how a set, $A$ interacts with the empty set, $\emptyset$, and the universal set, $U$. These are called boundary laws because $\emptyset$ and $U$ are the boundaries of any given system. They differ from identity laws in that the result of the operations are not the set $A$.

The universal bound laws are:
- $A\cup U=U$
- $A\cap \emptyset=\emptyset$
### De Morgan's Laws
De Morgan's Laws state that the complement of the union of two sets is the same as the intersection of the complements of the individual sets. They also state that the complement of the intersections of two sets are the same as the union of the complements of the individual sets.

Essentially:
- $(A\cup B)^c=A^c \cap B^c$
- $(A\cap B)^c=A^c \cup B^c$

### Absorption Laws
Absorption laws show how when you apply certain operations on a set to an operation between that set and another, it can be simplified to the set itself.

The absorption laws are:
- $A\cup (A\cap B)=A$
- $A \cap (A\cup B) = A$

In the first of these laws the union operation absorbs the intersection operation, as if something is in $A \cap B$ it is already in $A$.

In the second of these laws the intersection operation absorbs the union operation as the $A\cup B$ is a superset of $A$.
### Complement of $U$ and $\emptyset$
The complement $U$ and $\emptyset$ is always the other.

So:
- $U^c=\emptyset$
- $\emptyset^c=U$ 
### Set Difference Law
The set difference law states that $A - B$ is the same as the intersection of $A$ with the complement of $B$

So $A-B=A\cap B^c$.
## Proving Laws
### Proving The Commutative Laws
To prove the Commutative property of and operation, $O$ on two sets, $A$ and $B$, we need to prove that $A\; O\; B=B\; O\; A$. 

To do this we can look at an arbitrary element, $x$, and check if $x \in A\; O\; B\; and\;x\in B\;O\;A$ are equivalent for all possible cases. if $x \in A\; O\; B\; and\;x\notin B\;O\;A$ or vice versa for any case, then $A\; O\; B\neq B\; O\; A$, Otherwise $A\; O\; B=B\; O\; A$.

The four possible cases for an element $x$:
- $x\in A\;and\;x\in B$
- $x\in A\;and\;x\notin B$
- $x\notin A\;and\;x\in B$
- $x\notin A\;and\;x\notin B$

So to prove that $\cup$ is commutative:
	Case 1, $x\in A\;and\;x\in B$:
		Since $x\in A$, by definition of $\cup$, it must be that $x \in A \cup B\; and\; x \in B \cup A$.
	Case 2, $x\in A\;and\;x\notin B$:
		Since $x\in A$, by definition of $\cup$, it must be that $x \in A \cup B\; and\; x \in B \cup A$.
	Case 3, $x\notin A\;and\;x\in B$:
		Since $x\in B$, by definition of $\cup$, it must be that $x \in A \cup B\; and\; x \in B \cup A$.
	Case 4, $x\notin A\;and\;x\notin B$:
		Since $x\notin A\;and\;x\notin B$, by definition of $\cup$, it must be that $x \notin A \cup B\; and\; x \notin B \cup A$.
	As $x$ is either in both or neither of $A\cup B$ and $B\cup A$ in all of these cases, it means that $A\cup B=B\cup A$.

So to prove that $\cap$ is commutative:
	Case 1, $x\in A\;and\;x\in B$:
		Since $x\in A\;and\;x\in B$, by definition of $\cap$, it must be that $x \in A \cap B\; and\; x \in B \cap A$.
	Case 2, $x\in A\;and\;x\notin B$:
		Since $x\notin B$, by definition of $\cap$, it must be that $x \notin A \cap B\; and\; x \notin B \cap A$.
	Case 3, $x\notin A\;and\;x\in B$:
		Since $x\notin A$, by definition of $\cap$, it must be that $x \notin A \cap B\; and\; x \notin B \cap A$.
	Case 4, $x\notin A\;and\;x\notin B$:
		Since $x\notin A$, by definition of $\cap$, it must be that $x \notin A \cap B\; and\; x \notin B \cap A$.
	As $x$ is either in both or neither of $A\cap B$ and $B\cap A$ in all of these cases, it means that $A\cap B=B\cap A$.

So to prove that $\triangle$ is commutative:
	Case 1, $x\in A\;and\;x\in B$:
		Since $x\in A\;and\;x\in B$, by definition of $\triangle$, it must be that $x \notin A \triangle B\; and\; x \notin B \triangle A$.
	Case 2, $x\in A\;and\;x\notin B$:
		Since $x\in A\;and\;x\notin B$, by definition of $\triangle$, it must be that $x \in A \triangle B\; and\; x \in B \triangle A$.
	Case 3, $x\notin A\;and\;x\in B$:
		Since $x\notin A\;and\;x\in B$, by definition of $\triangle$, it must be that $x \in A \triangle B\; and\; x \in B \triangle A$.
	Case 4, $x\notin A\;and\;x\notin B$:
		Since $x\notin A\;and\;x\notin B$, by definition of $\triangle$, it must be that $x \notin A \triangle B\; and\; x \notin B \triangle A$.
	As $x$ is either in both or neither of $A\triangle B$ and $B\triangle A$ in all of these cases, it means that $A\triangle B=B\triangle A$.

>Previously, when proving that two sets are equal we proved that both sets were subsets of each other. 
>
>We can still do this with these sets, this strategy can just show a different way to prove set equivalence.
### Proving De Morgan's Laws
When trying to prove De Morgan's Laws we need to prove both $(A\cup B)^c=A^c \cap B^c$ and $(A\cap B)^c=A^c \cup B^c$.

To show how we can use either strategy used so far we will prove $(A\cup B)^c=A^c \cap B^c$ by looking at the possible cases of an element $x$ and prove $(A\cap B)^c=A^c \cup B^c$ by proving that $(A\cap B)^c\subseteq A^c \cup B^c$ and $A^c \cup B^c\subseteq (A\cap B)^c$.

So to prove $(A\cup B)^c=A^c \cap B^c$ we can do:
	Case 1, $x\in A\;and\;x\in B$:
		Since $x\in A$, by definition of complement, it must be that $x\notin A^c$.
		Therefore $x\notin A^c \cap B^c$.
		Since $x\in A$, by definition of union, it must be that $x\in A\cup B$.
		Therefore $x\notin (A\cup B)^c$. 
	Case 2, $x\in A\;and\;x\notin B$:
		Since $x\in A$, by definition of complement, it must be that $x\notin A^c$.
		Therefore $x\notin A^c \cap B^c$.
		Since $x\in A$, by definition of union, it must be that $x\in A\cup B$.
		Therefore $x\notin (A\cup B)^c$. 
	Case 3, $x\notin A\;and\;x\in B$:
		Since $x\in B$, by definition of complement, it must be that $x\notin B^c$.
		Therefore $x\notin A^c \cap B^c$.
		Since $x\in B$, by definition of union, it must be that $x\in A\cup B$.
		Therefore $x\notin (A\cup B)^c$. 
	Case 4, $x\notin A\;and\;x\notin B$:
		Since $x\notin A\;and\;x\notin B$, by definition of complement, it must be that $x\in A^c\;and\;x\in B^c$.
		Therefore $x\in A^c \cap B^c$.
		Since $x\notin A\;and\;x\notin B$, by definition of union, it must be that $x\notin A\cup B$.
		Therefore $x\notin (A\cup B)^c$. 
	As $x$ is either in both or neither of $(A\cup B)^c$ and $A^c \cap B^c$ in all of these cases, it means that $(A\cup B)^c=A^c \cap B^c$.

And to prove $(A\cap B)^c=A^c \cup B^c$ :
	We must prove $(A\cap B)^c\subseteq A^c \cup B^c$ :
		Let $x\in (A\cap B)^c$
		By definition of complement, $x\notin A\cap B$.
		This means that one of the following must be true:
			- $x\in A\;and\; x\notin B$
			- $x\notin A\;and\; x\in B$
			- $x\notin A\;and\; x\notin B$
		Case 1, $x\in A\;and\; x\notin B$ :
			Since $x\notin B$, it must be that $x\in B^c$.
			Therefore $x\in A^c\cup B^c$.
		Case 2, $x\notin A\;and\; x\in B$ :
			Since $x\notin A$, it must be that $x\in A^c$
			Therefore $x\in A^c\cup B^c$
		Case 3, $x\notin A\;and\; x\notin B$ :
			Since $x\notin A$, it must be that $x\in A^c$
			Therefore $Since $x\notin A$, it must be that $x\in A^c$
			Therefore $x\in A^c\cup B^c$$
		In all cases $x\in A^c\cup B^c$, and so it must be that $(A\cap B)^c\subseteq A^c \cup B^c$
	Next we must prove that $A^c \cup B^c\subseteq (A\cap B)^c$ :
		Let $x\in A^c \cup B^c$
		By definition of complement and union we know that one of the following must be true:
			- $x \notin A\; and\; x \notin B$
			- $x \notin A\; and\; x \in B$
			- $x \in A\; and\; x \notin B$
		Case 1, $x \notin A\; and\; x \notin B$ :
			Since $x\notin A$, it must be that $x\notin A \cap B$.
			Therefore $x\in (A\cap B)^c$.
		Case 2, $x \notin A\; and\; x \in B$ :
			Since $x\notin A$, it must be that $x\notin A \cap B$.
			Therefore $x\in (A\cap B)^c$.
		Case 3, $x \in A\; and\; x \notin B$ :
			Since $x\notin B$, it must be that $x\notin A \cap B$.
			Therefore $x\in (A\cap B)^c$.
		In all cases $x\in (A\cap B)^c$, and so it must be that $A^c \cup B^c\subseteq (A\cap B)^c$.
	Since both sets are subsets of each other it must be the case that $(A\cap B)^c=A^c \cup B^c$.
## Using Set Algebra
So far we've look at a bunch of different laws, and proved the truth of some of them. Now we are going to see how we can use these different laws in order to prove certain identities.

We are going to prove the following theorem, $(A\cap B^c) \cup (B\cap A^c)=(A\cup B)\cap (A\cap B)^c$.
Or order to do this we need to start with one side of this equation, and manipulate it using the laws we have discussed so far in order to show that it is the same as the other side.

So if we start with the right side:
	$(A\cup B)\cap (A\cap B)^c$
	$=(A\cup B)\cap (A^c\cup B^c)$ by De Morgan's Law
	$=((A\cup B)\cap A^c)\cup((A\cup B)\cap B^c)$ By distributing $\cap$ over $\cup$.
	= $((A\cap A^c)\cup(B\cap A^c)\cup((A\cap B^c)\cup(B\cap B^c))$ By distributing $\cap$ over $\cup$
	= $(\emptyset \cup (B\cap A^c))\cup((A\cap B^c) \cup \emptyset)$ by complement law
	= $(B\cap A^c) \cup (A\cap B^c)$ by identity law
	= $(A\cap B^c) \cup (B\cap A^c)$ by commutative law
	Therefore $(A\cap B^c) \cup (B\cap A^c)=(A\cup B)\cap (A\cap B)^c$

If you're struggling to notice exactly how we can use these identities at each step, the best thing to do it just practice. Go to the [textbook](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://digilib.stekom.ac.id/assets/dokumen/ebook/feb_ffa40f116d4322d430e4d4ff287f156f5b2aff8c_1659617647.pdf&ved=2ahUKEwjBnLaN-dORAxVYaEEAHempNIcQFnoECCQQAQ&sqi=2&usg=AOvVaw3_povfGh3w5nPLTmc6Y68K) chapter 6 and look for exercises that will help you practice this.


