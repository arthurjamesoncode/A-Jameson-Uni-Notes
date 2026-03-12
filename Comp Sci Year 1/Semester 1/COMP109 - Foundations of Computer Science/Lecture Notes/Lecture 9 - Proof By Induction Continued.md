e## Another Example of Proof By Induction:
Take the statement "${\forall{n} \in \mathbb{Z}\; where\; n\geq0,\; nc\; can\; be\; obtained\; using\; only\; 3c\; and\; 5c\; coins}$". This is a statement that can proved by induction, but it is slightly different process to the other ones.

We can prove it like so,
	*Base case ${n=8}$:
		Can be achieved with 1x5c coins and 1x3c coins.
	Base case n = 9:
		Can be achieved with 3x3c coins.
	Inductive Step:
		Assume kc can be obtained using only 3c and 5c coins
		Case 1, There is a 5c coin among those used to make up kc:
			We can make (k+1)c by removing the 5c coin and adding 2x3c coins.
		Case 2, There is no 5c coin among those used to make up kc:
			We can make (k+1)c by removing 3x3c coins and adding 2x5c coins
			This case relies on there being at least 3x3c coins whenever there . As we can see from the second base case, this is true for n=9, as every other multiple of 3 is greater than 8 is greater than 9, we know this is true.
	As the base cases are true and both cases of the inductive step are true, we can see that the statement is true for all n $\geq$ 8.

>You don't strictly need to show both base cases here, it just more clearly illustrates how, there is always at least 3c coins if there is no 5c coins with these conditions.
## Proving Properties of Programs
Take the following program:

```
mylist = [1, 2, 6, 3, 5, 6] \\ could be any list
i = 0  
M = mylist [0]

while i < len (mylist) :
	M = max (M , mylist[i])  
	i = i + 1
	
print (M)
```

This program finds the max of a given list and prints it to the screen.

To prove that this program always prints out the maximum of the list, we can use induction. To do this we need to recognise the property that `M = max (M, X)` assigns the value to be the larger value of `M` and `X`.

To prove this we can prove that the value of `M` is always the greatest value of the list from `0` to `i` with induction:
	*Base Case, `i = 0`.*
		*Before the statement, `M = mylist[0]`.*
		*So at the first step of the loop `M` = the maximum of `mylist[0]` and `mylist[0]`.
		This is the maximum of the list from indexes 0 to 0 so it is true for the base case. 
	Inductive Step
		Assume `M` is the maximum of the list from `0` to `i`
		At the `i+1`th step `M` becomes the maximum of `mylist[i+1]` and `M`.
		Case 1, `M` is smaller then `mylist[i+1]`:
			`M` becomes `mylist[i+1]` and so `M` is the greatest element of the list up to `i+1`
		Case 2, `M` is larger then `mylist[i+1]`:
			`M` stays with the value of `M` and so `M` is the greatest element of the list up to `i+1`
	As the base case is true, and the inductive step is true we can prove the the program works for all values of `i < len(mylist)`. And so `M` must be the maximum of the list at the end of the program.

This is obviously overkill for a program this simple, but for more complicated programs you can probably understand how it would be useful to prove something like this formally.
## Strong Induction:
Strong induction is very similar to regular induction, and often there isn't even a distinction drawn between the 2. 

Strong induction is done by the following:
- We prove that the property holds for the base case, $n=b$ 
- We prove that if the property holds for ${n=b,b+1,...,k}$ then it holds for $n=k+1$

This may not seem different to you, but the key difference is that we assume the property holds for all $n$ between $b$ and $k$ inclusive, and not just for $n=k$.

Take the statement "${\forall{n} \in \mathbb{N}\; where\; n\geq2,\; n\; is\; either\; a\; prime\; or\; a\; product\; of\; primes}$".

We can prove this by strong induction:
	*Base Case ${n = 2}$*
		*2 is prime and so n is prime.*
	Inductive Step:
		*Let ${n = k}$*
		*Assume that every number $i$ such that ${2 \leq i \leq k}$ is either a prime or the product of primes.
		Case 1, $k+1$ is prime:
			If $k+1$ is prime then the property holds for $k+1$
		Case 2, $k+1$ is not prime:
			Then $k+1=ab$ such that ${2 \leq a,b \leq k}$. 
			Since a and b are both either prime or the product of primes then $k+1$ must be the product of primes. 
			If a and b are both primes then $k+1$ is the product of 2 primes. 
			If either of a and b is the product of primes, $k+1$ is the product of more than 2 primes.
	Therefore since it holds for both the base case and the inductive step, all numbers greater than 2 must either be prime or a product of primes.

