When faced with new problem we consider all of the KR languages that we know. Whether we can use a language or not depends on whether a language is sufficiently expressive or not.

## Example 1
Recall, as an example, this statement:
- The meeting takes place if all members have been informed in advance, and it is quorate. 
- It is quorate provided that there are at least 15 people present. 
- Members will have been informed in advance if there is not a postal strike. 
- Therefore, if the meeting does not take place, we conclude that there were fewer than 15 members present, or there was a postal strike."

Last lecture, [[Lecture 14 - Propositional Knowledge Bases]], we discussed how this statement can be modelled as a propositional knowledge base. Since this statement uses conjunction, negation and disjunction, we cannot represent it with our Unary, or Binary knowledge bases, and must represent it with a propositional knowledge base.
## Example 2
Recall the following knowledge base from [[Lecture 10 - Knowledge Representation and Reasoning]]:
- If I have an AI lecture today, then it is Tuesday or Friday.
- It is not Tuesday.
- I have an AI lecture today or I have no class today. 
- If I have no class today, then I am sad. 
- I am not sad. 

Again this knowledge base contains disjunction and negation, concepts which we can only model with a propositional knowledge base. You can see how we model this below.

First we provide labels to the atomic propositions:
- $a$ - I have an AI lecture today
- $t$ - It is Tuesday
- $f$ - It is Friday
- $c$ - I have a class today
- $s$ - I am sad

We can then say the knowledge base contains the propositions:
- $(a\implies (t\lor f))$
- $\lnot t$
- $(a\lor \lnot c)$
- $(\lnot c\implies s)$
- $\lnot s$
## Example 3
Recall the following medical knowledge base from [[Lecture 10 - Knowledge Representation and Reasoning]]:
- Pericardium is a tissue contained in the heart 
- Pericarditis is an inflammation located in the pericardium
- Inflammation is a disease that acts on tissue 
- A disease located in something contained in the heart is a heart-disease

If we try to model this with propositional logic alone, we see that we can't. Propositional logic does not allow us to say "any $x$ is also $y$" and so we must model it with one of our class based KR languages. 

A unary language is all that is actually needed as we modelled this using a unary language in [[Lecture 10 - Knowledge Representation and Reasoning]], but we can be a bit more expressive if we use a binary language.

So we could represent the medical knowledge base above with the following knowledge base, $K$:
- $Tissue(Pericardium)$, 
- $ContinHeart(Pericardium)$
- $Inflammation(Pericarditis)$ 
- $LocatedIn(Pericarditis,Pericardium)$ 
- $Inflammation(x) \implies Disease(x)$
- $Disease(x) \land LocatedIn(x, y) \land contInHeart(y) \implies Heartdisease(x)$

If you compute derived assertions on this knowledge base we can see $$K\models Heartdisearse(Pericarditis)
$$
### Example 4
All of the examples we have done so far are pretty easy, however this is not always the case.

Consider a sudoku.
![[sudoku.png]]

To model a sudoku, we need a knowledge base that reflects the following:
- Every cell must have at least 1 number
- No cell can have more than 1 number
- No number can be repeated in a column
- No number can be repeated in a row
- No number can be repeated in a region

To model this, we need a concept for not and so the only KR language available to us is propositional logic.

If $p_{xyz}$ stands for "number $x$ is in cell $(y,z)$" where $y$ is the row and $z$ is the column of the cell then we can model all the statements we said above:
-  Every cell must have at least 1 number: For all $y,z$, $$
p_{1yz}\lor p_{2yz} \lor p{9yz}
$$
- No cell can have more than 1 number: For all $y,z$ $$
\lnot(p_{1yz} \land p_{2yz}), \lnot(p_{1yz} \land p_{3yz}), . . .
$$
- No number can be repeated in a column: For all $y\neq y'$ and $z$ $$
¬(p_{1yz} ∧ p_{1y′z} ), \lnot(p_{2yz} ∧ p_{2y ′z}), . . .
$$
- No number can be repeated in a column: For all $y$ and $z\neq z'$ $$
¬(p_{1yz} ∧ p_{1yz'}), ¬(p_{2yz} ∧ p_{2yz'}), . . .
$$
And lastly: No number can be repeated in a region, this one requires a bit of maths to figure out a way to distinguish regions in terms of $y$ and $z$. 

If we assume rows indexed $(0\to8)$ and columns indexed $(0\to 8)$, we can a way to calculate a box index given $x$ and $y$. 

Below you can see our target box indexes, along with the indexes of the corresponding rows and columns.
![[box_index.png.jpg]]

We will denote the integer division, that is division in which the remainder is discarded as, $a//b$.

You may notice that the target indexes in the first row are the same as the integer division of the column index by 3 or $col//3$. You may also notice that the target indexes in the second row are the same as $(col//3) + 3$ and that the target indexes in the last row are the same as $(col//3) + 6$.

The numbers we are adding is the same as if we $(row//3)*3$ where row is the row index. So we can define a $boxIndex$ function which gives us the index of a box. $$
boxIndex(row,col)=(col//3)+3(row//3)
$$
Using this $boxIndex$ function we can define our propositions for the region as this: For all $y,z$ such that $boxIndex(y,z)\neq boxIndex(y',z')$ $$
¬(p_{1yz} ∧ p_{1y'z'}), ¬(p_{2yz} ∧ p_{2y'z'}), . . .
$$
We would also need to include all of the positions that are currently filled. So we would need $p_{312}$ for example, along with all other filled squares.

Modelling a sudoku like this means that we could check if any individual propositions, such as $p_{277}$ follow from the full knowledge base by using the satisfiability checker method discussed in [[Lecture 14 - Propositional Knowledge Bases]].