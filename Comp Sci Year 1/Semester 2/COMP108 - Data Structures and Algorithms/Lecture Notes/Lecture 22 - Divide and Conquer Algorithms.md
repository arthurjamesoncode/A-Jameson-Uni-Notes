## Divide and Conquer Algorithms
"Divide and conquer" is one of the best known algorithm design techniques. 

It is an approach defined by:
- Splitting the problem down into smaller, more manageable problems of (usually) equal size  (Divide).
- Solving these smaller instances of this problem (Conquer).
- Combining these smaller solutions to form a solution to the whole problem.

Divide and conquer algorithms are typically defined recursively, but it is possible to define them iteratively as well. If you would like a recap of recursion I recommend going to [[Lecture 7 - Recursion|this note]] from the COMP105 course. 

This lecture will be spent looking at two simple problems we have seem before, 
- Sum of an array
- Min of an array
and seeing what a divide and conquer solution to them looks like.

>It is worth noting that the divide and conquer solutions to these algorithms are worse than the simple iterative approach we used before. This is true both in ease of implementation and efficiency. This will be discussed more when we get to time complexity analysis.
>
>These algorithms have simply been chosen to introduce this concept because they are simple. We will see problems better suited to these types of algorithms in the following two lectures.
## Summing an Array
Given an array of $n$ numbers, how could we apply a divide and conquer algorithm to find their sum?

We know we need to **divide** the problem down into smaller parts, but how can this help us? I think a useful first step is to determine how we can **combine** these solutions, since there is no use in solving these smaller problems unless we know how it can lead to a full solution. The easiest way to figure this out is to split the problem in two, imagine that we already have solved these smaller problems, and see how that can help us.

In this case, we can imagine that we have split the **array** in two, and have already found the **sum** of both of these smaller arrays. Since we want to find the sum of the whole array, we know that we can **combine** them by **adding** the sums of these two half arrays.

Now we have two steps:
- Split the array into two (Divide)
- Find the sum of both smaller arrays and add them (Conquer)

So how can we find the sum of these smaller arrays? Well if we identify a stopping point (recursive base case), where we can no longer divide and the answer is immediately clear, then we can simply apply the divide and conquer algorithm to these smaller arrays.

In the case of this problem, we will eventually split the array down into single numbers. When this happens, we will be unable to split it further and the sum of a single number is obvious (the number itself). This makes this a perfect base case for our recursive algorithm.

Imagine we have an array of 8 numbers and we apply this algorithm to it. Below you can see a figure of what this looks like:
![[d&c_sum.png]]

The black arrows indicate the **divide** step and the red arrows indicate the **conquer** step.

We can also define this algorithm in pseudocode. For the sake of simplicity, assume that $n$ is a power of 2. 

>If $n$ is not a power of 2 this same idea still works, you just need a way to handle when an array can't be divided easily in two.

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

