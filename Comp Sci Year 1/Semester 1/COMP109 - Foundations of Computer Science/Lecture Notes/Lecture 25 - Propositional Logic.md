For the sake of containing different topics to different notes, I have included some content from the last lecture in the notes for this one instead.
## Propositional Logic
Logic is concerned with the truth and falsity of statements, as well as when does a statement follow from a set of statements. Exactly what this means we will come back to.

A proposition is a statement that can be either true or false, but not both.

For example:
- I eat toast
- $2+3=5$
- $2\cdot 2=4$
- Logic is easy

These are all examples of "atomic" propositions. Exactly what this means will be discussed when talking about compound propositions.

Things that aren't propositions are things like:
- $4+5$ -This is an expression
- What is the capital of the UK? -This is a question
## Compound Propositions
We can use logical connectives (or Boolean connectives) to form more complex propositions.

The basic logical connectives and their symbols are:
1. Negation, $\lnot$, read "not".
2. Conjunction, $\land$, read "and".
3. Disjunction, $\lor$, read "or".
4. Implication, $\implies$, read "implies" or "if...then"
5. Equivalence, $\iff$, read "if, and only if,"

Propositions formed using these connectives are called compound propositions. If no connectives are used, they are called atomic propositions.

Any propositional formula is either an atomic or compound proposition.
## Truth Values and Tables
An interpretation $I$ is a function which assigns to any atomic proposition $p_i$ a truth value, either $0$ or $1$.

$I(p_i)\in \{0,1\}$
- If $I(p_i)=1$ then $p_i$ is called true under the interpretation $I$.
- If $I(p_i)=0$ then $p_i$ is called false under the interpretation $I$.

Given an assignment of $I$ we can compute the truth value of compound formulas step by step using truth tables.
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
### Computing Truth Values
Given an interpretation, $I$, we can compute the truth value of any formula $P$ under $I$.
- If $I(P)=1$ then $P$ is called true under the interpretation $I$.
- If $I(P)=0$ then $P$ is called false under the interpretation $I$.

For example take $P=((p\lor \lnot q)\land r)$. If we fill out a truth table, we will know all of the interpretations of $p$, $q$, and $r$ such that $I(P)=1$

| $p$ | $q$ | $r$ | $\lnot q$ | $(p\lor \lnot q)$ | $((p\lor \lnot q)\land r)$ |
| --- | --- | --- | --------- | ----------------- | -------------------------- |
| 1   | 1   | 1   | 0         | 1                 | 1                          |
| 1   | 1   | 0   | 0         | 1                 | 0                          |
| 1   | 0   | 1   | 1         | 1                 | 1                          |
| 1   | 0   | 0   | 1         | 1                 | 0                          |
| 0   | 1   | 1   | 0         | 0                 | 0                          |
| 0   | 1   | 0   | 0         | 0                 | 0                          |
| 0   | 0   | 1   | 1         | 1                 | 1                          |
| 0   | 0   | 0   | 1         | 1                 | 0                          |
We can see from this table that $I(P)=1$ when $I(p)=1, I(q)=1,I(r)=1$ or $I(p)=1,I(q)=0,I(r)=1$ or $I(p)=0,I(q)=0,I(r)=1$.
## Solving Logical Puzzles
Now we will look at how we can solve a logical puzzle by using propositional logic.
### Puzzle 1
The puzzle is as follows:
"An island has two kinds of inhabitants, knights, who always tell the truth, and knaves, who always lie. 

You go to the island and meet A and B. 

A says “B is a knight.” 
B says “The two of us are of opposite types.” 

What are A and B?"

We can now model this problem by using propositional logic.

First we need to establish some atomic propositions:
- $p:$ "A is a knight"
- $q:$ "B is a knight"

We know that $p$ and $q$ are either true or false. We also know what $p$ and $q$ imply based on what A and B said:
- Since A said "B is a knight", we know that $p\implies q$ as if A is a knight they will be telling the truth.
- We also know that $\lnot p\implies \lnot q$ as if A is a knave they will be lying.
- Since B said "The two of us are of opposite types", we know that $q\implies \lnot p$ since if B is a knight they would be telling the truth, meaning that A is a knave.
- We also know that $\lnot q\implies \lnot p$ since if B is a knave, they will be lying meaning that $A$ is also a knave.

Here we have 4 compound propositions that we know must be true:
- $p\implies q$
- $\lnot p\implies \lnot q$
- $q\implies \lnot p$
- $\lnot q\implies \lnot p$

You may be able to make some deductions about what $I(p)$ and $I(q)$ must be, but the simplest way to discover what they must be is to write a truth table.

