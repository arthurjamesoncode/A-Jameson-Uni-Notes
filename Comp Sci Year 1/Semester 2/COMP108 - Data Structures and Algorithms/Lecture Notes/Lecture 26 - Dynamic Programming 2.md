This lecture will be spent looking at an application of dynamic programming in assembly line scheduling. The model used is simplistic, but should help you understand why this algorithm method works.
## Assembly Line Scheduling
There are 2 assembly lines with $n$ stations which feed into each other.

$S_{i,j}$ denotes station $j$ on line $i$. $S_{1,j}$ and $S_{2,j}$ perform the same task but the time taken is different. The input is first fed into $S_{1, 1}$ or $S_{2,1}$ and must be fed into one of $S_{1, j}$ and $S_{2, j}$ for all $j\leq n$.

The assembly time at station $S_{i, j}$ is denoted by $a_{i,j}$. After each machine $S_{i,j}$, the input can either be instantly fed into the next machine on line $i$ (the current line), or transferred to the other line, but this takes some time. The time to transfer from $S_{i,j}$ is denoted by $t_{i,j}$.

You can see an example diagram representing this set up below:
![[assembly-line.png]]

The problem is this: Design an algorithm to determine which stations to go through in order the **minimise** the total time from start to end.

The naïve approach to solving this problem would be to just find every combination of station and see which one takes the smallest amount of time. Let's look at exactly how many combinations we need to check.

When $n=1$, there are only 2 stations so we are only comparing two combinations. Either we go through station 1 or 2.

When $n=2$, we can treat this as the same problem except that we have 2 ways to get to each final station. So we have 4 combinations to check.

If we keep doing this, what we will notice is that adding another machine at the start/end of each assembly line increases the number of combinations by a factor of 2 each time. So the total number of combinations is $2^n$.

This means that checking every combination would take $O(2^n)$ which is very bad. Let's see how we can lower this a bit using dynamic programming.

We want the minimum time to get from start to end. We know that the minimum time from start to end is the same as the minimum time to get to either $S_{1, n}$ or $S_{2,n}$ plus the respective machines assembly time.

To find the minimum time to $S_{1,n}$ we would need to find the minimum times to $S_{1,n-1}$ and $S_{2,n-1}$ and then compare them after adding their respective assembly time and (if applicable) transfer time. The same goes for finding the minimum time to $S_{2,n}$.

What you can see is that, when working with this style of algorithm, we actually need to repeatedly find the shortest time to the $i^{th}$ machine on each assembly line. If we do this, we can dramatically decrease the number of combinations we need to check.

Let's run this through with an example.
## Example
Take the assembly line given by the figure below
![[assembly-line-example.png]]

Let's work through this to find the minimum time to the end, and which machines to take.

First, we know we are going to store the minimum time to leave each machine. Since we are recording this we can make a table with 4 ($n$ in this case) rows which we can then fill. 

We will use $T(S_{i,j})$ to denote the minimum time to leave $S_{i,j}$, and $P(S_{i,j})$ to denote which machine is a direct predecessor of $S_{i,j}$ in the shortest path to it.

| $j$ | $T(S_{1,j})$ | $P(S_{1,j})$ | $T(S_{2,j})$ | $P(S_{2,j})$ |
| --- | ------------ | ------------ | ------------ | ------------ |
| 1   |              |              |              |              |
| 2   |              |              |              |              |
| 3   |              |              |              |              |
| 4   |              |              |              |              |
The time to leave $S_{1,1}$ or $S_{2,1}$ is the same as the assembly line at either machine. This let's us fill in the first two elements of our table.

| $j$ | $T(S_{1,j})$ | $P(S_{1,j})$ | $T(S_{2,j})$ | $P(S_{2,j})$ |
| --- | ------------ | ------------ | ------------ | ------------ |
| 1   | 5            |              | 15           |              |
| 2   |              |              |              |              |
| 3   |              |              |              |              |
| 4   |              |              |              |              |
Then, to find $T(S_{1,2})$ we have to take the minimum of $T(S_{1,1})+a_{1,2}$ and $T(S_{2,1}) + a_{1,2} + t_{2,1}$.

