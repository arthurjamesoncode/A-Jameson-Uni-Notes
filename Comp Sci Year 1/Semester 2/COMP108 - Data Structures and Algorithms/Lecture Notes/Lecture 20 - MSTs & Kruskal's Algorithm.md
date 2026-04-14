## Minimum Spanning Tree (MST)
Given an undirected connected graph $G$, a **spanning tree** of $G$ is a tree which contains all the vertices in $G$.

Now if this graph has **weights** associated with each edge, the **minimum spanning tree** is the spanning tree with the minimum weight.

For example below you can see a small, undirected, connected graph and some spanning trees. Which of these trees is the minimum spanning tree?

>Reminder that a tree is a connected, undirected graph with no cycles. You can refresh yourself [[Lecture 16 - Trees|here]].

![[spanning_trees.png]]

Well first, lets sum the weights and compare them:
- 1st: $2 + 2 + 1 = 5$
- 2nd: $3+3+1=7$
- 3rd: $2+2+3=7$

We can see that the first one is the smallest of these, but that is slightly different question to if it is the MST or not.

We actually know that the first is the MST because it takes the 3 smallest edges possible, and it takes exactly 3 edges to span a 4 node graph. This means no smaller tree is possible making it the MST.

We are studying this in relation to **greedy algorithms** as it is a good example of when a greedy algorithm is actually optimal.
## Kruskal's Algorithm
Kruskal's algorithm is a greedy approach to finding the MST of a connected, undirected graph.

The basic idea is simple:
- List your edges sorted by weight
- Repeatedly take the minimum weighted edge, as long as it doesn't form a cycle (if so take the next minimum)
- Continue until all nodes are part of the same tree.

Unlike the previous examples from [[Lecture 19 - Greedy Algorithms & The Knapsack Problem|last lecture]], this approach is actually optimal. We will quickly prove this.
### Proof of Optimality
Let $T$ be a tree created by Kruskal's algorithm applied to a graph $G$ with $n$ nodes.

Let's assume, for the sake of contradiction, $T$ is not a minimum spanning tree. This would mean that there exists a tree $T_{opt}$ such that $T_{opt}$ is a MST of $G$ and $T_{opt}\neq T$. 

Let $e$ be the first edge chosen by Kruskal's algorithm, that is not in $T_{opt}$.

Observe that adding $e$ to $T_{opt}$ creates a cycle.

Since $e$ is part of $T$ but not part of $T_{opt}$ that implies there is another edge $f$ which is not in $T$ but is in the cycle created when you add $e$ to $T_{opt}$. If we remove $f$ the cycle will be broken, and we will be left with a different spanning tree $T_{new}$.

Since Kruskal's algorithm selected $e$ before $f$, it must be the case that $weight(e)\leq weight(f)$. Since the only difference between $T_{opt}$ and $T_{new}$ is that $T_{opt}$ has edge $f$ while $T_{new}$ has edge $e$ we know that $totalWeight(T_{opt})\geq totalWeight(T_{new})$.

This is a contradiction as $T_{opt}$ is defined as a MST of $G$, but we have shown that $T_{new}$ can have a smaller weight than $T_{opt}$.

Therefore it is not possible for Kruskal's algorithm to produce any tree which is not the MST of $G$.
## Example
Let's try to run through an execution of Kruskal's algorithm on the graph below.

![[mst_exercise.png]]

First lets order all of our edges into table sorted by their weight.

| Edge       | Weight |
| ---------- | ------ |
| $\{b, f\}$ | 3      |
| $\{c, f\}$ | 3      |
| $\{b, c\}$ | 4      |
| $\{a, b\}$ | 4      |
| $\{e, f\}$ | 4      |
| $\{e, d\}$ | 5      |
| $\{a, f\}$ | 6      |
| $\{c, d\}$ | 6      |
| $\{b, e\}$ | 10     |
| $\{c, e\}$ | 10     |

>Note that, when two edges are even weight and both don't create a cycle, Kruskal's algorithm doesn't care about which edge it chooses. For the sake of this example we will simply run down the table in order.

Kruskal's algorithm then does the following:
- Chooses $\{b, f\}$
- Choose $\{c, f\}$
- Skip $\{b, c\}$ as it would create a cycle
- Choose $\{a, b\}$
- Choose $\{e, f\}$
- Choose $\{e, d\}$
- 5 edges have been chosen, meaning that this completes an MST and the algorithm stops.
## Pseudocode Implementation
Have a think about how we could implement this in an actual piece of code.

Firstly, we could store all of the edges from our graph in an array and sort them and then go through and choose them if they don't create a cycle.

This does still leave a big implementation question: How do we determine if adding an edge creates a cycle?

Well lets consider what possible cases exist when we add a new edge $\{u, v\}$ while building our MST:
- Neither $u$ nor $v$ belong to a chosen **partial tree**.
- Either $u$ or $v$ belong to a **partial tree** that has been chosen already, but not both.
- $u$ and $v$ belong to separate **partial trees**.
- Both $u$ and $v$ belong to the same **partial tree** that has been chosen already.

We can see each case means for forming cycles:
- In the first case, no cycle will be formed and both nodes will form the start of a new partial tree.
- In the second case, no cycle will be formed and the node that isn't part of any tree will be added to the partial tree that contains the other node.
- In the third case, no cycle will be formed and both partial trees will be connected.
- In the last case, a cycle will be formed as, by definition of tree, $u$ and $v$ are already connected by some other path.

Breaking this down like this, it becomes a lot easier to see if a cycle is formed just by keeping track of these partial trees.

If we label each vertex with a colour, an id, or object reference which corresponds to a partial tree, we can keep track of which partial trees. 

There are a number of ways to implement this, if you were asked to write this as a program I would recommend using a hash map which maps each vertex to a set. The set would be all of the vertices in the current partial tree. If the vertex in question has not been added to a partial tree yet, then it would not be in the hash map.

>These implementation details are a little unnecessary for this module, but are good to think about none the less. 
>
>I don't think hash maps have been covered in this course, they are mentioned in [[Lecture 14 - Collections]] of the comp122 module, but they are simply a way look something up using a (possibly) non-numeric key in constant time.

You can see the full pseudocode for this below
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
		currB = currTrees.get(b)
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
## Time Complexity Analysis
Imagine we start with a sorted list of edges.

In this case, we can go through the edges linearly, meaning that in the worst case (when the greatest edge is part of the MST), that we complete $n$ operations. This gives the algorithm a time complexity of $O(n)$.

If we start with an unsorted list of edges, obviously we need to first sort them. Since the best sorting algorithms take $O(n\log n)$ time to complete, and $n\log n$ dominates $n$, the time complexity in this case would be $O(n\log n)$.