| $p$ | $q$ | $\lnot p$ | $\lnot q$ | $p\implies q$ | $\lnot p\implies \lnot q$ | $q\implies \lnot p$ | $\lnot q\implies\lnot p$ |
| --- | --- | --------- | --------- | ------------- | ------------------------- | ------------------- | ------------------------ |
| 1   | 1   | 0         | 0         | 1             | 1                         | 0                   | 1                        |
| 1   | 0   | 0         | 1         | 0             | 1                         | 1                   | 0                        |
| 0   | 1   | 1         | 0         | 1             | 0                         | 1                   | 1                        |
| 0   | 0   | 1         | 1         | 1             | 1                         | 1                   | 1                        |
As we can see from the truth table, those 4 propositions that we know are true can only all be true when $I(p)=0$ and $I(q)=0$ meaning that both A and B must be knaves.
### Puzzle 2
The next puzzle is as follows:

Alice and Bob both choose an integer from {1,2,...,30}. Alice and Bob do not know each others numbers, but they do know their own. 

We hear the following conversation:
A: "Is your number twice my number?"
B: "I don't know. Is your number twice my number?"
A: "I don't know. Do we have the same number?"
B: "Yes we do."

What number do Alice and Bob have?

This is a slightly different question to the other one, as we won't be using a truth table. The core of this question is recognising that we gain information when Alice and Bob say "I don't know".

Let a = Alice's Number, and b = Bob's number.

After Alice asks "Is your number twice my number" and Bob replies "I don't know", we gain some information:
- $a\leq 15$ as otherwise Alice would know that Bob couldn't have twice her number.
- $b$ is even as otherwise Bob would know that his number is not twice Alice's number.

When Bob asks "Is your number twice my number?" and Alice replies "I don't know", we gain some more information:
- $b\leq 7$ as otherwise $2b > 15$ and Bob would know that Alice did not have twice his number and he would not ask the question.
- $a$ is twice some even number less than or equal to $7$, as Alice knows that $b\leq 7$ and $b$ is even. If wasn't twice some number in this range then she would know that her number is not twice his number.

When Alice asks "Do we have the same number?" we gain information yet again:
- This confirms that $a\leq 7$ as it must be in the same range as $b$ for Alice to ask this question. Otherwise she would know that they don't have the same number.
- Since $a\leq 7$ and $a$ is twice some even number less than or equal to $7$, we know that $a=4$ as 4 is the only number for which both those propositions are true.

When Bob replies with "Yes we do." it tells us that Bob also knows that Alice has 4, and that Bob has 4 as well.

And so we know that Alice and Bob both picked 4.
## Semantic Consequence
Suppose $\Gamma$ is a finite set of formulas and $P$ is a formula. In this case, $P$ is a **semantic consequence of** $\Gamma$ if the following implication holds for every interpretation $I$:$$\forall Q\in\Gamma,\;I(Q)=1\implies I(P)=1$$
When $P$ is a **semantic consequence** of $\Gamma$ we say that $P$ follows from $\Gamma$ which is denoted by $\Gamma\models P$.

For $I(\;\Gamma\models P\;)=1$ to be true, $I(P)=1$ must be true whenever a formula in $\Gamma$ is true.

### Example 1
Let $\Gamma = \{(p_1\land p_2)\},\; P=(p_1\lor p_2)$.

To show $\Gamma\models P$ we can write a truth table.

| $p_1$ | $p_2$ | $(p_1\land p_2)$ | $(p_1\lor p_2)$ | $((p_1\land p_2)\implies(p_1\lor p_2))$ |
| ----- | ----- | ---------------- | --------------- | --------------------------------------- |
| 1     | 1     | 1                | 1               | 1                                       |
| 1     | 0     | 0                | 1               | 1                                       |
| 0     | 1     | 0                | 1               | 1                                       |
| 0     | 0     | 0                | 0               | 1                                       |
As you can see $((p_1\land p_2)\implies(p_1\lor p_2))$ is true for all interpretations of $p_1$ and $p_2$. Essentially whenever there is a 1 in the $(p_1\land p_2)$ column there is also a 1 in the $(p_1\lor p_2)$ column.
### Example 2
Let $\Gamma = \{p_2\},\; P = p_2$.

We can show that $\Gamma\not\models P$ by writing a truth table.

| $p_1$ | $p_2$ | $p_1\implies p_2$ |
| ----- | ----- | ----------------- |
| 1     | 1     | 1                 |
| 1     | 0     | 0                 |
| 0     | 1     | 1                 |
| 0     | 0     | 1                 |
We can see that $p_1\implies p_2$ is not true for all interpretations of $p_1$ and $p_2$ as when $p_1$ is true $p_2$ can be false and so $\Gamma\not\models P$.
### Example 3
Let $\Gamma=\{p_1\},\; P=(p_1\lor p_2)$

We can show that $\Gamma\models P$ by writing a truth table.

