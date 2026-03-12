## Bubble Sort in Linked Lists
Last lecture we implemented bubble sort on an array. How will our algorithm differ if instead we implemented it using a linked list?

Firstly, we would need pointers to keep track of a few things. We're going to want to traverse the list, and so we need a `curr` pointer to point at the node we are currently on. We also need to know where we should stop in any given run so we'll need a `last` pointer which will initially be set to `NIL`.

How we swap when we find 2 nodes that are out of order is also a bit different, but mostly the same.

We don't actually need to change the order of our nodes, we just need to change the order of the **data** that our nodes hold. This lets us us a very similar approach to the one we used before, just this time we access the `data` property of our nodes.

```
Swap-Node(a, b)
begin
	tmp = a.data
	a.data = b.data
	b.data = tmp
end
```

We also can't traverse the list using an index now, so we need to use a while loop and the next pointers. When we reach the end of our list we change our `last` pointer to the node before the last (`curr`), and set our `curr` back to `head`.

Now we can write our algorithm
```
if head == tail then //List is empty or only has 1 element
	STOP             // therefore doesn't need to be sorted
endif

last = NIL
curr = head

while last /= curr do
	while curr.next /= last do
		if curr.data > curr.next.data then
			Swap-Node(curr, curr.next)
		endif
		
		curr = curr.next
	endwhie
	
	last = curr
	curr = head
endwhile
```

The steps and the number of operations for this algorithm are identical to the steps and number of operations for bubble sort in an array.
## Selection Sort
[[Lecture 13 - Bubble Sort in Arrays|Last lecture]], I talked about how bubble sort is essentially if we applied our "find max" algorithm to the sequence repeatedly. Selection sort is even closer to that approach, except we find the minimum instead of the maximum. 

We're going to cover this algorithm as if we are using an array (`A[1..n]`).

The steps of this algorithm are:
1. Set start to 1 (or the first index);
2. Loop through the array to find the location of the smallest element;
3. Swap this element with the first element;
4. Increment start by 1;
5. If start is less than the length of the array (or the last index), repeat from step 2.

Which we can see is just our "find min" algorithm being run repeatedly on smaller sections of the array.

Since we've covered find minimum already, and covered how to swap elements in an array, I'm just going to show you the pseudocode for this algorithm
```
start = 1
while start < n do
	loc = start
	
	for i = (loc + 1) to n do
		if A[i] < A[loc] then
			loc = i
		endif
	endfor
	
	tmp = A[start]
	A[start] = A[loc]
	A[loc] = tmp
	
	start = start + 1
endwhile
```

If we analyse the time complexity of this by counting the number of comparisons. The outer loop runs $n-1$ times. Every time the outer loop runs, the inner loop also runs. This changes each time and so the first time it runs $n-1$ times, the second it runs $n-2$ times and so on.

This means that the total number of comparisons $t$ is 
$$
\begin{split}
t 
& = n-1 + n-2 + \cdots + 2 + 1 \\
& = \frac{n(n-1)}{2} \\
& = \frac{n^2}2 - \frac n2
\end{split}
$$

Which gives us a big-O of $O(n^2)$, which is the same as bubble sort.

However if also count the swap operations for selection sort, we see that we only swap elements $n$ times. In the worst case (a list is completely reversed) bubble sort will swap every time it compares which gives it $\frac{n^2}2 - \frac n2$ swaps. 

What this means is that selection sort, despite having the same big-O value as bubble sort, is actually more efficient.

I'm not going to walk over how to do selection sort with a linked list, but the same considerations for bubble sort need to be made. You should be able to do this easily enough,
## Insertion Sort
Insertion sort is another similar sorting algorithm, where we build up a sorted list by inserting elements in the correct space. In practice it works like an inverse bubble sort.

We're going to cover this algorithm as if we are working with an array `A[1..n]`.

The main steps are:
- Loop through values of `i` starting at 1 and ending at $n$
- At each `i` compare `A[i]` to all the elements to the left of `i`, stopping just before the first value that is smaller than `A[i]` (or when you reach the start of the array)
- Continuously swap the value of `A[i]` with all the values to the left in order to insert it in the right position (You can imagine this like bubbling down instead of up).

This algorithm is fairly similar to the others so I am just going to write the pseudocode
```
for i = 2 to n do
	j = i
	
	for j = i down to 2 do
		if A[j] > A[j-1] then
			tmp = A[j]
			A[j] = A[j-1]
			A[j-1] = A[j]
		endif
	endfor
endfor
```

This algorithm works by assuming that everything to the left of `i` is already sorted. This is true when `i==2` since a list with only `1` element is already sorted and the "bubbling down" means that it is also true after each loop iteration.

To find the time complexity of this algorithm we need to count the number of comparisons. Since this is essentially bubble sort in reverse the process is the same. In fact, it has the exact same time complexity for both sort and swap operations as bubble sort.

This means that this algorithm is big-O of $O(n)$.