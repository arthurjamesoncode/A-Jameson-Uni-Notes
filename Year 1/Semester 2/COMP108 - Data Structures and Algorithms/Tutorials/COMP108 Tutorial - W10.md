## Question 1
Consider the following graph $G$. The label of an edge is the cost (weight) of the edge.
![[greedy_tut_graph_1.png]]

**Question:** Give a table listing all the edges in ascending order of the costs.

**Answer:**

| Edge       | Cost |
| ---------- | ---- |
| $\{a, b\}$ | 1    |
| $\{a, f\}$ | 1    |
| $\{b, f\}$ | 1    |
| $\{f, e\}$ | 1    |
| $\{c, d\}$ | 2    |
| $\{a, e\}$ | 3    |
| $\{b, c\}$ | 5    |
| $\{c, f\}$ | 6    |
| $\{d, e\}$ | 6    |
| $\{b, e\}$ | 7    |
| $\{d, f\}$ | 8    |
**Question:** Using Kruskal’s algorithm, draw a minimum spanning tree (MST) of the graph. Write down the order of the edges selected. Break ties by using your table in (a). If there is more than one solution, you only need to give one of the solutions.

**Answer:**
![[question1.drawio.png]]

**Order of Edges Selected:** $\{a, b\}$, $\{a, f\}$, $\{f, e\}$, $\{c, d\}$, $\{b, c\}$
## Question 2
Consider the following graph $G$. The label of an edge is the cost (weight) of the edge.
![[greedy_tut_graph_2.png]]

**Question:** Using Dijkstra’s algorithm, find the shortest paths from the vertex a to all the other vertices. You need to draw the edges chosen and show the changes of the labels of the vertices step by step and also the order of selection of vertices/edges. If there is more than one solution, you only need to give one of the solutions.

**Answer:** Note that I only replaced a distance if it was lower than the current, meaning that equal distances were not changed. Unselected edges have been removed from the graph.

![[question2.drawio.png.png]]

**Order of Edges Selected:** $\{a, b\}$, $\{a, f\}$, $\{f, e\}$, $\{b, c\}$, $\{e, d\}$
## Question 3
**Question:** Describe or write pseudo code for a divide-and-conquer algorithm to find the product of the numbers in an array $A[ ]$ with $n$ integers $A[1]..A[n]$.

**Answer:** 
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

`div` is used to indicate integer division (discarding remainder).