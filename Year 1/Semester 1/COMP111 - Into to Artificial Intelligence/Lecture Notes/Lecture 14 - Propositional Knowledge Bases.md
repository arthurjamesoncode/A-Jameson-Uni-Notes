>A lot of this lecture covers the same or similar content form [[Lecture 25 - Propositional Logic]] from the COMP109 Module.
## Satisfiability
A propositional formula is satisfiable if, and only if, there exists a an interpretation $I$ under which it is true.

All atomic propositions are inherently satisfiable, and most compound ones are two. However some are not.

For example, $(p\land \lnot p)$ is not satisfiable, because $I(p\land \lnot p)=0$ for all interpretations $I$.

You can see this in the following truth table.

| $p$ | $\lnot p$ | $(p\land \lnot p)$ |
| --- | --------- | ------------------ |
| 1   | 0         | 0                  |
| 0   | 1         | 0                  |

To show that a formula $P$ is satisfiable, you simply need to find an interpretation $I$ for which $I(P)=1$. To show that a formula $P$ is not satisfiable, however, you need to find every interpretation $I$ and show that for $I(P)=0$ for all $I$.

Problem "Show that $P=(p_1\implies (p_2\land \lnot p_2))$ is satisfiable".

To do this we just find an interpretation for which $P$ is true. Since $p\implies q$ is always true whenever $I(p)=0$, this means that $I(P)=0$ whenever $I(p_1)=0$. Since we have found an interpretation, we know that $P$ is satisfiable.

Problem "Show that $P = (p_1\iff ((p_2\land \lnot p_3)\land p_4))$ is satisfiable".

Again all we need to do is find an interpretation $I$ for which $P$ is true. Since $p\iff q$ is true whenever $I(p)=I(q)$ we need to find an interpretation where $I(p_1) = I(((p_2\land \lnot p_3)\land p_4))$.

If $I(p_2)=0$ then we know that $I(((p_2\land \lnot p_3)\land p_4))=0$ so when $I(p_1)=0$ and $I(p_2)=0$, $I(P)=1$. Therefore $P$ is satisfiable.

In these examples, it is relatively easy to determine whether something is satisfiable. However since there are $2^n$ interpretations of $P$ given $P$ contains $n$ atomic propositions, this means it becomes impractical very quickly to check whether $P$ is satisfiable.

Even for small $n$ such as $n=100$ it is entirely infeasible.

There has been a lot of progress when it comes to developing very fast satisfiability checking algorithms (called SAT solvers) that can deal with formulas containing very large numbers of atomic propositions. These use heuristics.
## Propositional Knowledge Bases
A propositional knowledge base $X$ is a finite set of propositional formulas.

We say a propositional formula $P$ follows from $X$ if $I(Q)=1$ for every formula $Q\in X$ then $I(P)$=1
as well.

We denote this with $X\models P$.

For example recall example from [[Lecture 13 - Propositional Logic]]:
- The meeting takes place if all members have been informed in advance, and it is quorate. 
- It is quorate provided that there are at least 15 people present. 
- Members will have been informed in advance if there is not a postal strike. 

We can label the atomic propositions like so:
- $m:$ the meeting takes place
- $a:$ all members are informed in advance
- $p:$ there is a postal strike
- $q:$ the meeting is quorate
- $f:$ there are at least 15 members present

Which allows us to rewrite the sentences of the original sentence like so:
- If $a$ and $q$ then $m$.
- If $f$ then $q$
- If not $p$ then $a$

We can say that the statement given corresponds to the following logic base $$
X=\{((a\land q)\implies m), (f\implies q), (\lnot p\implies a)\}
$$ Given this we can check if the conclusion from the original example "If the meeting does not take place, we conclude that there were fewer than 15 members present, or there was a postal strike." (or $(\lnot m\implies (p\lor \lnot f))$), follows from this knowledge base.

We can check this using a truth table, but for this example it would require a table with $2^5=32$ rows since we have 5 atomic propositions. Here we need to manipulate the propositions to get to $(\lnot m\implies (p\lor \lnot f))$.

We can do this like so:
- Since $((a\land q)\implies m)$ we know $(\lnot m\implies \lnot(a\land q))$
- Since $(\lnot m\implies \lnot(a\land q))$ we know $(\lnot m\implies (\lnot a\lor \lnot q)))$
- Since $(f\implies q)$ we know $(\lnot q \implies \lnot f)$
- Since $(\lnot p\implies a)$ we know $(\lnot a\implies p)$
- Since $(\lnot q \implies \lnot f)$, $(\lnot a\implies p)$, and $(\lnot m\implies \lnot a\lor \lnot q))$ we know $(\lnot m\implies (p\lor \lnot f))$

>This shows you how you can figure out if something follows from a knowledge base without a truth table, but most of the Boolean algebra laws that you would use to do this are not taught in this module and so you will not need to understand them for the exam.
### Examples
Problem "Show $\{(p_1\land p_2)\}\models (p_1\lor p_2)$".

To do this we can just write a truth table. The relevant truth table is below.
![[follows_truth_table_1.png]]

Since whenever $I(p_1\land p_2)=1$, $I(p_1\lor p_2)=1$ also, we know that $\{(p_1\land p_2)\}\models (p_1\lor p_2)$.

Problem "Show $\{(p_1,p_1\implies p_2)\}\models p_2$".

Again we just need to complete a truth table. Which we can see below.
![[follows_truth_table_2.png]]

Since whenever $I(p_1)=1$ and $I(p_1\implies p_2)=1$ it's also true that $I(p_2)=1$, we know that $p_2$ follows from this knowledge base. Therefore $\{(p_1,p_1\implies p_2)\}\models p_2$
### Complex Follows From Checks
Again, since there are $2^n$ interpretations for a knowledge base containing $n$ propositional atoms, it is infeasible to use a truth table to check whether a proposition follows from a knowledge base, even from relatively small $n$ such as $n=100$.

However we can check if a proposition $P$ follows from a knowledge base $X$ by using a SAT Solver.

Let $X$ contain $Q_1,...,Q_n$ and $A=Q_1\land ... \land Q_n \land \lnot P$

Since $X\models P$ if and only if $I(P)=1$ for all interpretations $I$ such that $I(Q)=1$ for all $Q\in X$, to show $X\models P$ it suffices to show that $A$, as defined above, is not satisfiable.