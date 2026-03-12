## Data Structures
What are data structures, and why do we need them?

Data is **dynamic** which means it might grow, shrink or otherwise change over time.

We often want to perform operations on this dynamic data. These operations can involve:
- Searching
- Inserting
- Deleting
- Finding the minimum value
- Finding the maximum value
- Finding a successor
- Finding a predecessor

Some of these operations, namely **inserting** and **deleting** actually change the data in some way.

Data structures are essentially systematic ways of organising and accessing data in order to make various operations on the data efficient. There are many different data structures which all have different uses, advantages and disadvantages. We will learn about these over this course and they include:
- Arrays
- Queues
- Stacks
- Linked Lists
- Trees
- Graphs
- Hash Tables
### Arrays
An array is a numbered collection of data of the same type. Every **cell** has an index and contains an **element**.

In pseudocode you can denote an array `A` of size `n` with indices `1 to n` as `A[1..n]`. You can denote the `i`th element of an array by using `A[i]`. Elements of an array can be redefined the same as variables can. You could also choose a different set of indexes.

Note that, in most programming languages,  arrays are zero indexed. If you want to use 0 indexing in pseudocode you can, but in the lecture notes `1 to n` will be used. This is partially to illustrate that the logic of the program does not change if the index changes. 

If an array is passed an index outside of it's range, we get an "out of bounds" error.

Here is a pseudocode algorithm for summing all of the elements of an array `A[1..n]`.
```
sum = 0,
i = 1

while i <= n do
	sum = sum + A[i]
	i = i + i
endwhile

output sum
```
## Sequential Search
Sequential search, also called **linear search** is a simple algorithm for finding an item in an array

Consider the following problem: 
"Input: `n` numbers stored in an array `A[1..n]`, and a target number `key`.

Output: a boolean indicating if `key` is in the array.

Determine an algorithm to get this output from this input."

Sequential search offers 1 solution to this problem.

The algorithm is as follows:
- Set `i = 1`
- If `A[i] == key`, stop and return `true`
- Increment `i` by 1
- If `i > n`, stop and return `false`
- Otherwise repeat from step 2.

You can see full pseudocode for this algorithm below
```
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
### Time Complexity
Given the algorithm above, let's try and work out the time complexity of **sequential search**.

First we need to identify an **important operation** for us to count. We can identify comparing the key with an element of the array.

Next we count the operations needed for the **best case** and **worst case** scenario. In this case:
- The **best case** is that the key is the first element of the array, meaning we would find the key immediately and only make 1 comparison, $O(1)$
- The **worst case** is that the key is not in the list, or the key is the last element of the list, meaning it would take `n` comparisons to determine if it is in the list, $O(n)$

When designing algorithms and doing time complexity analysis, we rarely care deeply about the **best case** scenario. It is the **worst case** that really matters.

While it is technically more accurate to say that **sequential search** is $O(n)$ in the worst case, you may see people say that sequential search is $O(n)$ full stop, as we more or less only care about the worst case scenario.

This is true for most algorithms, although if two algorithms have a similar worst case time complexity, but one has a better best or average case time complexity, then we would prefer the one with the better best or average case time complexity.
### Binary Search
Binary search is a more efficient way of searching when the sequence of elements is **sorted**. 

The examples we will look at will be numbers, but it is important to recognise that for elements to be sorted we only need a way to determine if an element should go before or after another. This could be alphabetical, or some other ordering function, so binary search works on more than just arrays of numbers.

Consider the following problem: 
"Input: `n` numbers stored in an array `A[1..n]`, where `A[i] < A[i+1]` for all `1<=i<n`, and a target number `key`.

Output: a boolean indicating if `key` is in the array.

Determine an algorithm to get this output from this input with less than $O(n)$ time complexity in the worst case."

Now sequential search is not a valid solution to this problem as it has $O(n)$ time complexity in the worst case, but **binary search** offers us a solution.

The algorithm for binary search is as follows:
- Set `min = 1`
- Set `max = n`
- Set `i =`  the midpoint of `min` and `max`
- If `A[i] = key` stop and return `true`
- If `A[i] < key` set `max = i - 1`
- If `A[i] > key` set `min = i + 1`
- If `min > max` then stop and return `false`
- Otherwise repeat from step 3.

The strategy here is to remove half of the array with each check, leading to a much faster search algorithm. This does require you to have a sorted array, as otherwise there is no guarantee you will find `key` if it exists.

You can see full pseudocode for this algorithm below:
```
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

This works as described above. Note that since `mid` must be an integer we have to truncate (round down) `(min + max)/2`. 
### Time Complexity Analysis
Again we need to identify an **important operation** for us to count. Again, like sequential search, we can count the number of times we compare an element of `A` against `key`.

Then we need to count how many times this operation occurs in the best and worst case scenarios. In this case:
- The **best case** is that `key` is in the mid point of the list. This would mean we find `key` immediately, only requiring 1 comparison, $O(1)$.
- The **worst case** is that the `key` is the last item we check, or is not in the list. Since we divide the list in 2 every step this would mean we make $\lceil{\log_2n}\rceil + 1$ comparisons, $O(\log n)$.

$\lceil{x}\rceil$ is read as **ceiling of $x$** and means $x$ rounded to the nearest integer greater than $x$.




