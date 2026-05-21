## Key Definitions
A **divide and conquer** algorithm is an algorithm which works by splitting a problem down into smaller parts and then solving the smaller parts before joining the solutions together to form a solution to the whole problem.

**Merge sort** is a divide and conquer sorting algorithm which works by splitting a list down into individual elements (which are already sorted lists) and then merging them together to maintain the order.

The **Fibonacci numbers** is a sequence of numbers in which the next number is obtained by adding the most recent 2 numbers.

A **recurrence** $f$ is an equation/inequality that describes the value of $f(n)$ in terms of $f(x)$ where $x$ is defined relative to $n$.
## General D&C Algorithms
Example of finding sum using D&C algorithm
```
//Takes input of an array A indexed [1..n]

RecursiveSum(A, p, q)
begin
	if p == q then 
		return A[p]
	endif
	
	newQ = (p + q - 1)/2
	newP = (p + q + 1)/2
	
	sum1 = RecursiveSum(A, p, newQ)
	sum2 = RecursiveSum(A, newP, q)
	
	return sum1 + sum2
end

RecursiveSum(A, 1, n) //Initial call
```

**Properties of general recursive D&C algorithms on arrays:**
- If splitting the input in half, they will always return a value $2n-1$ times
- Their execution will always form a binary tree with $\log_2(n)+1$ layers, including the top layer
- Each layer of the execution tree will still have $n$ elements

For simple D&C algorithms, such as summing, finding product, or finding minimum, where the *conquer* step is done in constant time, D&C algorithms have a time complexity of $O(n)$.
## Merge Sort
**Merge Pseudocode:** $O(n)$ where $n=p+q$
```
Merge(A[1..p], B[1..q])
begin
	merged = [1..(p+q)] \\new array of length (p+q)
	a = 1
	b = 1
	
	while a <= p AND b <= q do
		if A[a] < B[b] then
			merged[a+b-1] = A[a]
			a = a + 1
		else
			merged[a+b-1] = B[b]
			b = b + 1 
		endif
	endwhile
	
	if a <= p then
		for i = a to p do
			merged[i+b-1] = A[a]
		endfor
	else
		for i = b to p do
			merged[i+a-1] = B[b]
		endfor
	endif
	
	return merged
end
```

**Merge Sort Pseudocode:** $O(n\log n)$
```
MergeSort(A[1..n])
begin 
	if n == 1 then 
		return A[1]
	endif
	
	copy A[1..(n/2)] to left[1..(n/2)]
	copy A[(n/2)+1..n] to right[1..(n/2)]
	MergeSort(left)
	MergeSort(right)
	
	return Merge(left, right)
end
```
## D&C Fibonacci Numbers
**Pseudocode:** $O(2^n)$
```
F(n)
begin
	if n == 0 OR n == 1 then
		return 1
	endif
	
	return F(n-1) + F(n-2)
end
```

This algorithm is slow because it uses **multiple recursion**. You can calculate time complexity of algorithms like this by solving the recurrence. I doubt this will be needed in the exam but there is an example of this [[Lecture 24 - Fibonacci Numbers & Recurrences#Solving a Recurrence|here]].