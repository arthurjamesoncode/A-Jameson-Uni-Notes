>A lot of this lecture covers the same or similar content from [[Lecture 25 - Propositional Logic]] and the following lectures from the COMP109 Module.

The rules and atomic propositions we covered in the last few lectures are not really expressive enough to say what we often want to say.

For example, we can't say that something *isn't* the case like this:
- $not\; FrenchFootballClub(LiverpoolFC)$

We also can't connect propositions with words like *or*:
- $FrenchFootballClub(LiverpoolFC)\; or\; EnglishFootballClub(LiverpoolFC)$

If we create systems that can use **propositional logic** however, we can.
## Propositions
A proposition is a statement that can be either true or false, but not both.

For example:
- I eat toast
- $2+3=5$
- $2\cdot 2=4$
- Logic is easy

These are all examples of "atomic" propositions. This is what we called the assertions in our knowledge base too.

Things that aren't propositions are things like:
- $4+5$ -This is an expression
- What is the capital of the UK? -This is a question

We can build **compound propositions** from atomic propositions using various connectives.

Take for example this statement: "
- The meeting takes place if all members have been informed in advance, and it is quorate. 
- It is quorate provided that there are at least 15 people present. 
- Members will have been informed in advance if there is not a postal strike. 
- Therefore, if the meeting does not take place, we conclude that there were fewer than 15 members present, or there was a postal strike."

This is a complex statement that has many different atomic propositions baked into it. We can break it down like this.

We can label our atomic propositions like so:
- $m:$ the meeting takes place
- $a:$ all members are informed in advance
- $p:$ there is a postal strike
- $q:$ the meeting is quorate
- $f:$ there are at least 15 members present

We can now rewrite each sentence, substituting in our labels for the things they represent.

The statement is now:
- If $a$ and $q$ then $m$.
- If $f$ then $q$
- If not $p$ then $a$
- Therefore, if not $m$ then $p$ or not $f$

All these sentences are examples of compound propositions. All of them are combined using connectives.

The connectives that may be used are as follows:
- $\lnot$, not (negation)
- $\land$, and (conjunction)
- $\lor$, or (disjunction)
- $\iff$, if, and only if (equivalence)
- $\implies$, if then, (implication)

We will see more of this, as well as there in detail effects, when we get to [[#Connectives]].
## Propositional Formulas
The set of propositional formulas is defined as follows.

Every atomic proposition is a propositional formula. We denote these by $p,q,a,b,p_1$ etc.

If $P$ and $Q$ are propositional formulas then:
- $(P\land Q)$
- $(P\lor Q)$
- $(P\implies Q)$
- $(P\iff Q)$
Are all propositional formulas.

If $P$ is a propositional formula then $\lnot P$ is also a propositional formula.
## Truth Values
An interpretation I assigns to every atomic proposition $p$ a truth value. $$I(p) \in {0, 1}$$
- If $I(p) = 1$, then p is called true under the interpretation $I$.
- If $I(p) = 0$, then p is called false under the interpretation $I$. 

Given an assignment $I$ we can compute the truth value of compound formulas step by step using truth tables. A truth table is a table that shows the value of propositional formulas given every interpretation $I$. You can see examples of these as we discuss connectives below.
## Connectives
### Negation
The negation $\lnot P$ of a formula $P$ means "it is not the case that $P$".

| $P$ | $\lnot P$ |
| --- | --------- |
| 1   | 0         |
| 0   | 1         |
### Conjunction
The conjunction $(P\land Q)$ of $P$ and $Q$ means "both $P$ and $Q$ are true".

| $P$ | $Q$ | $(P\land Q)$ |
| --- | --- | ------------ |
| 1   | 1   | 1            |
| 1   | 0   | 0            |
| 0   | 1   | 0            |
| 0   | 0   | 0            |
### Disjunction
The disjunction $(P\lor Q)$ of $P$ and $Q$ means "at least one of $P$ or $Q$ is true".

| $P$ | $Q$ | $(P\lor Q)$ |
| --- | --- | ----------- |
| 1   | 1   | 1           |
| 1   | 0   | 1           |
| 0   | 1   | 1           |
| 0   | 0   | 0           |
### Equivalence
The equivalence $(P\iff Q)$ of $P$ and $Q$ means that "$P$ and $Q$ take the same truth value".

| $P$ | $Q$ | $(P\iff Q)$ |
| --- | --- | ----------- |
| 1   | 1   | 1           |
| 1   | 0   | 0           |
| 0   | 1   | 0           |
| 0   | 0   | 1           |
### Exclusive OR
The exclusive or $(P\oplus Q)$ of $P$ and $Q$ means "$P$ and $Q$ different truth values".

| $P$ | $Q$ | $P\oplus Q$ |
| --- | --- | ----------- |
| 1   | 1   | 0           |
| 1   | 0   | 1           |
| 0   | 1   | 1           |
| 0   | 0   | 0           |
### Implication
The implication $(P\implies Q)$ of $P$ and $Q$ means "if $P$ then $Q$"

| $P$ | $Q$ | $(P\implies Q)$ |
| --- | --- | --------------- |
| 1   | 1   | 1               |
| 1   | 0   | 0               |
| 0   | 1   | 1               |
| 0   | 0   | 1               |
## Examples
Now we will work through some problems.

Problem "List the interpretations $I$ such that $P = ((p_1 \land \lnot p2) \implies (p_2 \land \lnot p1))$ is true under $I$"

To solve this we first need to compute a truth table for this proposition, which we can see below.
![[truth_table_1.png]]

The way to complete this table would be to write all the combinations of interpretations of $p_1$ and $p_2$ and then use the truth tables we have above for negation, conjunction, and implication to fill out the other column.

>If you have 2 atomic propositions, then there will be 4 combinations of interpretations and therefore 4 rows of your truth table. 
>
>This can be generalised to there are $2^n$ combinations and therefore $2^n$ rows of a truth table for $n$ atomic propositions.

And so we can list that the interpretations that make $P$ true are:
- $I(p_1)=1$ and $I(p_2)=1$
- $I(p_1)=0$ and $I(p_2)=1$
- $I(p_1)=0$ and $I(p_2)=0$

Problem "How many interpretations $I$ of $p_1$, $p_2$ and $p_3$ are there such that $P = ((p_1 \lor p_2) \iff p_3)$ is true under $I$?"

For this one again we need to compute a truth table, which you can see below.
![[truth_table_2.png]]

This time we would need to list 8 rows, as there are 8 combinations of interpretations for 3 atomic propositions. We then use the truth tables for disjunction and equivalence to fill out the other columns.

After we are finished we can see that there are 4 interpretations which make $P$ true.

Problem "How many interpretations $I$ of $p_1$, $p_2$ and $p_3$ are there such that $P = ((p_1 \lor \lnot p_2) \land p_3)$ is true under $I$?"

Again, we need to compute a truth table, which you can see below.
![[truth_table_3.png]]

This time we need to list 8 rows again, and then use the truth tables for negation, disjunction and conjunction to complete the other columns.

Once complete we can see that there are 3 interpretations which make $P$ true.

