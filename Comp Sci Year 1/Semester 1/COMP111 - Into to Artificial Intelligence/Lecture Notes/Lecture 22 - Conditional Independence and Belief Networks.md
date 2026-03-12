## Independence and Random Variables
Random variables $F$ and $G$ are independent if $$\mathbf{P}(F, G)=\mathbf{P}(F)\times\mathbf{P}(G)$$which means that, for all values $r$ and $s$, $$P(F = r, G = s) = P(F = r)\times P(G = s)$$
What this also means is that if we know that 2 variables are independent we know that the above is true.

Consider the **dentist domain** and the **weather domain** from [[Lecture 20 - Random Variables]].

As we know that visits to the dentist don't influence the weather in any way, the pairs of random variables:
- $Toothache$, $Weather$
- $Catch$, $Weather$
- $Cavity$, $Weather$
Are each independent.

The full joint probability distribution for these variables$$\mathbf{P}(Toothache, Catch,Cavity,Weather)$$has 32 entries.

It is made up of 4 different tables, for the dentist related variables. 1 for each of $$sunny,rain,cloudy,snow$$
Since $Toothache$, $Catch$, and $Cavity$ are all binary variables, meaning they take values of either 0 or 1, we have 8 probabilities in each table.

Therefore we have:
- 8 Probabilities for $(Weather=sunny)$ $$P(Weather=sunny, Toothache=r_1, Catch=r_2, Cavity=r_3)$$
- 8 Probabilities for $(Weather=rain)$ $$P(Weather=rain, Toothache=r_1, Catch=r_2, Cavity=r_3)$$
- 8 Probabilities for $(Weather=cloudy)$ $$P(Weather=cloudy, Toothache=r_1, Catch=r_2, Cavity=r_3)$$
- 8 Probabilities for $(Weather=snow)$ $$P(Weather=snow, Toothache=r_1, Catch=r_2, Cavity=r_3)$$

All of the probabilities in these four tables will sum to 1.

As we can assume independence between the dentist variables and $Weather$, we know a few things. Firstly we know that, for all $r_1,r_2,r_3\in \{0,1\}$$$P(Weather=sunny|Toothache=r_1,Catch=r_2,Cavity=r_3)=P(Weather=sunny)$$We also know that, for all $r_1,r_2,r_3\in \{0,1\}$,$$P(Weather=sunny,Toothache=r_1,Catch=r_2,Cavity=r_3)=P(Weather=sunny)P(Toothache=r_1,Catch=r_2,Cavity=r_3)$$
The above also holds for the variables $rain$, $cloudy$, and $snow$.

What this tells us is that the full joint probability distribution $$\mathbf{P}(Toothache, Catch,Cavity,Weather)$$can be written as:$$\mathbf{P}(Weather)\mathbf{P}(Toothache,Catch,Cavity)$$
What this means is that we can create the full 32-element table using one 4-element table and one 8-element table. With the 4-element table representing $\mathbf{P}(Weather)$ and the 8-element table representing $\mathbf{P}(Toothache, Catch, Cavity)$.
### Determining Independence
When given probabilities, we can check if outcomes are independent by using our formulas for conditional independence. Other times, we may not have probabilities yet and so we must use reasonable analysis to determine whether pairs of variables are independent.

Lets consider the domains we've looked at previously and determine independence for these variables:
- Dentist domain: the variables Toothache, Catch, and Cavity are all dependent on each other.
- Student exam domain with variables Grade, Answers, Background, Works hard: It seems reasonable to assume that Background and Works hard are independent. No other pair is independent.
- Fire alarm domain: Fire, Alarm, Tampering, Smoke, Leaving, and Report. 
- It seems reasonable to assume that Tampering and Fire, and Tampering and Smoke are independent. No other pair is independent

After analysing these domains, we can see that independence is slightly rare. Now, we'll have a look at Conditional Independence.
### Conditional Independence
Random variables $G$ and $F$ are conditionally independent given $H_1,...,H_n$ if $$\mathbf{P}(G,F\;|\;H_1,...,H_n)=\mathbf{P}(G\;|\;H_1,...,H_n)\times\mathbf{P}(F\;|\;H_1,...,H_n)$$or, equivalently $$\mathbf{P}(G,\;|\;F,H_1,...,H_n)=\mathbf{P}(G,|\;H_1,...,H_n)$$
These are the same as our original rules for independence, except that we operate under the assumption that events $H_1,...,H_n$ have occurred.

