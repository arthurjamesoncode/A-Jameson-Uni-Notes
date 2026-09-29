## Common Mistakes
### Arguing From Example
An incorrect proof of a universal statement is arguing that a statement must be true because an example is true.

An incorrect “proof” of the fact that the sum of any two even integers is even.  
This is true because if m = 14 and n = 6, which are both even, then  
m + n = 20, which is also even.

This is not a correct proof, for a universal statement as it proves nothing about the 4+6, or any other number of cases when the premise (both numbers are even) is true.
### Using The Same Letter to Mean Two Different Things
Consider the following “proof” fragment:  
	Suppose m and n are any odd integers. Then by definition of odd,  
	m = 2k + 1 and n = 2k + 1 for some integer k, therefore $m=n$.

This statement says that m and n are equal. This is obviously not necessarily true.

The correct thing would be to do something like this:
	Suppose m and n are any odd integers. Then by definition of odd,  
	m = 2k + 1 and n = 2l + 1 for some integer k.

When using the same letter for 2 different things, those things must be equal. When using different letters, the thing **can** still be equal but they do not have to be. This is obviously the more useful of the 2 properties.
### Jumping to a Conclusion
To jump to a conclusion means to allege the truth of something without giving an adequate reason.  

For Example:
	Suppose m and n are any even integers. 
	By definition of even, m = 2r and n = 2s for some integers r and s. Then m + n = 2r + 2s. 
	So m + n is even.

The above proof does not show, sufficiently, that m+n is even as it does not show m+n in the same form as the definition of even. 

The proof is missing the following lines:
	m + n = 2r + 2s = 2(r + s)
	As r and s are integers, r + s must be an integer. 
	Therefore by definition of even r + s is even.
### Circular Reasoning
To engage in circular reasoning means to assume what is to be proved.  

For Example, when proving that "*the product of 2 odd integers is odd*":
	Suppose m and n are any odd integers. When any odd integers are  
	multiplied, their product is odd. 
	Hence mn is odd.

Obviously, this is wrong, although the example is very trivial.

The core of circular reasoning is confusion around what is **known**, and what is still to be shown.

For example:
	Suppose m and n are any odd integers. We must show that mn is odd. 
	This means that there exists an integer s such that mn = 2s + 1.  
	Also by definition of odd, there exist integers a and b such that m = 2a + 1 and n = 2b + 1.  
	Then mn = (2a + 1)(2b + 1) = 2s + 1.  
	So, since s is an integer, mn is odd by definition of odd.

The conclusion of this proof relies on the fact that mn = 2s + 1, but that is part of the claim and as such is yet to be shown. So you are, in fact, assuming something you need to prove.
## Good Practice
Good practice when you're writing proofs is to do the following:
- **State your game plan -** Explain the general line of reasoning, for example, “We use case analysis” or “We argue by contradiction.”
- **Keep a linear flow -**  The steps of your argument should follow one another in an intelligible order. 
- **Treat it like an essay, not a calculation -** You should not write a proof the same way you compute something. You should use complete sentences, and fully explain each step.
### Structure of a proof:

You can structure your proofs by using the following
- **Observation** – A fact stated quite often without any formal proof.  
- **Claim** – A minor true statement that is used in other proofs.  
- **Lemma** – A true statement used in proofs of other statements.  
- **Proposition** – A less important but still interesting statement.  
- **Theorem** – A very important true statement.  
- **Corollary** – A simple consequence of a theorem or a proposition.

The above is not an order, just components. The structure of a proof should look like the following:
- **Set Up -** This is where your claim lives and where you set up various variables.
- **Reasoning/Logic -** This is the bulk of your proof and where you show the conclusion to be true.
- **Conclusion -** This is where you compile the consequences of your reasoning, and state the truth of the statement.

You must finish your proofs. After a certain point you will have established all the essential facts needed to understand the conclusion. You must not quit, and leave the reader to draw this conclusion by themselves. You have to tie everything together and explain why the original claim follows.