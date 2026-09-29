## Circuit Equivalence
Two circuits are equivalent if they produce the same output given the same inputs.

For example, lets revisit one of the examples from [[Lecture 25 - Propositional Logic]].
![[equiv_circuits.png]]
Here we can see 2 circuits from last lecture's example. We showed that these 2 circuits are equivalent at the end of last lecture.

We also know that the corresponding formulas of these circuits are equivalent. So we know that $((P\land Q\land R)\lor(P\land\lnot Q\land R)\lor(P\land Q \land\lnot R))\equiv(P\land (Q\lor R))$

>$\equiv$ is the symbol for logical equivalence.

To formally define logical equivalence: "Two formulas $P$ and $Q$ are called equivalent if they have the same truth value under every possible interpretation. In other words, $P\equiv Q\iff \forall I,\; I(P)=I(Q)$"

We can prove that the relation $\equiv$ is an equivalence relation on $P$ like so:
- $\equiv$ is reflexive, since, trivially, $I(P) = I(P)$ for every interpretation $I$. 
- $\equiv$ is transitive, since $P\equiv Q$ and $Q\equiv R \implies P\equiv R$. 
- $\equiv$ is symmetric, since $P \equiv Q \implies Q \equiv P$.
## Boolean Algebra Laws
We can use laws of Boolean algebra to simplify many formulas. A lot of these laws are very similar to the laws we discussed when it came down to set algebra in [[Lecture 13 - The Algebra of Sets]].

I went over, in detail, what different properties of operations meant there. In this I am simply going to reiterate some of the important equalities.

### Associative Laws:
For associative operations, the order in which operations are grouped by brackets does not matter.

$\land$ and $\lor$ are both associative and so:
- $(P\lor(Q\lor R))\equiv((P\lor Q)\lor R)$
- $(P\land(Q\land R))\equiv((P\land Q)\land R)$
### Commutative Laws
For commutative operations, the order of the operands does not matter.

$\land$ and $\lor$ are both commutative and so:
- $(P\lor Q)\equiv(Q\lor P)$
- $(P\land Q)\equiv(Q\land P)$
### Identity Laws
Identity laws describe ways in which a proposition $P$ interacts with the identities $\top$ and $\bot$.

The identity laws are:
- $(P\lor\bot)\equiv P$
- $(P\lor\top)\equiv\top$
- $(P\land\top)\equiv P$
- $(P\land\bot)\equiv\bot$

>$\top$ is a special proposition which is always true, and $\bot$ is a special proposition which is always false.
### Distributive Laws
Some operations are distributive over other operations. This means that the effect of the operation can be spread over the operands of the other operation.

$\land$ and $\lor$ and both distributive over each other and so:
- $(P\land(Q\lor R))\equiv((P\land Q)\lor(P\land R))$
- $(P\lor(Q\land R))\equiv((P\lor Q)\land(P\lor R))$

>You can think of distributive laws like you would factoring.
## Complement Laws
Complement laws describe the ways in which propositions interact with their negations.

The complement laws are:
- $(P\lor\lnot P)\equiv\top$
- $(\lnot\top)\equiv\bot$
- $(\lnot\lnot P)\equiv P$
- $(P\land\lnot P)\equiv\bot$
- $(\lnot\bot)\equiv\top$

### De Morgan's Laws
De Morgan's laws describe how negation interacts with and and or.

De Morgan's laws are:
- $\lnot(P\lor Q)\equiv(\lnot P\land\lnot Q)$
- $\lnot(P\land Q)\equiv(\lnot P\lor\lnot Q)$

>Essentially whenever applying a $\lnot$ to a bracket, we can apply it to the individual propositions and flip the operation.
## Boolean Functions of Arity 2
Arity refers to the number of arguments of a function.

There are exactly 16 possible Boolean functions that take 2 arguments, or are of arity 2. Why 16?

We can see why by just listing all the possible outcomes of 2 variables.
![[boolean_arity_2.png]]
Here we can see the 16 possible Boolean functions with an arity of 2. The reason there is only 16 is because there are 4 combinations of inputs when you have 2 inputs. You can see this by just looking at the 4 rows in these tables. 

This means that the outputs of a function that takes 2 arguments is the same as a bit string of length 4. This means that there are $2^4$ possible function outputs, and therefore $2^4$ or 16 functions.

You can generalise this by number of inputs as the possible combinations for $n$ inputs is $2^n$. This means that the number of possible Boolean functions of arity $n$ is $2^{(2^n)}$.
## Logic Gate Symbols
Below is a figure showing all the symbols used for various logic gates. The truth tables for these gates have been covered in [[Lecture 25 - Propositional Logic]], so I will not bother going over them again.
![[logic_gate_symbols.png]]
>One thing worth mentioning is that the bottom row are simply negated versions of AND, OR, and XOR.
## Universality of NAND and NOR
NAND and NOR are 2 new gates visible in the above figure. They also have their own symbols.
- $(\lnot(P\land Q))\equiv(P\;|\;Q)$
- $(\lnot(P\lor Q))\equiv(P\downarrow Q)$

NAND gates are universal, meaning that they can create all other types of circuits.

View the figure below to see how NAND can be used to make NOT, AND, and OR gates.
![[universal_nand.png]]As an exercise see if you can create these same three gates but only using NOR gates.
## Number Systems
We need to know how to convert between number systems, namely binary and decimal, when working with computers. This is because computers operate with binary representations of numbers.

Both binary and decimal are positional number systems, meaning that you multiply each value by its place value.

For example in decimal: $$
4268_{10}=4\cdot10^3 + 2\cdot 10^2 + 6\cdot10^1 + 8\cdot10^0
$$
And in binary:$$
11000111_2=1\cdot2^7 + 1\cdot2^6 + 0\cdot2^5 + 0\cdot2^4 + 0\cdot2^3 + 1\cdot2^2 + 1\cdot2^1 + 1\cdot2^0 = 128 + 64 + 4 + 2 + 1 = 199_{10}
$$
>Here we have used a subscript of 10 and 2 to highlight the base of the number system. Decimal is base 10, and binary is base 2.
### Converting Between Binary and Decimal
To convert from binary to decimal you multiply each position by its place value as shown above.

To convert from decimal to binary I will give you 2 ways.
#### Method 1
Continue to divide by 2, noting the remainder at each step. Then write down the remainders from each stage right to left.

For example take 533, to turn this into a binary number we do as follows.
- $533/2=266$ remainder 1
- $266/2=133$ remainder 0
- $133/2=66$ remainder 1
- $66/2=33$ remainder 0
- $33/2=16$ remainder 1
- $16/2=8$ remainder 0
- $8/2=4$ remainder 0
- $4/2=2$ remainder 0
- $2/2=1$ remainder 0
- $1/2=0$ remainder 1

You can then write down all the remainders from each stage from right to left. 

So $533_{10}=1000010101_2$.
#### Method 2
Continually subtract the greatest power of 2 possible from the number. Whenever you subtract a power of 2 place a 1 in the location with the same place value.

For example take 533, to turn this into a binary number we do as follows:
- $533 - 2^9=533-512=21$ 
- $21 - 2^4=21-16=5$
- $5-2^2=5-4=1$
- $1-2^0=1-1=0$

Once we reach 0, we stop and we construct the numbers from the place values of the numbers we subtracted. So a 1 goes in the 0th spot since we subtracted $2^0$, a 1 goes in the 10th spot since we subtracted $2^9$ etc.

And what we get is $533_{10}=1000010101_2$.

Both of these methods work, you should use whichever is easiest for you to remember and implement.