From this we know that 
$$
\begin{split}
T(S_{1,2})
&= \min(5 + 5, 15 + 5 + 1) \\
&= \min(10, 21) \\
&= 10
\end{split}
$$
Since we chose the path from $S_{1,1}$ we can also mark $S_{1,1}$ as our predecessor to $S_{1,2}$

| $j$ | $T(S_{1,j})$ | $P(S_{1,j})$ | $T(S_{2,j})$ | $P(S_{2,j})$ |
| --- | ------------ | ------------ | ------------ | ------------ |
| 1   | 5            |              | 15           |              |
| 2   | 10           | $S_{1,1}$    |              |              |
| 3   |              |              |              |              |
| 4   |              |              |              |              |
We can do pretty much the same thing to fill in our values for $S_{2,2}$.

| $j$ | $T(S_{1,j})$ | $P(S_{1,j})$ | $T(S_{2,j})$ | $P(S_{2,j})$ |
| --- | ------------ | ------------ | ------------ | ------------ |
| 1   | 5            |              | 15           |              |
| 2   | 10           | $S_{1,1}$    | 11           | $S_{1,1}$    |
| 3   |              |              |              |              |
| 4   |              |              |              |              |
I'm not going to run through the rest of this algorithm in detail since it takes a lot of time, however I recommend you do. The full completed table is below

| $j$ | $T(S_{1,j})$ | $P(S_{1,j})$ | $T(S_{2,j})$ | $P(S_{2,j})$ |
| --- | ------------ | ------------ | ------------ | ------------ |
| 1   | 5            |              | 15           |              |
| 2   | 10           | $S_{1,1}$    | 11           | $S_{1,1}$    |
| 3   | 19           | $S_{1,2}$    | 14           | $S_{2,2}$    |
| 4   | 20           | $S_{2,3}$    | 21           | $S_{2,3}$    |
Now we have a full table, we see that the minimum time spent to traverse the whole line is 20. We can find the optimal path by tracing back the predecessors of our optimal final machine (in this case $S_{1,4}$).

From this we know that the optimal path is:
- $S_{1,1}$
- $S_{1,2}$
- $S_{2,3}$
- $S_{1,4}$
## Pseudocode
Writing the pseudocode for this is similar to what we did [[Lecture 25 - Dynamic Programming|last lecture]]. 

Let's assume that the assembly times for the first line are given by `a1[1..n]` and the second line by `a2[1..n]` and that the transfer times for leaving the first line are given by `t1[1..n]` and the second line is given by `t2[1..n]`.

Our inputs are numbers, so we can use an array `m1[1..n]` to store the minimum times for the first line and `m2[1..n]` to store the minimum times for the second line.

We can then get started writing our pseudocode
```
m1[1] = a1[1]
m2[1] = a2[1]

for j = 2 to n do
	m1[j] = min(m1[j-1] + a1[j], m2[j-1] + a1[j] + t2[j-1])
	m2[j] = min(m2[j-1] + a2[j], m1[j-1] + a2[j] + t1[j-1])
endfor

return min(m1[n], m2[n])
```
Note that if we also want to get the path, we need to store the predecessor along with the minimum time.
## Time Complexity Analysis
If you look at the body of the for loop from our pseudocode, you can see that no operation inside the loop is greater than constant time.

The operations in the loop are:
- Finding the minimum of two elements
- Indexing an array
- Summing Values

All of these are $O(1)$, meaning that we perform $O(1)$ operations $n-1$ times as part of our loop giving us a big-O of $O(n)$.

You can also understand this as finding the minimum of each machine given the previous machines takes constant time, so the total time taken is the same as the number of machines. In this case we have $2n$ machines, meaning that it takes $2n$ operations and still has a big-O of $O(n)$.

Note that if, instead of having a fixed number of assembly lines, we had $m$ assembly lines. Now we have $m\times n$ machines in total. So to find the time complexity of this algorithm we need to look at how long it takes to find the minimum of the $j^{th}$ machine in a given assembly line given the previous layer.

Before it took constant time to find the minimum of a given machine since we had a **fixed** number of lines. Now we don't we have $m$ lines, and therefore must find the minimum of $m$ values for every machine. The time complexity of finding the minimum of $m$ values is $O(m)$.

This means that in total we need to find perform an $O(m)$ operation $mn$ times, meaning that the big-O for this algorithm is $O(m^2n)$.