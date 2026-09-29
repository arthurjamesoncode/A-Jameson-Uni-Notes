## Deriving Assertions Unary Knowledge Bases
At the end of the last lecture, [[Lecture 10 - Knowledge Representation and Reasoning]], we saw an algorithm for deriving assertions given a knowledge base.

Now we will look at some examples.
### Example 1
Let
- $K_a=\{A_1(a)\}$
- $K_r=\{A_1(x)\to A_2(x), A_2(x)\to A_3(x)\}$
- $K$ be a knowledge base only containing $K_a$ and $K_r$

The process to derive all of the assertions that are part of $K$ is:
- First set $DerivedAssertions=K_a$
- Then apply $A_1(x)\to A_2(x)$ to $A_1(a)$, which adds $A_2(a)$ to $DerivedAssertions$
- Then apply $A_2(x)\to A_3(x)$ to $A_2(a)$, which adds $A_3(a)$ to $DerivedAssertions$
- Now, as no rule can be applied, we finish and return $DerivedAssertions$.

Therefore$$DerivedAssertions=\{A_1(a),A_2(a),A_3(a)\}$$
is returned.
### Example 2
Let
- $K_a=\{A_1(a)\}$
- $K_r=\{A_1(a)\to A_2(a), A_2(a)\land B(a)\to A_3(a)\}$ 
- $K$ be a knowledge base containing only $K_a$ and $K_r$

The process to derive all of the assertions that are part of $K$ is:
- First set $DerivedAssertions=K_a$
- Then apply $A_1(a)\to A_2(a)$ to add $A_2(a)$ to $DerivedAssertions$.
- Now, as $B(a)\notin DerivedAssertions$, we have no rules which can be applied. So we finish and return $DerivedAssertions$.

Therefore $$DerivedAssertions=\{A_1(a),A_2(a)\}$$
is returned.
### Example 3
Let $$K_a=\{A_2(b),A_1(c),A_2(c)\}$$
$$K_r = \{A_1(x)\land A_2(x)\to A_3(x),A_3(x)\to A_4(x), A_4(x)\land A_1(x)\to A_5(x), A_2(x)\to A_4(x)\}$$
And let $K$ be a knowledge base containing only $K_a$ and $K_r$.

The process to derive all of the assertions that are part of $K$ is:
- First set $DerivedAssertions=K_a$
- Then apply $A_1(c)\land A_2(c)\to A_3(c)$ to add $A_3(c)$ to $DerivedAssertions$.
- Then apply $A_3(c)\to A_4(c)$ to add $A_4(c)$ to $DerivedAssertions$.
- Then apply $A_4(c)\land A_1(c)\to A_5(c)$ to add $A_5(c)$ to $DerivedAssertions$.
- Then apply $A_2(b)\to A_4(b)$ to add $A_4(b)$ to $DerivedAssertions$
- Now, we have no rules which can be applied. So we finish and return $DerivedAssertions$.

Therefore $$DerivedAssertions=\{A_1(c),A_2(c),A_3(c),A_4(c),A_5(c),A_2(b),A_4(b)\}$$
is returned.

So now, if asked, we can say that
- $K\not\models A_5(b)$
- $K\models A_5(c)$
### Time and Space Complexity
For our algorithm to compute derived assertions we define the time and space complexity as follows:
- Time complexity is the number of times a new assertion is added to $DerivedAssertions$. Note that ignore checking if we can apply a rule or not.
- Space complexity is the final size of $DerivedAssertions$. Note that $DerivedAssertions$ only grows, it does not shrink.

Let $K$ consist of $K_a$ and $K_r$. By $I_{K_a}$ we denote the individual names in $K_a$. By $|M|$ we denote the number of elements of a set $M$. So:
- $|K_a|$ is the number of atomic assertions in $K_a$
- $|K_r|$ is the number of rules in $K_r$
- $|I_{K_a}|$ is the number of individual names in $K_a$

This means that the number of times an assertion is added to $DerivedAssertions$ is $\leq |I_{K_a}|\times|K_r|$, and the total number of assertions in $DerivedAssertions$ is $\leq|K_a|+|I_{K_a}|\times |K_r|$.

So, in the worst case:
- Time Complexity $=|I_{K_a}|\times|K_r|$
- Space Complexity $=|K_a|+|I_{K_a}|\times |K_r|$

>Note we have seen this notation in [[Lecture 14 - The Cardinality of Sets]] of the COMP109 module.