Consider the **dentist domain**, it seems reasonable to assert conditional independence of the variables $Toothache$ and $Catch$ given $Cavity$. So $$\mathbf{P}(Toothache,Catch\;|\;Cavity)=\mathbf{P}(Toothache\;|\;Cavity)\mathbf{P}(Catch\;|\;Cavity)$$Or equivalently, $$\mathbf{P}(Toothache\;|\;Cavity)=\mathbf{P}(Toothache\;|\;Catch,Caivity)$$
Asserting conditional independence of $Catch$ and $Toothache$ given $Cavity$ we can compute the joint probability distribution $$\mathbf{P}(Toothache, Catch, Cavity)$$using **only** the probability distributions:$$\mathbf{P}((Toothache\;|\;Cavity),\;\;\mathbf{P}(Catch\;|\;Cavity),\;\;\mathbf{P}(Cavity)$$
We can do this by first using the multiplication rule to get $$\mathbf{P}(Toothache, Catch, Cavity)=\mathbf{P}(Toothache, Catch\;|\;Cavity)\times\mathbf{P}(Cavity)$$and then using conditional independence we can get $$\mathbf{P}(Toothache, Catch\;|\;Cavity)\times\mathbf{P}(Cavity)=\mathbf{P}(Toothache\;|\;Cavity)\times\mathbf{P}(Catch\;|\;Cavity)\times\mathbf{P}(Cavity)$$
Because of this we only need 5 probabilities, which we can often learn from data.
## Belief Networks
We can use conditional representation to give concise representations of many domains.

A belief network, or Bayesian network, is a graphical probabilistic model of a domain in which nodes represent random variables, and edges represent probabilistic dependence, usually causality.

What this means is that if there is an edge, from a random variable $F$ to another random variable $G$ then $G$ depends on $F$. We call $F$ a parent of $G$.

In a belief network, it is assumed there are no cycles and that any random variable $G$ is conditionally independent of any non-parent variable $G'$ given the parents of $G$ as long as $G'$ cannot be reached by a sequence of edges from $G$.

For example:
![[belief_1.png]]

In this example, we can see that $Catch$ and $Toothache$ both depend on their **parent** $Cavity$. This means that both $Catch$ and $Toothache$ are independent given their parents, in this case only $Cavity$.

You can compute the full joint probability distribution from a belief network by using $$\prod_{F\text{ in network}}\mathbf{P}(F\;|\;parents(F))$$We will see a proof of why this is in [[Lecture 23 - Belief Networks Continued]].

What this means is that the full joint probability distribution is a result of the product of the probability distributions of each variable $F$ given their parents.

So for the example above we can get the full joint probability distribution from $$\mathbf{P}(Toothache\;|\;Cavity)\times\mathbf{P}(Catch\;|\;Cavity)\times\mathbf{P}(Cavity)$$
Now we will go over belief networks for the domains discussed in [[Lecture 20 - Random Variables]]
### Student Exam Domain
Recall the student exam domain with random variables:
- $Grade$ - which takes as values the possible grades of a student in the exam, say $\{A,B,C,D,E,F\}$
- $Answers$ - which takes as values the answers given by the student in the exam, not really possible to list here.
- $Background$ - which takes as a value the school visited before coming to university, say $\{Comprehensive, Academy, Public\}$
- $WorksHard$ - which takes as a value the degree to which the student works hard, say $\{0,1\}$

From this it seems reasonable to assume that
- $WorksHard$ and $Background$ are independent
- $Grade$ and $WorksHard$ are independent given $Answers$
- $Grade$ and $Background$ are independent given $Answers$

Based on this we could represent our modelling of this domain using the following belief network:
![[belief_2.png]]
### Fire Alarm Domain
Recall the fire alarm domain with random variables (all taking values of 0 and 1):
- $Fire$: there is fire;
- $Alarm$: the alarm goes off;
- $Tampering$: there is tampering with the alarm system;
- $Smoke$: there is smoke (no smoke detector used);
- $Leaving$: people leave the building;
- $Report$: it is reported that people leave the building (reporting not always correct).

It is reasonable to assume:
- $Fire$ and $Tampering$ are independent
- $Alarm$ depends on $Fire$ and $Tampering$
- $Smoke$ and $Tampering$ are independent.
- $Smoke$ depends only on $Fire$ and is conditionally independent of $Alarm$ given fire.
- $Leaving$ is conditionally dependent of the other variables above given $Alarm$
- $Report$ only directly depends on $Leaving$

Based on all of this we can represent our modelling of the fire alarm domain using the belief network:
![[belief_3.png]]
