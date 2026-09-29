## Finding Max/Min Value
Consider the following problem:

"Input: An array `A` containing $n$ positive numbers, indexed with the values `[1..n]`.

Output: The maximum value of the elements of `A`

Design an algorithm to determine the output given the input."

Last lecture, [[Lecture 5 - Array Basics & Searching]], we saw how a sorted array allows us to use binary search to find an element of the array.

If we think like this, we know that if the array is sorted in ascending order we simply need to take `A[n]`, and if it is sorted in descending order we can take `A[1]`. 

But what about when it isn't sorted? Well the obvious solution would be to sort it and then take the correct value after the array has been sorted. 

This works, and is preferable when having a sorted array is useful for some other operations we want to perform, but can we find the value faster than we can sort the array?

The fastest sorting algorithms take $O(n\log n)$ time. Can we do better than this for finding the maximum?

What if we just stored the first value in a variable, and then checked it against every other value in the list, changing the variables value to any value greater than it's current value?

This works, it will find the maximum value, but how quickly? Well it always compares the value stored in our variable with every item in the list except the first. This means it makes $n-1$ comparisons, giving it a time complexity of $O(n)$. This is less than the time complexity of sorting the array $O(n\log n)$.

You can see the full pseudocode for this below:
```
m = A[1]

for i = 2 to n do
	if A[i] > m then
		m = A[i]
	endif
endfor

output m
```

We can actually change this algorithm in order to find the minimum value by only changing 1 line. Instead we must check `if A[i] < m`.
## Finding Max/Min Locations
Now consider if, instead of just finding the max value of the array, we want to find both the max value and the **location** of the max value.

This question becomes a bit more interesting because now we some more questions. Mainly:
- If there are multiple instances of the max value, which location do we return
- Is there a way for us to return all locations of the max value

Firstly, lets assume that we want to return the **first** location of the max value. In this case the algorithm is very similar to the one we wrote before. 

Now we simply need to store the location of the current maximum, and index the value whenever we compare. We also must make sure to return both the location and the maximum value. You can see the full code below.
```
loc = 1

for i = 2 to n do
	if A[i] > A[loc] then
		loc = i
	endif
endfor

output loc and A[loc]
```

If we wanted to instead output the **last** location of the max value, we simply need to change the line `A[i] > A[loc]` to `A[i] >= A[loc]`, which means that the location will be overwritten if it sees that a `A[i]` is equal to `A[loc]`.

In both of these cases the algorithm still makes $n-1$ comparisons giving both of these solutions a time complexity of $O(n)$

But how about if we wanted to find **all** the locations of the max value.

Well, there are a few ways to go about this. The first is that we could run our max value algorithm once and then iterate through the loop again outputting any instances of the found max value.

So the full pseudocode would be
```
m = A[1]

for i = 2 to n do
	if A[i] > m then
		m = A[i]
	endif
endfor

for i = 1 to n do
	if A[i] == m then
		output i
	endif
endfor
```
This takes $2n-1$ comparisons, which still gives us a time complexity of $O(n)$, but is there a way to get the same output without looping through again?

The answer is yes, but it still requires some extra operations. What if we added the locations of the current max to an output array whenever we find them. If the max ever increases, we overwrite the array with one that contains only the current element. This allows us only run through the array once instead of twice.

The full pseudocode for this approach is below.
```
m = A[1]
out = [1]

for i = 2 to n do
	if A[i] == m then
		add i to out
	else if A[i] > m then
		m = A[i]
		out = [i]
	endif
endfor

output out
```
This does require extra operations, adding the values to this new array.

In the worst case, every element of the initial array can be added to this new array before the end. This means that there are $n-1$ comparisons and $n$ additions meaning there are $2n-1$ operations still giving this a time complexity of $O(n)$.

While this doesn't seem any better than the first solution of running through the array twice, it does actually speed up the average performance as running through the array twice is guaranteed to need $2n-1$ operations but this second algorithm only requires $2n-1$ operations in the worst case. 

There is still no way to find all of the locations of a maximum value in only $n$ operations.
## Finding 1st and 2nd Max/Min Values
How about if we wanted to find both the max value and the second max value of an array.

This complicates our algorithm a bit as now we have more conditions to check.

Firstly lets consider our initial values. We cant simply set `m1` and `m2`, which represent our first and second max values, to `A[1]` and `A[2]` as this will depend on whether `A[1] > A[2]` or otherwise. So we must set `m1` to the maximum of `A[1]` and `A[2]` and set `m2` to the minimum of `A[1]` and `A[2]`.

Now, we have our initial values let's consider the logic within the loop. If the value we check is greater than `m1`, we want to change `m1` to this value, and change `m2` to the old value of `m1`. If it is not greater than `m1` but is greater than `m2` we want to change the value of `m2` this value. If neither of those conditions are true we, we don't want to do anything.

You can see the full pseudocode for this below.
```
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
Note that as we place the `if A[i] > m2` inside of the else block, this is only ever checked in `A[i] > m1` is false. Therefore we don't need to check if `A[i] <= m1`.

To analyse the time complexity of this, again we just want to count the number of comparisons. In the worst case for each iteration of the loop, we check both `A[i] > m1` and `A[i] > m2` meaning that there are 2 comparisons. Since we start on the third item of the array there are $n-2$ iterations completed. This means that, in the worst case, there are $2(n-2)=2n-4$ comparisons, giving this algorithm a time complexity of $O(n)$.

Note that we could do something similar to find the 1st, 2nd, and 3rd max values of this array. For every value we add the we would add roughly $n$ more comparisons.

In a future lecture, we will cover **bubble sort**, **insertion sort**, and **selection sort**. These are 
sorting algorithms that work by repeatedly finding the maximum or minimum value of an array. Based on what we've said here, what do you think the time complexity of these algorithms would be?