| $p_1$ | $p_2$ | $(p_1\lor p_2)$ | $(p_1\implies (p_1\lor p_2))$ |
| ----- | ----- | --------------- | ----------------------------- |
| 1     | 1     | 1               | 1                             |
| 1     | 0     | 1               | 1                             |
| 0     | 1     | 1               | 1                             |
| 0     | 0     | 0               | 1                             |
We can see that $(p_1\implies (p_1\lor p_2))$ is true for all interpretations of $p_1$ and $p_2$ as when $p_1$ is true $p_1\lor p_2$ must be true and so $\Gamma\models P$.
## Logic and Proof Principles
We can rephrase many ideas we learnt about when writing proofs by using propositional logic and semantic consequence.

### Modus Ponens (Direct Proof)
Direct proof corresponds to the following semantic consequence$$
\{P,(P\implies Q)\}\models Q
$$
### Reducto ad Absurdum (Proof by Contradiction 1)
Proof by contradiction corresponds to $$
\{(\lnot P\implies \perp \}\models P
$$
>$\perp$ is a special proposition, which is false under every interpretation.
### Modus Tollens (Proof by Contradiction 2)
Another semantic consequence that proof by contradiction corresponds to is$$
\{(P\implies Q),\lnot Q\}\models \lnot P
$$
### Case Analysis
Case analysis corresponds to $$
\{(P\implies Q),(R\implies Q), (P\lor R)\}\models Q
$$
This can be extended into 3 or more cases as well.
### Proof Theory
We have studied proofs as carefully reasoned arguments to convince a sceptical listener that a given statement is true. These are called “Social” proofs. 

Proof theory is a branch of mathematical logic dealing with proofs as mathematical objects 
- Strings of symbols
- Rules for manipulation 

With proof theory mathematics becomes a ‘game’ played with strings of symbols which can be read and interpreted by computer.
## Digital Circuits
Electric circuits are often constructed in ways that mirror propositional logic. For an example check the circuits below.
![[Electric circuits.png]]
The left circuit mirrors the behaviour of the **logical and** operation and the right circuit mirrors the behaviour of a **logical OR** operation. With closed and on being 1, and open and off being 0.
### Logic Gates
Logic gates are used for building digital circuits. Check the figure below for images of 3 of the main logic gates.
![[logic_gates.png]]We can use gates like these to build up more complex combinatorial circuits, that take a variable number of inputs and return 1 or more outputs.

The rules for constructing a combinatorial circuit are as follows:
- Never combine two input wires. 
- A single input wire can be split partway and used as input for two separate gates. 
- An output wire can be used as input. 
- No output of a gate can eventually feed back into that gate.

If we look at the figure below we can start to see how we can read these circuit diagrams:
![[circuit_example_1.png]] 

The first diagram can be written as $R=(\lnot P \land Q)$, and the second can be written as $S= (\lnot(P\lor Q)\land R)$.

If we substitute in the input signals written above each diagram we can see that $R=1$ in the first circuit and $S=0$ in the second circuit.

If we work from the other way, we can create circuits based on propositional formulas.

For example $(\lnot P \land Q)\lor\lnot Q$ corresponds to the following circuit
![[drawn_circuit_1.drawio.png]]

And and or gates can also take more than 2 inputs for example:
![[multi_input_gate.png]]
### Disjunctive Normal Form
Disjunctive normal form is a type of circuit which can be built from a truth table.

Take the following table, where $P$, $Q$, and $R$ are the inputs and $S$ is the output.

| $P$ | $Q$ | $R$ | $S$ |
| --- | --- | --- | --- |
| 1   | 1   | 1   | 1   |
| 1   | 1   | 0   | 0   |
| 1   | 0   | 1   | 1   |
| 1   | 0   | 0   | 0   |
| 0   | 1   | 1   | 1   |
| 0   | 1   | 0   | 0   |
| 0   | 0   | 1   | 1   |
| 0   | 0   | 0   | 0   |
To get the DNF of the circuit for this table we simply look at all the cases in which the output is 1 and connect them with $\lor$.

So the DNF for this circuit is $(P\land Q\land R)\lor(P\land\lnot Q\land R)\lor(\lnot P\land Q\land R)\lor(\lnot P\land\lnot Q\land R)$. Which when drawn as a circuit diagram is below.
![[DNF_example_1.drawio.png]]

Below is another truth table, with its DNF below and a circuit drawn to the right.
![[DNF_example_2.png]]
### Simplifying Circuits
If you look back the last 2 examples you may notice that they are not particularly size efficient.

If you look at the first example, you can see in the truth table that $S\iff R$. $S$ and $R$ always have the same value. You can see this further as if you look at the cases, as within each bracket is every combination of $P$, $Q$, and their negations. 

So we can replace $S=(P\land Q\land R)\lor(P\land\lnot Q\land R)\lor(\lnot P\land Q\land R)\lor(\lnot P\land\lnot Q\land R)$ with simply $S=R$.

Similarly the second example has a much more simple circuit diagram. We will view the specifics about how to simplify these diagrams in a different lecture.
![[simplify_example1.png]]
