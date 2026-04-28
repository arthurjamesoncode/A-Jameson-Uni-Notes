## Question 1 - Merge Sort
**Question:** Suppose we are given the following numbers: 40, 23, 11, 35, 15, 30, 18, 25. If we apply merge sort to sort these numbers into ascending order, the final merge step would be to merge the two sorted sequences:
$$
(11, 23, 35, 40) \text{ and } (15, 18, 25, 30)
$$
Draw figures to show this final merge step. Use two pointers to point to the two sorted sequences. Show step by step how the pointers move to obtain the final merged sequence.

**Answer:** I have done this using a table to represent each step. The first table represents the initial.

| Input 1 | Pointer 1    | Input 2 | Pointer 2    | Output |
| ------- | ------------ | ------- | ------------ | ------ |
| 11      | $\leftarrow$ | 15      | $\leftarrow$ |        |
| 23      |              | 18      |              |        |
| 35      |              | 25      |              |        |
| 40      |              | 30      |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |


| Input 1 | Pointer 1    | Input 2 | Pointer 2    | Output |
| ------- | ------------ | ------- | ------------ | ------ |
| 11      |              | 15      | $\leftarrow$ | 11     |
| 23      | $\leftarrow$ | 18      |              |        |
| 35      |              | 25      |              |        |
| 40      |              | 30      |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |

| Input 1 | Pointer 1    | Input 2 | Pointer 2    | Output |
| ------- | ------------ | ------- | ------------ | ------ |
| 11      |              | 15      |              | 11     |
| 23      | $\leftarrow$ | 18      | $\leftarrow$ | 15     |
| 35      |              | 25      |              |        |
| 40      |              | 30      |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |

| Input 1 | Pointer 1    | Input 2 | Pointer 2    | Output |
| ------- | ------------ | ------- | ------------ | ------ |
| 11      |              | 15      |              | 11     |
| 23      | $\leftarrow$ | 18      |              | 15     |
| 35      |              | 25      | $\leftarrow$ | 18     |
| 40      |              | 30      |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |

| Input 1 | Pointer 1    | Input 2 | Pointer 2    | Output |
| ------- | ------------ | ------- | ------------ | ------ |
| 11      |              | 15      |              | 11     |
| 23      |              | 18      |              | 15     |
| 35      | $\leftarrow$ | 25      | $\leftarrow$ | 18     |
| 40      |              | 30      |              | 23     |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |

| Input 1 | Pointer 1    | Input 2 | Pointer 2    | Output |
| ------- | ------------ | ------- | ------------ | ------ |
| 11      |              | 15      |              | 11     |
| 23      |              | 18      |              | 15     |
| 35      | $\leftarrow$ | 25      |              | 18     |
| 40      |              | 30      | $\leftarrow$ | 23     |
|         |              |         |              | 25     |
|         |              |         |              |        |
|         |              |         |              |        |
|         |              |         |              |        |

| Input 1 | Pointer 1    | Input 2 | Pointer 2 | Output |
| ------- | ------------ | ------- | --------- | ------ |
| 11      |              | 15      |           | 11     |
| 23      |              | 18      |           | 15     |
| 35      | $\leftarrow$ | 25      |           | 18     |
| 40      |              | 30      |           | 23     |
|         |              |         |           | 25     |
|         |              |         |           | 30     |
|         |              |         |           |        |
|         |              |         |           |        |
Since input 2 has been exhausted we can then add the remaining items from input 1 to get our full output.

| Input 1 | Pointer 1 | Input 2 | Pointer 2 | Output |
| ------- | --------- | ------- | --------- | ------ |
| 11      |           | 15      |           | 11     |
| 23      |           | 18      |           | 15     |
| 35      |           | 25      |           | 18     |
| 40      |           | 30      |           | 23     |
|         |           |         |           | 25     |
|         |           |         |           | 30     |
|         |           |         |           | 35     |
|         |           |         |           | 40     |
**Question:** Merge sort makes use of an algorithm to merge two sorted sequences. Assume that the given two sequence are already in descending order. Modify the pseudo code Merge() in the lecture notes to merge two descending ordered sequences into one descending ordered sequence.

**Answer:** 
```
Algorithm Merge(B[1..p], C[1..q], A[1..(p + q)]) 
	i ← 1, j ← 1, k ← 1 
	while i ≤ p AND j ≤ q do 
	begin 
		if B[i] ≥ C[j] then //only changed line
			A[k] ← B[i], i ← i + 1 
		else 
			A[k] ← C[j], j ← j + 1 
		k ← k + 1 
	end 
	if i == p + 1 then 
		copy C[j..q] to A[k..(p + q)] 
	else 
		copy B[i..p] to A[k..(p + q)]
```
## Question 2
Suppose there are two assembly lines each with 4 stations, $S_{i,j}$. The assembly time is given in the circle representing the station and the transfer time is given next to the arrow from one station to another.

