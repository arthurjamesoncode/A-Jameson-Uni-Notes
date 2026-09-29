## Key Definitions
A **greedy algorithm** is an algorithm which, at each step of the algorithm, makes the decision which moves the current state closest to the goal state based on some metric. This usually involves selecting something with the largest/smallest value depending on the goals of the algorithm.

The **knapsack problem** is "Given a knapsack that can carry a limited weight $W$ and a set of items $\{(w,v)\}$ which have a weight $w$ and value $v$, choose the subset of items with the largest value which you can fit into the knapsack"

A **spanning tree** of a undirected connected graph $G$ is a tree which contains all the vertices of $G$ and a subset of the edges of $G$.

A **minimum spanning tree** (MST) of $G$ is a spanning tree of $G$ which has the minimum total cost of edges possible. We say "a" MST because multiple distinct MSTs may exist for the same graph if some edges share weights.

**Kruskal's algorithm** is a greedy algorithm which, given a connected undirected graph $G$, provides a minimum spanning tree of $G$.

The **single-source shortest paths** of a vertex $a$ in an undirected graph $G$ is a spanning tree of $G$ containing the shortest paths from $a$ to every other vertex. There may be multiple distinct sets of single-source-shortest paths for any vertex if some vertex has two identical (cost wise) ways to it from $a$.

**Dijkstra's algorithm** is a greedy algorithm which, when given a connected undirected graph $G$ and a starting vertex $a$, provides a set of single-source shortest paths from $a$.
## Algorithms
### Greedy algorithms:
- Easy to implement
- Solutions are not optimal but (usually) decent
- Solutions are (usually) found quite quickly
### Knapsack Problem with Greedy Algorithms:
- Multiple ways of implementing - Sort by value, sort by value/weight etc.
- Can be **arbitrarily bad**
- Can correct for the arbitrarily bad nature to ensure the solution is at least half of the optimal solution (view [[Lecture 19 - Greedy Algorithms & The Knapsack Problem#Greedy Isn't Always Great|here]] for the method)
- $O(n)$ on a sorted list of items
- $O(n\log n)$ on an unsorted list of items
- (Non greedy knapsack approaches are not covered)
### Kruskal's Algorithm
**Pseudocode:**
```
//Given a undirected connected graph G=(V, E)

T = Empty Set
E' = E
Sort E' from smallest weight to largest weight
CurrTrees = Empty Map

while E' is not empty do
	e = first/smallest item of E'
	{a, b} = The endpoints of e 
	//a and b are variables which would hold the unique label for the vertices
	
	remove e from E'
	
	if CurrTrees contains both a and b then
		currA = CurrTrees.get(a)
		currB = CurrTrees.get(b)
		if (currA == currB) then //a cycle would be formed if we add e
			continue to next iteration 
			//this skips the rest of the execution 
		endif
		
		for each element x of currB do
			currA.add(x)
			CurrTrees.set(x, currA)
		endfor					
	endif
	
	T.add(e)
	
	if CurrTrees contains neither a or b then
		newTree = Empty Set
		newTree.add(a)
		newTree.add(b)
		CurrTrees.set(a, newTree)
		CurrTrees.set(b, newTree)
		continue to next iteration
	endif
	
	if CurrTrees contains a but not b then
		curr = CurrTrees.get(a)
		curr.add(b)
		CurrTrees.set(b, curr)
		continue to next iteration
	endif
	
	if CurrTrees contains b but not a then
		curr = CurrTrees.get(a)
		curr.add(b)
		CurrTrees.set(b, curr)
		continue to next iteration
	endif 
endwhile
```

**Properties:**
- Optimal - will always find an MST
- Can find multiple MSTs for some graphs with duplicate edge weights depending on how ties are broken in the sorting of edges
- $O(nm)$ if given $n$ vertices and $m$ edges
## Dijkstra's
**Pseudocode:**
```
//Given a graph G=(V, E) and a source vertex s

for all vertice v in graph do
	v.distance = infinty
	v.predecessor = null
endfor

s.distance = 0
s.predecessor = null
unvisited = V

while unvisited is not empty do
	curr = node with smallest distance in unvisited
	unvisited.remove(curr)
	for every neighbour v of curr in unvisited do
		if (curr.distance + {curr, v}.weight) < v.distance then
			 v.distance = curr.distance + {curr, v}.weight
			 v.predecessor = curr
		endif
	endfor
endwhile
```
>I have skipped over implementation details for choosing the node with the smallest distance. In practice, you would usually do this by storing available nodes in a [priority queue](https://en.wikipedia.org/wiki/Priority_queue).

**Properties:**
- Optimal - Always produces a valid set of single source shortest paths
- Can produce different paths (specific nodes could have different predecessors) if two paths from the start to the same node have the same weight
- Time complexity $O(n^2)$

Note that, when tracing the algorithm on paper, the `distance` of each node is updated the each time a possible predecessor is travelled to, meaning that an edge with it as one of its endpoints is selected.

This is important to know since some questions will be of the form "which of these sets of changes could this algorithm produce" are common.




