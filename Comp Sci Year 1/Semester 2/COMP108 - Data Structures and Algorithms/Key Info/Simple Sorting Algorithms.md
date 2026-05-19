## Key Definitions

A **sorting algorithm** is an algorithm which takes an unsorted list/array and produces a sorted one.

**Bubble sort** is a sorting algorithm which works by repeatedly swapping out of order element resulting in the largest elements repeatedly *bubbling up* to the top of the list.

**Selection sort** is a sorting algorithm which works by repeatedly finding the smallest element of the list and swapping that value with the first unsorted element in the list.

**Insertion sort** is a sorting algorithm which works by building a new list by inserting elements of the original list in the correct place. In practice this works like a reversed bubble sort.
## Algorithms

**Bubble sort in arrays:** $O(n^2)$
```
for i = 1 to (n-2) do
	for j = 1 to (n-i) do
		if A[j] > A[j+1] then
			tmp = A[j]
			A[j] = A[j+1]
			A[j+1] = tmp
		endif
	endfor
endfor
```

**Bubble sort in linked lists:** $O(n^2)$
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

The remaining algorithms are only implemented (in this note) for arrays

**Insertion sort:** $O(n^2)$
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

**Selection sort:** $O(n^2)$
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
>In practice, selection sort is faster than both insertion and bubble sort despite having the same time complexity. 
>
>This is because selection sort only requires $O(n)$ swap operations, while the other two require $O(n^2)$ swap operations. 
>
>The $O(n)$ swap operations is dominated by the $O(n^2)$ comparisons which need to be made as part of selection sort.