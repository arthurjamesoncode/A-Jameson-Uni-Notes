## Dynamic Programming
Dynamic programming is a way to optimise algorithms by storing previous results. 

Often this is done through **memoisation** (pronounced memo-I-say-shun), which means to store the result of calling a pure function with specific arguments. After doing this, we can skip the time taken to compute this function and instead retrieve it.

A function which uses memoisation is called a **memoised** function.

The word **memoisation** comes from the idea that instead of calling the function and going through with potentially expensive calculations, the function can just look at it's arguments and grab a **memo** stating the correct output.

>In the slides Prudence says **memorisation** instead of **memoisation**. I don't think that's right but it doesn't really matter. I'm putting the link to the [Wikipedia page](https://en.wikipedia.org/wiki/Memoization) for memoisation just to back myself up.
## Memoising Fib
Let's reconsider our algorithm to find the Fibonacci numbers. We showed [[Lecture 24 - Fibonacci Numbers & Recurrences#Solving a Recurrence|last lecture]] that the time complexity of this algorithm was $O(2^n)$. This is obviously really bad, so how could we improve it.

If you look at the figure below, you can see why this algorithm is so inefficient.
![[fib-repeats.png]]
Many of the calculations are done multiple times since the same values appear in this tree multiple times. As stated $F(2)$ alone shows up 5 times.

This suggests to us that we could use **dynamic programming** to speed up the execution of this algorithm. Let's start by trying to write a **memoised** version of this.

We need some way of storing the computed values. In this case, we are working with numbers, and we know that we will need to store exactly $n$ values (or technically $n-1$) to calculate the $n^{th}$ Fibonacci number. This means that, in this case, we can just use an array of $n$ elements.

>In a lot of **memoised** functions, the inputs may not be numeric, or they may have multiple and be varied. In these cases you would use a [hash table](https://en.wikipedia.org/wiki/Hash_table) to store the results as key value pairs, where the key is derived from the arguments (e.g. a string made of concatenating every argument).

We will define a **Wrapper algorithm** where we will define our array and our **Fib function** which will actually compute the values. 

>In most programming languages, you would need to consider the **scope** of the variables to ensure that **Fib** can see the array defined in **Wrapper**. For the sake of simplicity assume it can for our algorithm.

```
Wrapper(n)
begin
	table = [0..n]
	table[0] = 1
	table[1] = 1
	
	for i = 2 to n do
		table[i] = -1
	endfor
	
	return Fib(n)
end

Fib(n)
begin
	if table[n] = -1 then
		table[n] = Fib(n-1) + Fib(n-2)
	endif
	
	return table[n]
end
```

If we look at the execution tree for our **memoised algorithm** (assuming left side is executed first), we can see how much smaller the execution tree is.
![[memoised-fib-tree.png]]

Since each sub-tree no longer needs to be recomputed, we can remove most of the tree. This now only calculates the value of each `Fib(x)` once and, when it needs it again, just retrieves it.

If we count the number of returns of this algorithm we find that there are $2n-1$ for `Fib(n)`. This is $O(n)$ which is obviously much better than $O(2^n)$ but we can go a little further.
## Doing Better
In our algorithm, we still make quite a few recursive calls that we don't need to make. When our algorithm computes `Fib(4)`, it requires `Fib(2)` to be called twice. 1st for calculating the value of `Fib(3)` and then for calculating the value of `Fib(4)`.It doesn't need to do much more work on the second call, but it is still something. 

If we think about this, it's slightly unnecessary since, after calculating a Fibonacci number for the first time, we know we have it and we shouldn't need to check. However, since this algorithm works recursively from the top down, we have to check every time.

If, instead, we worked from the bottom up we can always just take the last two computed values. 

```
Fib(n)
begin
	table = [0..n]
	table[0] = 1
	table[1] = 1
	
	for i = 2 to n do
		table[i] = table[i-1] + table[i-2]
	endfor
	
	return table[n]
end
```
Let's have a look at why this is better.

Our algorithm is no longer recursive, meaning we can't count returns anymore. Instead we can count how many times an element of the table is assigned. The answer is $n+1$ times. While this is still $O(n)$, this is roughly double as fast as the **memoised** approach.

