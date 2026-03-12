Sometimes, our unary knowledge bases are not enough.

Suppose we want to reason the following:
- Peter is a son of John
- John is a son of Joseph
- Therefore, Peter is a grandson of Joseph.

We can represent Peter, John, and Joseph in our knowledge base as individual names, but we haven't declared them to be part of any classes. Instead we have said that they are **related** to each other. So now, we need a way to represent these relations in our knowledge base.
## Non-Unary Knowledge Bases
These knowledge bases require names for relations in addition to names for classes.

A relation name $R$ denotes a set of pairs of individual objects. We can also call relation names **binary predicates**. 

For example:
- $sonOf$
- $grandsonOf$ 

We often denote relation names by the upper case letters $R$, $S$, $R_1$ and so on.

To express that an individual object $a$ is related to an individual object $b$ through the relation $R$ we write $R(a,b)$. So we could say, for example, $sonOf(Peter, John)$ to say that Peter is a son of John.

$R(a,b)$ is also an atomic assertion. This is because "$a$ is related to $b$" is either true or false, and relies on no other statement. The same can be said for "$b$ is a member of $A$" and the other atomic propositions we have seen so far.

A rule in this knowledge base has the form$$R_1(x_1,y_1)\land ... R_n(x_n,y_n)\land A_1(x_{n+1})\land ... \land A_m(x_{n+m})\to R(x,y)$$or$$R_1(x_1,y_1)\land ... R_n(x_n,y_n)\land A_1(x_{n+1})\land ... \land A_m(x_{n+m})\to A(x)$$ where $R_1,...,R_n$ and $R$ are relation names, $A_1,...,A_n$ and $A$ are class names, and $x_1,y_1,...,x_n,y_n,x_{n+1},...,x_{n+m},x,y$ are individual variables.

Again our rule-based knowledge base $K$ is a collection of atomic assertions $K_a$ and rules $K_r$.

For example, let $K_a$ contain: 
- $childOf(Peter, John)$
- $childOf(John, Joseph)$ 

Let $K_r$ contain:
- $childOf(x, y) \land childOf(y, z) \to grandchildOf(x, z)$
- $childOf(x,y)\to parentOf(y,x)$
- $grandchildOf(x,y)\to grandparentOf(y,z)$

We can compute assertions using the algorithm from [[Lecture 10 - Knowledge Representation and Reasoning]]. 

We can compute $derivedAssertions$ like so:
- Set $derivedAssertions=K_a$
- Apply $childOf(x, y) \land childOf(y, z) \to grandchildOf(x, z)$ to add $grandchildOf(Peter, Joseph)$
- Apply $grandchildOf(x,y)\to grandparentOf(y,z)$ to add $grandparentOf(Joseph, Peter)$
- Apply $childOf(x,y)\to parentOf(y,x)$ to add $parentOf(John, Peter)$
- Apply $childOf(x,y)\to parentOf(y,x)$ to add $parentOf(Joseph, John)$
- We now have no more rules we can apply and so we finish and return $DerivedAssertions$

Therefore$$DerivedAssertions=\{childOf(Peter, John),childOf(John, Joseph),grandchildOf(Peter, Joseph),grandparentOf(Joseph, Peter),parentOf(John, Peter),parentOf(Joseph, John)\}$$Is returned.

The only difference between this and how we derive assertions from unary knowledge bases is that we must consider relationship rules as well.
## Knowledge Graphs
Binary predicates allow us to represent our knowledge bases as graphs.

For example, let $K_a$ contain:
- $childOf(Peter,John)$
- $childOf(John,Joseph)$

And let $K_r$ contain:
- $childOf(x,y)\to descendantOf(x,y)$
- $descendantOf(x,y)\land descendantOf(y,z)\to descendantOf(x,z)$

We can compute $derivedAssertions$ like so:
- Set $derivedAssertions=K_a$
- Apply $childOf(Peter,John)\to descendantOf(Peter,John)$ to add $descendantOf(Peter, John)$
- Apply $childOf(John,Joseph)\to descendantOf(John,Joseph)$ to add $descendantOf(John, Joseph)$
- Apply $descendantOf(Peter,John)\to descendantOf(John,Joseph)$ to add $descendantOf(Peter, Joseph)$
- We now have no more rules we can apply and so we finish and return $DerivedAssertions$

Therefore $$DerivedAssertions=\{childOf(Peter,John),childOf(John,Joseph),descendantOf(Peter, John),descendantOf(John, Joseph),descendantOf(Peter, Joseph)\}$$
We can represent this knowledge base with the following graph:![[knowledge_graph.png]]
On this graph, nodes represent the individual names, and the arrows represent relations between those names. 

This can be a quick, readable way to represent a knowledge base. You will need to know how these graphs are drawn for your exam.

