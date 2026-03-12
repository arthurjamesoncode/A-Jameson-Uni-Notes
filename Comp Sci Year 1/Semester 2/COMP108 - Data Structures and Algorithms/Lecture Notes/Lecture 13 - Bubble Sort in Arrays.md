## Sorting
Consider the task of defining an algorithm to **sort** a sequence of $n$ numbers into **ascending order**.

This is very well defined problem in computer science, and there are a number of **sorting algorithms:**
- Bubble Sort
- Insertion Sort
- Merge Sort
- Quick Sort
- Selection Sort

All of these can be applied to sort algorithms into any order, given that there is someway to compare 2 elements to know which should come first.

Today we will be running through the simplest (and worst) of these algorithms **bubble sort**, and specifically how you can implement it when the sequence of numbers you are working with is an **array**.
## Bubble Sort
If you recall [[Lecture 6 - Finding Min & Max of Arrays|lecture 6]], we created an algorithm which finds the maximum value of an array. Bubble sort is essentially if you applied that algorithm to find the maximum value, then applied it again to find the second max, and so on until you have a sorted array. 


The way it works is simple:
- Start from the first element in the array
- Traverse the array and swap elements which are not in ascending order
- When you reach the top, the last item will be the largest
- Repeat from the beginning, stopping at the second to last item (and so on)

This is called bubble sort since the process of swapping is like the largest item in the list is a **bubble** which rises to the top. If you want to see a visualisation of bubble sort you can look [here](https://www.hackerearth.com/practice/algorithms/sorting/bubble-sort/visualize/).

This is why I think this algorithm is similar to implementing our "find the maximum" algorithm that many times, although bubble sort is actually slightly worse than this approach because there can be more than $n$ swap operations. [[Lecture 14 - More Sorting Algorithms#Selection Sort|Selection sort]], which is covered next lecture, is even closer to this approach.

So how can we implement this algorithm?

Firstly, we need a loop to iterate through the list. We know that we will need to iterate through the list a number of times, so we will need another loop to put this first loop in.

So what should our loop conditions be? For the 1st iteration, we will need to go through the full list and so we know that we will be checking up to $n$. For the 2nd iteration we will need to loop to $n-1$ and so on.

We can use the value of the iterator in the outer loop along with the length of the list to control where the end of our inner loop should be.

Then how can we swap the $i$th and $j$th values? We might be tempted to do something like:
```
A[i] = A[j]
A[j] = A[i]
```
but this won't work as the information in `A[i]` is lost when we reassign it to `A[j]`. So we need to use a temporary value to store `A[i]` before we reassign `A[i]`.

If we put all this together we get
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

## Time Complexity Analysis
We will use the number of comparisons to analyse the time complexity of this algorithm

So the outer loop runs exactly $n-2$ times. Every time the outer loop runs the inner loop runs as well.

You can see the number of comparisons the inner loop makes based on this table:

| `i` | number of comparisons |
| --- | --------------------- |
| 1   | n-1                   |
| 2   | n-2                   |
| ... | ...                   |
| n-2 | 2                     |
| n-1 | 1                     |
And so we see the total number of comparisons is the same as the sum of all numbers up to $n-1$, which we know to be
$$
\begin{split}
\frac{n(n-1)}{2}
& = \frac{n^2-n}{2} \\
& = \frac{n^2}2 - \frac{n}2
\end{split}
$$
giving us a big-O of $O(n^2)$.