In this recursive approach, the sum of the left subarray is found before the sum of the right sub array. This is because recursion builds a **call stack** and if we remember our [[Lecture 18 - Paths and Circuits in Graphs#Searching Algorithms|searching algorithms]], we know that using a **stack** to traverse a graph/tree leads to **depth first** traversal. 

>The way this has been written specifically does a **post order** traversal of the **binary tree** made up of the sums of the subarrays. Reminder on the types of traversals [[Lecture 16 - Trees#Binary Trees|here]].

## Finding the Minimum of an Array
We can find the minimum of an array in a very similar approach to how we found the sum:
- Split array in two (**divide**)
- Find the minimum of both arrays and compare them (**conquer**)
Again, we can use a single element as the base case, since we cannot divide this further and the minimum of a single number is the number itself.

This process is identical to finding the sum, the only difference is that operation we use to **combine them** (comparison instead of addition).

Again we can visualise this with the following figure:
![[d&c_min.png]]

Again the black arrows represent the **divide** operations, and the red arrows represent the **conquer** operations.

Just like before we can write our pseudocode for this. Since all we are changing is the method of combining them, we only need to change a few lines.

```
//Takes input of an array A indexed [1..n]

RecursiveMin(A, p, q)
begin
	if p == q then 
		return A[p]
	endif
	
	newQ = (p + q - 1)/2
	newP = (p + q + 1)/2
	
	min1 = RecursiveSum(A, p, newQ)
	min2 = RecursiveSum(A, newP, q)
	
	if min1 < min2 then
		return min_1
	else
		return min_2
	endif
end

RecursiveMin(A, 1, n) //Initial call
```
## Time Complexity Analysis
The time complexity of both of these algorithms is identical, so we will cover them together.

So far, we have usually analysed time complexity by looking at operations within loop iterations. 

There are no loops in the pseudocode programs we have written today, so how can we count them?

Well we still need to pick an operation and count it, how we do this just becomes a bit more complicated.

The most simple operation to count is the number of **returns** executed by the algorithm.

If we look back at our figure, we can see that every rectangle returns **exactly once**. So how can we find the number of rectangles as a function of $n$.

![[d&c_min.png]]

Well (assuming for simplicity that $n$ is a power of two) we start with 1 rectangle on layer 1, this splits into 2, then 4, and continues to double each layer until eventually we get to $n$ rectangles on the final layer.

Since we want the total number of rectangles, we want to sum the number of rectangles on each layer. So the total number of operations $x$ is given by
$$
x=\sum_{i=0}^{\log_2n}2^i
$$

First lets table out what this looks like for some small $n$

| $n$ | Operations |
| --- | ---------- |
| 1   | 1          |
| 2   | 3          |
| 4   | 7          |
| 8   | 15         |
From this, we can intuit that this takes $2n-1$ operations, since it holds for these examples. This is true, and I have provided a proof of this below.

This means that these algorithms have a big-O of $O(n)$. 

Compared to their iterative approaches, they do use more operations. By factor of about 2. This means that in this case they are not as good as the simple, linear, iterative algorithms.

However, when applied to more complicated problems, which don't have solutions in **linear time**, (like sorting) we can see massive benefits from this type of algorithm design. For a good example of this turn to [[Lecture 23 - Merge Sort|next lecture]].
### Proof
To simplify things we are only going to use powers of 2 for $n$. As such we will perform induction on $m$ where $n=2^m$. 

>Observe that $m=\log_2 n$, and $2^{m+1} = 2n$.

**Claim**:
For all $m\in\mathbb N$
$$
\sum_{i=0}^{m}2^i = 2^{m+1}-1
$$
**Base Case:** $m=0$
When $m=0$, $2^m=1$ and
$$
\sum_{i=0}^{m}2^i = 2^0=1
$$

Observe that 
$$
2^1-1 = 1
$$
and so the claim holds for the base case of $m=1$.

**Inductive Step:** Assume the claim is true for $m=k$
We want to find
$$
\sum_{i=0}^{k+1}2^i
$$
which we can rewrite as 
$$
(\sum_{i=0}^{k}2^i) + 2^{k+1}
$$
Based on our inductive hypothesis
$$
\sum_{i=0}^{k}2^i = 2^{k+1}-1
$$
meaning that we can substitute this back in to our equation
$$
\begin{split}
(\sum_{i=0}^{k}2^i) + 2^{k+1} 
& = 2^{k+1} - 1 + 2^{k+1} \\
& = 2(2^{k+1}) - 1 \\
& = 2^{k+2} - 1 \\
& = 2^{(k+1) + 1} -1
\end{split}
$$

Since 
$$
2^{(k+1) + 1} -1
$$
Is of the same form as 
$$
2^{m+1}-1
$$
We know that if the claim holds for $m=k$, it must also hold for $m=k+1$.

**Conclusion:** Since we have shown the claim to hold in both our base case and inductive step we have shown the claim to be true for all $m\in\mathbb N$.



