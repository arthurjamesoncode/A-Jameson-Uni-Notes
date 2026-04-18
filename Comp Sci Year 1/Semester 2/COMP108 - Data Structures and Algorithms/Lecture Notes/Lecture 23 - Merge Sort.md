## Merge Sort
We have looked at sorting algorithms earlier in this module including:
- [[Lecture 13 - Bubble Sort in Arrays|Bubble Sort]]
- [[Lecture 14 - More Sorting Algorithms#Selection Sort|Selection Sort]]
- [[Lecture 14 - More Sorting Algorithms#Insertion Sort|Insertion Sort]]

Merge sort is a sorting algorithm which uses the [[Lecture 22 - Divide and Conquer Algorithms|divide and conquer]] technique. So how does it work? We will consider this as a problem of sorting **arrays**.

Well since it is a divide and conquer algorithm we have two steps:
- Split the array in two (divide)
- Sort each half and then combine them (conquer)

Like the examples before, we can perform the **conquer** step by recursively applying this algorithm to each smaller half. We just need a base case. 

Since an array containing only a single number can't be divided further and is already sorted, this is an excellent choice for our base case.

Now, the only question we are left with is: "How can we combine two sorted arrays to get a sorted array?"
## Merging
In previous examples, the operations to combine the smaller solutions were obvious. We added to find the sum, and compared to find the minimum. Combining sorted arrays are a bit more complicated. 

Imagine we have two sorted (ascending order) arrays given by
```
A1 = [1, 5, 8, 10]
A2 = [2, 6, 7, 9]
```

We know that each of the arrays are sorted, so how can we combine them?

Let's start by looking at a smaller problem: "How can we find the minimum of these two arrays?"

This solution to this problem is simple. Since we know the arrays are sorted, the smallest number must either be the first element of `A1` or the first element of `A2`. This means that we only need to compare 1 value.

Once we have found our minimum (the first value of our sorted array), if we simply remove this value, we are left with the same problem, combining two sorted arrays, except one of the arrays is now shorter.

This means that we can actually just repeatedly:
- Find the minimum of these two arrays;
- Place the minimum in our sorted array;
- Remove the minimum from it's respective array;
Until one array has no values left in it. When this happens, you can add all values from the non-empty array to the end of the sorted array.

In practice, we can use start and end pointers to control the window of the arrays we are concerned with. We do not need to actually remove elements.

Below you can see the pseudocode for the merge part of our solution
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

Now that we have this, we can look at how our full merge sort algorithm will work. Assume for convenience that $n$ is a power of 2.
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
## Time Complexity Analysis
Before, when looking at the time complexity analysis, we counted the number of boxes on our drawn tree. We could do this because each box only requires a single operation to combine each divided half.

Now, we combine using the `Merge` function that we wrote. This contains a loop, so it is clearly no longer constant time. How do we determine time complexity in this case?

Well first we need to see the time complexity of our `Merge` function. 
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

It has three non-nested loops which together which together ensure that every element of both input arrays get added to our `merged` array. 

It doesn't do anything else and so, if there are $r$ total items in the input arrays, will require exactly $r$ additions to the merged array. So the time complexity of our `Merge` function is $O(r)$ where $r=p+q$.

Now consider the the following example tree representing our merge sort algorithm.
![[merge_sort_tree.png]]

As we have shown, each box requires $O(r)$ time to merge (and therefore conquer). Notice that at each level though, there are a total of $n$ integers, where $n$ is the size of the original array. This means that each level take $O(n)$ time to resolve.

Since we split the array in two each time, there are $\log_2 n$ levels to this tree. Meaning we have to perform $n$ operations $\log_2 n$ times. This gives us a time complexity of $O(n\log n)$.

This is much faster than the $O(n^2)$ sorting algorithms that we were working with before, and is as fast as sorting algorithms can get.

Hopefully this shows you how powerful **divide and conquer** can be when designing algorithms.
