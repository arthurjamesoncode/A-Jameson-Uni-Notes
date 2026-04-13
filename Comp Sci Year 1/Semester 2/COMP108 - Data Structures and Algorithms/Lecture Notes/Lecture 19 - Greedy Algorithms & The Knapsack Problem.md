## Greedy Algorithms
Greedy algorithms are a kind of algorithm that can be applied to various problems.

A greedy algorithm is an algorithm that attempts to make the "best move possible" at every step. The "best move possible" at each step is the move that moves you closest to the goal state while only taking into account the current step.

This might sound confusing but should make more sense if given an example. 

Imagine we wanted to determine the minimum number of coins to make various target amounts. A greedy algorithm keep track of the total of the currently selected coins and at each step take the largest possible coin available which wouldn't push us over the target.

Greedy Algorithms have some key advantages:
- They are usually simple to implement
- Don't require much effort at each step
- Usually find a solution quickly
- The solution found is usually pretty good

They also have one big disadvantage: The solution found may not be the best one.

Some problems are very well suited to greedy solutions, and a greedy algorithm will find the best solution:
- Minimum Spanning Tree (Kruskal's algorithm)
- Single-Source Shortest-Paths (Dijkstra's algorithm)

For some problems, however, a greedy algorithm will not find the best solution:
- The coin change problem (described above)
- The Knapsack Problem (shown below)

We will be looking at the minimum spanning tree problem in the next lecture note, but for now we will go over a problem for which greedy algorithms are not well suited.
## The Knapsack Problem
Imagine a fire started in your house. No other people are in the house but, all of your belongings are. 

You have a knapsack, but you have a limited amount of strength so can only carry a weight of $W$. You are forced to decide which items you want to take and you want to choose the subset of items with the highest value. 

How can you go about doing this?

This is an (informal) explanation of what the knapsack problem is. Below I will give a more formal definition

"Given $n$ items with weights $w_1,w_2,...,w_n$ and values $v_1, v_2, ...,v_n$ and a knapsack with capacity $W$, how can you find the most valuable subset of items that can fit in the knapsack?"

Well first let's think about how we could approach this. The most intuitive response is to check every possible subset of items, and take the most valuable subset of items which don't exceed the knapsack's capacity.

We know that the set of all subsets of a set is the power set. We saw in [[Lecture 14 - The Cardinality of Sets]] that the cardinality (size) of the power set of a set with $n$ items is $2^n$.

This means that checking all of the subsets takes exponential ($O(2^n)$) time. This is **really** slow.

What if we could do a bit better by trying a **greedy** approach? Well there are a two decent ways to do this:
- Choose the item with the next largest value if total weight is less than or equal to the capacity
- Choose the item with the next largest value to weight ratio if the total weight is less than or equal to the capacity

>The only thing that differs about these two approaches is the way that we order the items. Aside from that they are the same, including in time complexity.
### Sort by Value
Lets start with "Choose the item with the next largest value if total weight is less than or equal to the capacity".

We could use one of the algorithms we made in [[Lecture 6 - Finding Min & Max of Arrays]] to repeatedly find maximum value item from the list, however that algorithm takes $O(n)$ to perform and we would need to perform it $O(n)$ times meaning that this approach would take $O(n^2)$ time.

While $O(n^2)$ is pretty good compared to $O(2^n)$, we can still do a little better. We can sort the list into descending order of value first. Then once we have sorted it we can check the items in sequential order. 

The best sorting algorithms (which are yet to be covered) take $O(n\log n)$ time, and checking the items in sequential order takes $O(n)$ time. $O(n\log n)$ dominates $O(n)$ so this algorithm is only $O(n\log n)$ which is much better than $O(n^2)$.

Lets run through this with an example. Let $W=50$ and the items be given by the following list:
$$
\begin{split}
1:&\; w=10,\;v=60 \\
2:&\; w=20,\;v=100 \\
3:&\; w=30,\;v=120
\end{split}
$$
- First the algorithm selects item 3, making the total value 120 and the total weight 30
- Next the algorithm selects item 2, making the total value 220 and the total weight 50
- The algorithm has now reached the exact capacity of the knapsack, and exits.

In this case, the algorithm selects the **optimal** solution, meaning there is no more valuable subset to choose. Is this always the case?

Well the answer is no, and we will see an example of this now.

Let $W=10$ and the items be given by the following list
$$
\begin{split}
1:&\; w=7,\;v=42 \\
2:&\; w=3,\;v=12 \\
3:&\; w=4,\;v=40 \\
4:&\; w=5,\;v=25
\end{split}
$$
- First the algorithm selects item 1, making the total value 42 and the total weight 7
- Next it tries to select item 3, but this exceeds the weight limit 
- Next it tries to select item 4, but this exceeds the weight limit
- Next it selects item 2, making the total value 54 and the total weight 10
- The algorithm has now reached the exact capacity of the knapsack, and exits.

In this case we can see that it clearly hasn't chosen the best solution. If instead we chose item 3 and item 4, then the final value would be 65.

But this could just be a problem with how we order it right? I mean item number one is the most valuable but also the heaviest. What if instead we order by the weight to value ratio.
### Sort by Ratio
Now let's try the second approach.

We'll reuse the example above, where $W=10$ and the items given by the following list. For convenience $v/w$ is also noted.
$$
\begin{split}
1:&\; w=7,\;v=42,\;v/w=6 \\
2:&\; w=3,\;v=12,\;v/w=4 \\
3:&\; w=4,\;v=40,\;v/w=10 \\
4:&\; w=5,\;v=25,\;v/w=5
\end{split}
$$
- First the algorithm chooses item 3, making the total value 40 and the total weight 4
- Next it tries to select item 1, but this exceeds the weight limit
- Next it selects item 4, making the total value 65 and the total weight 9
- Next it tries to select item 2, but this exceeds the weight limit
- The algorithm has run out of items to choose and stops

Note that this is the optimal solution to this. So does changing this metric now mean that this algorithm finds the optimal solution every time?

Well no, and we'll see this by going back to our first example.

Let $W=50$ and the items be given by the following list
$$
\begin{split}
1:&\; w=10,\;v=60,\;v/w=6 \\
2:&\; w=20,\;v=100,\;v/w=5 \\
3:&\; w=30,\;v=120,\;v/w=4
\end{split}
$$
- First the algorithm chooses item 1, making the total value 60 and the total weight 10
- Next the algorithm chooses item 2, making the total value 160 and the total weight 30
- Next it tries to choose item 3, but this exceeds the weight limit
- The algorithm has run out of items to choose and stops

We know that this is not optimal as we saw before that choosing items 2 & 3 was the optimal solution.

So is it possible to always find an optimal solution with a greedy approach?
## Greedy Isn't Always Great
Greedy algorithms can perform really badly sometimes. 

For the "Sort by Value" algorithm, imagine a set of $n$ items ($n>3$) where one item has $v=2$ and $w=W$, and $n-1$ items with $v=1$ and $w=\frac{W}{n-1}$.

The optimal solution in this case is to choose all of the small items giving a total value of $n-1$, while the solution the greedy algorithm turns up is only the single item with $v=2$.

For the "Sort by Ratio" algorithm, imagine 2 items one with $v=2$ and $w=1$, and the other with $v=W$ and $w=W$.

The optimal solution is obviously to choose the larger of the two items, but greedy sees that $\frac21>\frac WW$, and chooses the smaller item.

Both of these solutions perform very badly here, and if you don't know what your real input is they could perform equally badly when given a real input.

Greedy algorithms won't help us much if we want to end up with an optimal solution, but there is a trick we can do to stop them being arbitrarily bad.

Imagine a our "Sort by Ratio" algorithm has just selected a subset of items and tries to select the next item but it is too large to fit into this subset. Before, we simply skipped it, but we have seen in our examples that this single item could be larger than our whole selected subset.

What if we corrected for this by, instead of skipping, checking whether this one item has a larger value then our current total and, if so, taking the single item instead of the whole selected subset.

This avoids some of the worst situations that can arise from using the "Sort by Ratio" algorithm, and actually means that the solution found by the algorithm will be **at least half** of the optimal solution.

What this shows us is that we can often apply a greedy algorithm to find fast, easy solutions that may not be optimal, although we can use a little bit of clever trickery to make them decent approximations.

