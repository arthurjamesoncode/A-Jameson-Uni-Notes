Intelligent agents need to be able to perform several tasks:
- Perception - Understanding the state of the environment.
- Deliberation - Deciding what action they should take.
- Action - Executing the action.

State recognition implies they have some **representation** of their knowledge of the state, and deliberation requires some form of **reasoning**.

So, essentially, when building agents, we need to tell it what it needs to know and give it some way of reasoning about the relevant consequences of this knowledge.
## Knowledge Bases and Reasoning Engine
This is a declarative approach to building agents. We build 2 parts:
- A knowledge base, which contains facts and general knowledge about a domain in some formal language.
- A reasoning engine, which produces the relevant consequences of the knowledge base.

Consider the following knowledge base: 
- If I have an AI lecture today, then it is Tuesday or Friday.
- It is not Tuesday.
- I have an AI lecture today or I have no class today. 
- If I have no class today, then I am sad. 
- I am not sad. 

Can you infer what day it is?

We can obviously use simple logic to infer things about this. 
- Since he is not sad, it must be the case that he has class today. 
- Since he has class today, it must be the case that he has an AI lecture today. 
- Since he has an AI lecture today, it must be the case that it is Tuesday or Friday.
- Since it is not Tuesday, it must be Friday.

And so we can infer that it is Friday.

This section of the module is focused on formalising these sorts of logical deductions in a way in which machines can understand them.
### Medical Knowledge
As another example, consider the following medical knowledge base: 
- Pericardium is a tissue contained in the heart 
- Pericarditis is an inflammation located in the pericardium
- Inflammation is a disease that acts on tissue 
- A disease located in something contained in the heart is a heart-disease 

Can you infer that pericarditis is a heart-disease?

Again we can:
- Since pericarditis is an inflammation located in the pericardium and inflammation is a disease that acts on tissue, it must be that pericarditis is a disease located in the pericardium.
- Since pericardium is a tissue contained the heart, pericarditis is a disease located in something contained in the heart.
- Since pericarditis is a disease located in something contained in the heart, pericarditis is a heat-disease.

This example contains propositions from SNOMED CT, a medical and healthcare knowledge base. We call this a medical ontology. It contains more that 300,000 propositions that define the meaning of medical terms in a machine readable way.

SNOMED CT is used as a knowledge base by the NHS and healthcare systems of more than 20 countries and is used to process electronic medical records containing test results medications and treatments. Your GP uses SNOMED CT terms to fill in your electronic medical record.
### Mathematical Knowledge
Consider a mathematical problem such as: $$\text{for which x does }ax^2 + bx + c = 0\text{ hold?}$$
There are infinitely many equations, so it is not possible to store the answers to all these problems in a database or knowledge base. 

Instead we can: 
- Store axioms of arithmetic such as $$x + y = y + x,\; x(y + z) = xy + xz$$ in a knowledge base. 
- Use reasoning algorithms to solve particular problems using the axioms in the knowledge base.
### Knowledge Graph
When you search for Liverpool you receive structured information about Liverpool FC. 

In particular: 
- Liverpool Football Club is a professional association football club based in Liverpool, Merseyside, England. They compete in the Premier League, the top tier of English football. 
- Nickname: The Reds
- Manager: Arne Slot 
- Arena/Stadium: Anfield 
- Customer service: 0151 264 2500 
- Parent organization: Fenway Sports Group 

This information is stored in the Google knowledge graph (which is a knowledge base).

Many facts are not stored in the knowledge graph. 

Possibly the following:
- Liverpool FC competes in the FA Cup; 
- Arne Slot is employed by Liverpool FC. 

If, however, the following is stored in the knowledge graph: 
- If a club competes in the Premier League, then it competes in the FA Cup; 
- A manager of a football club is employed by the football club. 

Then the facts above can be deduced from the knowledge graph using reasoning.
## Rule Based Languages
To store knowledge in a knowledge base and perform reasoning, we have to represent the knowledge in a formal language that machines can read.

Many knowledge representation and reasoning (KR&R) languages were first developed in logic, a subdiscipline of maths and philosophy, and now also of computer science.

We consider rule-based languages and propositional logic as KR&R languages. Both are important in computer science.
### Syntax
The syntax of a rule based language is as follows.

Individual names, also called **constant symbols**, denote individual objects. For example: 
- $LiverpoolFC$ 
- $ArneSlot$
- $England$

Often we might use lower case letters like $a$, $b$, $a_1$, $a_2$ and so one as individual names.

Individual variables are placeholders for individual names. These are denoted by lower case letters. For example: $x$, $y$, $x_1$, $x_2$ and so on.

Class names, also called **unary predicate symbols**, denote a set, or group, of individual objects. For example: 
- $CompetesInPremierLeague$
- $FootballClub$ 
- $HumanBeing$