>Note that the black text and arrows represent the assertions present in $K_a$ and the red represent the additional assertions added after computing $DerivedAssertions$. Computing derived assertions corresponds to graph completion.

For another example, let $K_a$ contain:
- $Female(Alice)$
- $Male(Bob)$
- $childOf(Alice, Carl)$
- $childOf(Bob, Carl)$

Let $K_r$ contain:
- $childOf(x, y) \land childOf(z, y) \land x ̸= z \to siblingOf(x, z)$
- $Female(x) \land siblingOf(x, y) \to sisterOf(x, y)$
- $Male(x) \land siblingOf(x, y) \to brotherOf(x, y)$

We can compute $derivedAssertions$ like so:
- Set $derivedAssertions=K_a$
- Apply $childOf(Alice, Carl) \land childOf(Bob, Carl) \land Alice\neq Bob \to siblingOf(Alice, Bob)$ to add $siblingOf(Alice, Bob)$
- Apply $childOf(Bob, Carl) \land childOf(Alice, Carl) \land Bob \neq Alice \to siblingOf(Bob, Alice)$ to add $siblingOf(Bob, Alice)$
- Apply $Female(Alice) \land siblingOf(Alice, Bob) \to sisterOf(Alice, Bob)$ to add $sisterOf(Alice, Bob)$
- Apply $Male(Bob) \land siblingOf(Bob, Alice) \to brotherOf(Bob, Alice)$ to add $brotherOf(Bob, Alice)$
- We now have no more rules we can apply and so we finish and return $DerivedAssertions$

Therefore $$DerivedAssertions=\{Female(Alice),Male(Bob),childOf(Alice, Carl),childOf(Bob, Carl),siblingOf(Alice, Bob),siblingOf(Bob, Alice),sisterOf(Alice, Bob),brotherOf(Bob, Alice)\}$$
We can represent this knowledge base with the following graph:

![[knowledge_graph_2.png]]

These boxes represent classes. Individual names connected with a dotted line indicate that it's a part of that class.

>The colours aren't consistent with this one, but don't worry about it.
## Non-Unary Time and Space Complexity
We consider time and space complexity the same as how we did for the unary case:
- Time complexity is the number of times a new assertion is added to $DerivedAssertions$. Note that ignore checking if we can apply a rule or not.
- Space complexity is the final size of $DerivedAssertions$. Note that $DerivedAssertions$ only grows, it does not shrink.

Since atomic propositions indicating a relationship can contain 2 individual names, it means that if every rule in $K_r$ relates every combo of individual names then $|I_{K_a}|^2\times |K_r|$ is the number of names added. This is obviously the worst case scenario.

If $K$ consists of $K_a$ and $K_r$, and by $I_{K_a}$ we denote the individual names in $K_a$ then
- The time complexity of this algorithm is $|I_{K_a}|^2\times |K_r|$
- The space complexity of the algorithm is $|K_a| + |I_{K_a}|^2\times |K_r|$
## Formulating Queries Using Rules
Sometimes we need to formulate rules to fit a certain definition or requirements. Here we will run over a couple of examples of how we can do this.

First consider the problem "Assume that atomic assertions in $K_a$ are formulated using the binary relation $childOf$ and the class name $King$. Define a set $K_r$ of rules for the class name $GrandchildK$ such that for any such set of atomic assertions $K_a$: $$K \models GrandchildK(a) \iff\text{ a is a grandchild of a king}$$"
>$\iff$ is the symbol for "if, and only if"

Essentially we need to come up with a rule, or group of rules, that mean that $GrandchildK$ works as described.

Here since we are given 2 conditions, which must both be true, for $GrandchildK$ to be true, our $K_r$ must contain a rule which specifies both of these conditions to be true.

So the answer is $$
K_r=\{chlidOf(x,y)\land childOf(y,z)\to grandchildOf(x,z), grandchildOf(x,y)\land King(y)\to GranchildK(x)\}
$$
For another example consider the problem "Assume that atomic assertions in $K_a$ are formulated using the binary relation $childOf$ and the class name $King$. Define a set $K_r$ of rules for the class name $DescendantK$ such that for any such set of atomic assertions $K_a$: $$ K\models DescendantK(a) \iff \text{ a is a descendant of a king}$$"

Here we need to define rules for descendant, based on the rules for child. It is important that these rules are transitive, meaning that if $a$ is a descendant of $b$ and $b$ is a descendant of $c$ then $a$ is a descendant of $c$. To make a transitive rule such as this, it requires self reference as we saw above.

So the answer is $$
K_r=\{childOf(x,y)\to descendantOf(x,y), descendantOf(x,y)\land descendantOf(y,z)\to descendantOf(x,z), descendantOf(x,y)\land King(y)\to DescendantK(x)\}$$