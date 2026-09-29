## What Are Proofs?
A mathematical proof is a carefully reasoned argument to convince a sceptical listener, who is often yourself, that a given statement is true.

Proof complements discovery. When you believe that you've discovered something is true, you must try to figure why it is true. Upon being successful you know your discovery is genuine, upon failure you will be given insight into the nature of the problem, which may even lead to discovery that the statement is false.

>Discovery and Proof are both integral parts of problem solving.
## Visual Proofs
Visual proofs can be a fairly elegant way to prove certain properties.

**For example**:
![[visual_proof_example.png.png]]

The above example on the left contains a very elegant proof of the property *"(a+b)$^2$=a$^2$+2ab+b$^2$"*. The right however contains a "proof" of something impossible. This is meant to show you that while visual proofs can be elegant and quick to understand, they can also be misleading. 

>The proof on the right is wrong because, if you zoom in, you can see that the hypotenuse of the blue and red triangles don't meet in an exactly straight line. This allows for the extra space necessary for the empty square. As this is spread out it is hard for us to see.
## The Role of Definition in Proofs
Proofs are built off of definitions.

In order to prove the following statements we require some kind of definition of what an *even* number is:
- *0 is even*
- *-301 is odd*
- *The sum of any 2 odd numbers is even*
- *Every integer is either even or odd*

This is true for all proofs, we define certain identities and then use these identities to prove certain things. Once we have proved these things, those proofs can then be used when proving other concepts.

**Even an odd numbers are defined as follows:**
	An integer *n* is **even** if, and only if, *n* equals twice some integer.
	An integer *n* is **odd** if, and only if, *n* equals twice some integer plus 1.
Using notation we can write:
	*n* is **even** $\iff$ $\exists$ an integer *k* such that *n=2k*
	*n* is **odd** $\iff$ $\exists$ an integer *k* such that *n=2k+1*

>$\iff$ means *"if, and only if,*". $\exists$ means "*there exists*" and is called the existential quantifier. 

Using this definition we can formally prove the first 2 statements.

**0 is Even**
	*0 = 2(0)
	0 is an integer.
	"2(0)" is of the form "2k".
	Therefore, by definition, 0 is even.*

**-301 is Odd**
	*-301 = 2(-151) + 1
	-151 is an integer.
	"2(-151) + 1" is of the form "2k+1". 
	Therefore, by definition, -301 is odd.*

The next statement also require this definition of even and odd to solve but they are a bit more complicated since they are more general. 

This increased level of abstraction means we have to do a bit more work, but the core idea is the same. We use these identities and we show that any 2 chosen arbitrary odd numbers sum to an even number.

**This statement can be formally proved like this:**
	*Let n and m be arbitrary odd integers.
	By definition: n = 2k+1, k $\in$ $\mathbb{Z}$, m=2l+1, l $\in$ $\mathbb{Z}$.
	2k + 2l = 2(k + l).
	As k and l are both integers, "k + l" is an integer.
	Therefore, by definition, 2(k+l) is even and so the sum of any 2 arbitrary odd integers is even.

>$\in$ means "is in" or "is a member of", and $\mathbb{Z}$ is the symbol for the set of integers.

Note that we cannot reuse *k* for both *n* and *m* as *k* and *l* do not need to be the same integer. It is important to recognise as well that while *k* and *l* do not have to be the same integer they can be, as there are no constraints stopping them from being so.  
## End of Note
The rest of this lecture Karteek just goes over examples, I don't want to just fill my notes with tons of practice, these are for core concepts and a couple of examples to illustrate it. Also the last statement is will be used as an example in the next statement.