**Question:** 
Using dynamic programming, fill in the table of the minimum time $f_i [j]$ needed to get through station $S_{i,j}$ . You should also show all the intermediate steps in computing these values, e.g., in computing $f_1[2]$, you need to specify that $f_1[2] = \min\{\_ ,\_ \}$.

**Answer:**

| $j$ | $f_1[j]$ | $f_2[j]$ |
| --- | -------- | -------- |
| 1   | 3        | 3        |
| 2   | 8        | 5        |
| 3   | 10       | 9        |
| 4   | 11       | 14       |
**Intermediate Steps:**
$$
\begin{split}
f_1[2] 
&= \min\{f_1[1] + 0 + 5,f_2[1] + 3 + 5\} \\
&= \min\{3 + 0 + 5,3 + 3 + 5\} \\
&= \min\{8,11\} \\
&= 8 \\
\\
f_2[2] 
&= \min\{f_1[1] + 4 + 2,f_2[1] + 0 + 2\} \\
&= \min\{3 + 4 + 2,3 + 0 + 2\} \\
&= \min\{9,5\} \\
&= 5 \\
\\
f_1[3] 
&= \min\{f_1[2] + 0 + 4,f_2[2] + 1 + 4\} \\
&= \min\{8 + 0 + 4,5 + 1 + 4\} \\
&= \min\{12,10\} \\
&= 10 \\
\\
f_2[3] 
&= \min\{f_1[2] + 0 + 4,f_2[2] + 1 + 4\} \\
&= \min\{8 + 1 + 4,5 + 0 + 4\} \\
&= \min\{13,9\} \\
&= 9 \\
\\
f_1[4] 
&= \min\{f_1[3] + 0 + 1,f_2[3] + 3 + 1\} \\
&= \min\{10 + 0 + 1,9 + 3 + 1\} \\
&= \min\{11,13\} \\
&= 11 \\
\\
f_2[4] 
&= \min\{f_1[3] + 2 + 5,f_2[3] + 0 + 5\} \\
&= \min\{10 + 2 + 5,9 + 0 + 5\} \\
&= \min\{17,14\} \\
&= 14 \\
\end{split}
$$
**Question:** What is the minimum time $f^∗$ needed to get through the assembly line?

**Answer:** By our table, $f^*=11$.

**Question:** Which stations should be chosen to achieve the minimum time?

**Answer:** 
In reverse order:
- $S_{1,4}$
- $S_{1,3}$
- $S_{2,2}$
- $S_{2,1}$
## Question 3
Consider the following recurrence.
$$
T(n)=\cases{
\begin{split}
1 & \text{ if } n = 0 \text{ or } n = 1 \\
2 & \text{ if } n = 2 \\
T(n-1) + T(n-3) & \text{ if } n > 2
\end{split}
}
$$
**Question:** Design and write a pseudo code for a recursive procedure to compute $T(n)$.

**Answer:**
```
T(n)
begin
	if n == 2 then 
		return 2
	endif
	
	if n == 0 OR n == 1 then
		return 1
	endif
	
	return T(n-1) + T(n-3)
end
```

**Question:** Draw the execution tree for $T(7)$.

**Answer:**
![[execution-tree.drawio.png]]

**Question:** Using the concept of dynamic programming, rewrite your recursive procedure into a non-recursive one.

**Answer:**
```
T(n)
begin
	table = [0..n]
	table[0] = 1
	table[1] = 1
	table[2] = 2
	
	for i = 3 to n do
		table[i] = table[i-1] + table[i-3]
	endfor
	
	return table[n]
end
```
## Question 4
In the last tutorial, you have been asked to design a divide-and-conquer algorithm to find the product of the numbers in an array $A[ ]$ with $n$ integers $A[1]..A[n]$. 

**Question:** Explain why the time complexity $T(n)$ of your algorithm can be described by the following recurrence.
$$
T(n)=
\cases{
\begin{split}
1 &\; \text{ if } n=1\\
2\cdot T\Bigl(\frac n2\Bigr) + 1 &\; \text{ if } n > 1
\end{split}
}
$$

**Answer:** I've pasted the algorithm I wrote from last week's tutorial.
```
Product(A, start, end)
begin
	if start == end then
		return A[start]
	endif
	
	mid = (start + end) div 2
	left = Product(A, start, mid)
	right = Product(A, mid + 1, end)
	
	return (left * right)
end

Product(A, 0, n) //initial call
```

$n$, in the given recurrence, represents the number of elements in the list.

We can find time-complexity by counting the number of times our algorithm returns.

As you can see, if there is only one item in the list (when `start == end`) it takes a single return operation. This covers the first case of the recurrence.

If there are multiple items in the list, the list is split in two, the algorithm is applied to both halves, and the results are multiplied together and then returned. 

This covers the second case of the recurrence as the time taken to apply the algorithm to one half of the list is $T(\frac n2)$, and it takes a single return operation outside of that.