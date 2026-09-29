## Key Definitions

An **array** is a numbered collection of data elements of the same type, and therefore the same size.

A **nested array**, also called a **2D array**, is an array which contains a number of other arrays.

**Sequential search** is a search algorithm which works by checking every element of the array in sequence to see if it matches the `key`. This is also called **linear search**.

**Binary search** is a search algorithm which works on a sorted list by repeatedly splitting it in two, and comparing the mid points of each sub-list with the `key`.

**Naïve pattern matching** is a pattern matching algorithm which determines whether a given pattern exists in a given array/string. It does so by checking every position of the array for the pattern. Better alternatives are not needed for this course but can be read about [[Lecture 7 - 2D Arrays and Pattern Matching#Doing Better|here]].
## Array Properties & Notation
We use `A[1..n]` to denote an array with $n$ elements numbered from $1$ to $n$.

We use `A[i]` to denote the $i^{th}$ element of array `A`.

In the case of **2D arrays** we use `A[i][j]` to denote the $j^{th}$ element of the $i^{th}$ array in `A`.

Retrieving the $i^{th}$ element of an array is an $O(1)$ operation.

Inserting an element into an array at position $i$ while maintaining the order is an $O(n)$ operation, as all later elements need to be shifted to the right by 1.
## Array Algorithms
**Sequential Search:**
```
//Inputs: key, A[1..n]

i = 1
found = false

while (NOT found) AND i <= n do
	if A[i] = key then
		found = true
	else
		i = i + 1
	endif
endwhile

output found 
```

**Binary Search:**
```
//Inputs: key, A[1..n]

min = 1
max = n
found = false

while (NOT found) AND min <= max do
	mid = (min + max)/2 truncated to an integer
	if A[mid] == key then
		found = true
	else if A[mid] < key then
		max = mid - 1
	else 
		min = mid + 1
	endif
endwhile

output found
```

**Finding max value:**
```
//Inputs: A[1..n]

m = A[1]

for i = 2 to n do
	if A[i] > m then
		m = A[i]
	endif
endfor

output m
```

**Finding max value and location**:
```
//Inputs: A[1..n]

loc = 1

for i = 2 to n do
	if A[i] > A[loc] then
		loc = i
	endif
endfor

output loc and A[loc]
```

**Finding first and second match**:
```
//Inputs: A[1..n]

if A[1] > A[2] then
	m1 = A[1]
	m2 = A[2]
else
	m1 = A[2]
	m2 = A[1]
endif

for i = 3 to n do
	if A[i] > m1 then
		m2 = m1
		m1 = A[i]
	else if A[i] > m2 then
		m2 = A[i]
	endif
endfor

output m1, m2
```

**Naïve pattern matching:**
```
//Inputs: text[1..n], patten[1..x]
found = false
i = 1
while (NOT found) AND i <= n-x+1 do
	j = 0
	while j < x AND text[i + j] == pattern[j + 1] do
		j++
	endwhile
	
	if j == x then
		found = true
	endif
	
	i++
endwhile

output found
```

For all **finding max** algorithms, a **finding min** algorithm can be achieved by swapping any `>` for `<` and vice versa.
## Properties of Array Algorithms
Assume all algorithms are on an array of size $n$, excluding **naïve pattern matching**.

**Sequential search** on arrays has $O(n)$ time complexity, whether sorted or unsorted, although there are some small optimisations you can do if sorted. 

**Sequential search** is the most efficient searching algorithm for unsorted/unordered data.

**Binary Search** on a sorted array has $O(\log n)$ time complexity. It does not work on unsorted arrays, but is optimal for sorted data.

**Finding max/min** of an unsorted array has $O(n)$ time complexity for all given variations.

**Finding max/min** of a sorted array (obviously) has $O(1)$ time complexity.

**Naïve pattern matching** has a time complexity of $O(xn - x^2)$. This is much worse than the time complexity of the better algorithms discussed [[Lecture 7 - 2D Arrays and Pattern Matching#Doing Better|here]].
## Proof of Correctness
For examples of how to prove the correctness of programs look to [[Lecture 8 - Proof Of Correctness]].

We prove the correctness of programs by using **proof by induction**. This works well because pretty much all complicated algorithms involve tracing effects through a loop. 

We can perform induction on either:
- The value of a counter (such as $i$) as it iterates through the loop
- The size of the input

This lets us prove some property that is always true at the end of a loop iteration/run of a program. This property is called the **invariant**. We must choose an **invariant** which results in the **consequence** we want to show is true.

Proof by induction has 4 steps:
- Proving the truth for the base case. This could be the value of the counter after the first iteration, or a small/empty input. Usually $n=1$ or $n=0$ in some form.
- Assume the claim holds for values up to $n=k$. This is called the **induction hypothesis**.
- Prove that if the claim holds for $n=k$ then the claim must hold for $n=k+1$. This is called the **inductive step**.
- Write a conclusion tying everything together.

There is also **strong induction** which is the same except that, in the inductive hypothesis, you assume that the claim is true for all $n\leq k$.