Often we might use upper case letters like $A$, $B$, $A_1$, $A_2$ as class names.

Atomic assertions take the form $A(b)$ and state that $b$ is in the class $A$. For example:
- $CompetesInPremierLeague(LiverpoolFC)$ asserts that Liverpool FC competes in the premier league.
- $Manager(Slot)$ asserts that Slot is a manager.

A unary rule takes the form $$
A_1(x)\land ... \land A_n(x)\to A(x)
$$ where $A_1$, $A_n$, and $A$ are class names and $x$ is an individual variable.

This rule states that if $x$ is in all classes $A_1,A_2,...,A_n$ then $x$ is in the class $A$.

For example:
- $CompetesInPremierLeague(x) \to CompetesInFACup(x)$ states that everything that competes in the Premier League also completes in the FA Cup.
- $Disease(x) \land LocatedInHeart(x)\to HeartDisease(x)$ states that everything that is a disease and is located in the heart is a heart disease.
### Unary Rule-Based Systems
A unary rule-based knowledge base $K$ is a collection $K_a$ of atomic assertions and $K_r$ of unary rules.

For example, let $K_a$ contain the following atomic assertions:
- $CompetesInPremierLeague(LiverpoolFC)$
- $CompetesInPremierLeague(Everton)$
- and so on for all clubs competing in the Premier League (20 facts in total)

Let $K_r$ contain the following rules: 
- $CompetesInPremierLeague(x) \to CompetesInFACup(x)$
- $CompetesInPremierLeague(x) → FootballClub(x)$ 
- $CompetesInPremierLeague(x) → BasedInEngland(x)$.

The following atomic assertions **follow** from $K$:
- $CompetesInFACup(LiverpoolFC)$
- $FootballClub(Everton)$
- and so on

Since we have 20 assertions, and 3 rules that apply to all those assertions, we can derive 60 total facts from that knowledge base.

We say an assertion $A(b)$ follows from a knowledge base $K$ if whenever $K$ is true, $A(b)$ is also true.

In symbols follows $A(b)$ follows from $K$ is$$
K\models A(b)
$$
and $A(b)$ doesn't follow from $K$ is $$
K\not\models A(b)
$$
In the example above we have$$
K\models CompetesInFACup(LiverpoolFC)
$$
In fact if we have $$K'_a=\{CompletesInPremierLeague(LiverpoolFC)\}$$ and $$K'_r=\{CompetesInPremierLeague(x) \to CompetesInFACup(x)\}$$ we know that, for $K'$ containing $K'_a$ and $K'_r$ $$K'\models CompetesInFACup(LiverpoolFC)$$
### Abstract Examples
Below we have a few more examples, which don't model any real world objects.

For example 2, let 
- $K_a = \{A_1(a)\}$
- $K_r = \{A_1(x) \to A_2(x), A_2(x) → A_3(x)\}$

Let $K$ contain $K_a$ and $K_r$ . Then 
- $K \models A_1(a)$ 
- $K \models A_2(a)$ 
- $K \models A_3(a)$ 

For example 1, let 
- $K_a = \{A_1(a)\}$
- $K_r = \{A_1(x) \to A_2(x), A_2(x) ∧ B(x) → A_3(x)\}$

Let $K$ contain $K_a$ and $K_r$ . Then 
- $K \models A_1(a)$ 
- $K \models A_2(a)$ 
- $K \not\models A_3(a)$ 
- $K \not\models B(a)$

You can see the same notation in [[Lecture 25 - Propositional Logic]] from the COMP109 module.
## Deriving Assertions
The process of deriving assertions from a knowledge base $K$ is the process of listing all of the atomic propositions that follow from $K$. We call the resulting set $DerivedAssertions$. To check that an assertion $A(b)$ follows from $K$ all we need to do is check if $A(b)$ is in $DerivedAssertions$.

The following algorithm computes the set $DerivedAssertions$ by starting with $DerivedAssertions=K_a$ and exhaustively applying the rules in $K_r$ to the atomic assertions in $DerivedAssertions$. 

```
Input: 
	a knowledge base K containing
	assertions Ka and rules Kr
	DerivedAssertions := Ka 

repeat
	if there exists E(a) not in DerivedAssertions
		and A1(x)∧···∧An(x) → E(x) in Kr
		and A1(a),···,An(a) in DerivedAssertions
	then add E(a) to DerivedAssertions
		NewAssertion := true
	else NewAssertion := false
	endif
until NewAssertion = false

return DerivedAssertions
```

In the above algorithm, we say that $E(a)$ is added to $DerivedAssertions$ by applying the rule $$A_1(x)\land ... \land A_n(x) \to E(x)$$
To the atomic assertions$$A_1(a),...,A_n(a)\in DerivedAssertions$$
>$\in$ means "is an element of" or "in". So the above means $A_1(a),...,A_n(a)$ which are in $DerivedAssertions$.