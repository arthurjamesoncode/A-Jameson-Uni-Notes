## Single-Source Shortest Paths
Consider a connected graph $G$ with weighted edges. Given a particular **source** node, how can we find the shortest (smallest total weight) paths from the source node to all other vertices?

[[Lecture 20 - MSTs & Kruskal's Algorithm|Last lecture]], we had a look at **spanning trees**. Each collection of **single-source shortest paths** is a spanning tree of $G$. 

It is important to not confuse these with **minimum spanning trees** as, while similar, MSTs are a **global property** of the graph while **single-source shortest paths** is a local property of a given node.

You can see below some example shortest paths using the first example from last lecture.

![[single-source-vs-mst.png]]

This problem has a lot of algorithms designed to solve it. One of them, the one we will be looking at today, is **Dijkstra's algorithm**.
## Dijkstra's Algorithm
Dijkstra's algorithm is a greedy approach to solve this problem that assumes the weight of each edge is non-negative.

The basic idea is simple:
- Start from the source
- Keep track of visited vertices, and their distance from the source
- At each step choose the next available non-visited vertex with the shortest path from the source
- Continue until the whole graph has been visited

>This algorithm is just [[Lecture 8 - Uniform Cost Search and Heuristic Searches#Uniform Cost Search|uniform cost search]] (which was covered in COMP111), except, instead of trying to find the shortest path to a goal, it continues until it has found the shortest path to every node.
>
>Because the algorithms are so similar, I have gone into a little less detail with the example than I could have. If you are getting lost, I recommend going back to the COMP111 notes.

For example consider the graph below
![[djikstra_initial.png]]

You can see that each vertex has been labelled with a tuple. The first element of the tuple represents the distance of the current shortest path from $a$ (initially set to $\infty$ which is a placeholder to show that it has not been reached yet) and the second element shows the vertex immediately before it on that path.

Every round, a vertex is chosen (initially the source), and the neighbours labels are updated and they are made available to move to, as you can see below. From now on I will call this process **expanding** the vertex/node.

![[dijkstas_1.png]]

Then, from all available vertices, we choose the one with the shortest path from our source and expand it. If a neighbour of the vertex we choose to expand is already labelled with a distance, we only update the label if the new distance is smaller.

So here we would expand vertex $b$ since it has the smallest current distance, which causes us to label vertex $h$ as you can see below

![[dijkstras_2.png]]

Now we choose one of the available vertices $c$, $d$, and $h$ to expand. Since $c$ has the smallest current weight, we expand $c$.

Note that now, when we update the labels of the neighbours of $c$, the weight of travelling to $d$ and $e$ is less if we travel through $c$. Because of this, we must update their labels accordingly.

![[dijkstras_3.png]]

This should be enough for you to understand the algorithm. I recommend trying to complete it in your head.

The full solution is shown below:
![[dijkstras_final.png]]
## Pseudocode Implementation
To implement this in pseudocode we first need a bit of notation:
- We use `node.distance` to represent the current shortest path to the given node.
- We use `node.predecessor` to represent the immediate predecessor of the given node on the current shortest path
- We use `{a, b}.weight` to represent the weight of the given edge between vertices `a` and `b`.

With this we can implement our pseudocode
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

>Note that I have skipped over implementation details for choosing the node with the smallest distance. In practice, you would usually do this by storing available nodes in a [priority queue](https://en.wikipedia.org/wiki/Priority_queue).
## Time Complexity Analysis
For convenience, we will call `V.size` $n$ and the **degree** of the graph $m$.

Our program is made of three loops. The first loop runs exactly $n$ times and contains no other loops.

The outer loop executes exactly $n$ times as every iteration 1 element from `V` is removed from `unvisited`. The inner loop executes $m$ times every time in the worst case (every node having the same degree).

This gives us a time complexity of $O(n+mn)$ which simplifies to $O(mn)$. So can we stop there?

Well no, because we can actually compare how big $m$ and $n$ are. If a graph had every possible connection then every node would have a degree of $n-1$. This is the maximum possible degree of the graph (or maximum value of $m$).

Since $n-1<n$, we know that $n>m$, and therefore we can simplify our big-O value to $O(n^2)$.
