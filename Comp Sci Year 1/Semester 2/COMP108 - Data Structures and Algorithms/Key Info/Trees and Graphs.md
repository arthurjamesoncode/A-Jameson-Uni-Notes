## Key Definitions
### Graphs
A **graph** is a set of nodes and a set of edges which connect nodes together. If the graph is **directed** edges only connect one way, if the graph is **undirected** the edges connect both ways.

Formally:
- In a **directed graph** the edges are defined as ordered pairs.
- In an **undirected graph** the edges are defines as unordered pairs.

A **connected graph** is a graph which has at least one path between any two individual vertices.

The **degree of a vertex** in an undirected graph is the number of edges the vertex is incident with.

In a **directed graph** each vertex has an:
- **In-degree** - The number of edges which point to the vertex
- **Out-degree** - The number of edges which leave a vertex

A **simple graph** is a graph where there is at most 1 connection between vertices and each vertex cannot be connected to itself.

A **multigraph** is a graph which is not simple.

**Breadth first search** is an algorithm used to search a graph for a specific node by checking the nearest nodes first.

**Depth first search** is an algorithm used to search a graph for a specific node which continues down each path until it hits a dead-end/repeated node.
### Paths & Circuits
A **path** is an ordered list of edges which connect two nodes.

A **cycle** or **circuit** is a path which starts and ends on the same node.

A **simple circuit** is any circuit that travels at least 3 edges without repeating an edge or vertex (aside from the start). A simple circuit does not need to travel through every edge or vertex in the graph.

A **Euler circuit** is any circuit which visits every edge of a graph exactly once. Vertices are allowed to be repeated.

A **Hamiltonian circuit** is a circuit which containing every vertex of $G$ exactly once (aside from the start). It does not need to visit all edges.
### Representations of Graphs
An **adjacency matrix** is a matrix indicating which nodes of a graph are adjacent to each other (connected by an edge).

An **adjacency list** is a list of each node attached to a list of the nodes it is adjacent to.

An **incidence matrix** is a matrix indicating which nodes of a graph are incident with each edge.

An **incidence list** is a list of all edges attached to the list of nodes each edge is incident with.
### Trees
A **tree** is a undirected, connected graph with no cycles.

A **rooted tree** is a tree where every node descends from a single **root node**. This implies some kind of hierarchy or direction.

A **root** is the topmost vertex of a **rooted tree**.

A **child** of a node is any node directly below it in a rooted tree hierarchy.

A **parent** of a node is any node directly above it in a rooted tree hierarchy.

An **ancestor** of a node is any node higher than it in a rooted tree hierarchy.

A **descendant** of a node is any node lower than it in a rooted tree hierarchy.

A **leaf** is a vertex of a rooted tree which has no children.

An **internal vertex** is any non-leaf vertex in the tree.

The **degree of a vertex** in a **rooted tree** is the number of children it has.

The **degree of a rooted tree** is the maximum of the degrees of all vertices in the tree.

A **subtree** of a rooted tree is a smaller tree formed by taking any vertex of the tree as the root. In general a subtree is a smaller tree contained inside a larger tree.
### Tree Traversals
**Preorder traversal** - Visits the vertex first, then the left subtree, then the right subtree. (VLR)

**Inorder traversal** - Visits the left subtree first, then the vertex, then the right subtree. (LVR)

**Postorder traversal** - Visits the left subtree first, then the right subtree, then the vertex (LRV)

>Note that the left and right subtrees are always visited in order. This makes these easy to remember by just matching the prefix to where the vertex goes in the order.
### Binary Trees
A **binary tree** is a tree which has a degree of at most 2.

A **full binary tree** is a binary tree where every node has exactly 0 or 2 children.

A **binary search tree** is a binary tree where the left subtree of a vertex always contains data which is less than the vertexes data, while the right subtree always contains data which is greater than the vertexes data.
## Properties of Trees
A tree $(V, E)$ with $|V|$ vertices will always have $|E|=|V|-1$.

Any full traversal of a tree with $n$ nodes has $O(n)$ time complexity.

A binary search performed on a **binary search tree** will take $O(\log n)$ only if the binary search tree is **balanced**. A balanced tree is a tree in which the depth of 2 leaves differs by at most 1.
## Representing Graphs
### Adjacency
For a simple undirected graph with $n$ vertices the **adjacency matrix** $M$ is an $n\times n$ matrix. $M(i, j)$ denotes the $j^{th}$ element of the $i^{th}$ row, or the cell in the $i^{th}$ row and $j^{th}$ column. 

In an undirected graph, if vertex $i$ and vertex $j$ are adjacent then the $M(i,j)$ is a 1, otherwise it is a 0.

In a directed graph, $M(i, j)$ being 1 indicates that the vertex $i$ is connected to (points to) the vertex $j$.

>Importantly: **in a directed graph the rows point to the columns**.

Adjacency matrices can be represented by a 2D array.

Adjacency matrices have fast lookup times compared to adjacency lists, but always store $n^2$ entries for $n$ nodes in the graph. In a sparse graph adjacency matrices store much more than an adjacency list of the same graph.

If we represent a graph as an **adjacency list**, we store a list of adjacent vertices next to each vertex.
### Incidence
If a graph has $m$ edges and $n$ nodes then it's **incidence matrix** will be an $m\times n$ matrix.

$M(i,j)$ being 1 indicates that edge $i$ is incident with node $j$.

In an undirected graph, if $a$ and $b$ were the endpoints of $i$ then both $M(i,a)$ and $M(i,b)$ would be 1.

In a directed graph, if $i$ leads out from $a$ and into $b$ then $M(i,a)$ would be $1$ and $M(i, b)$ would be $-1$. In other words, there is a negative 1 for the destination, and a positive one for the origin.

>Importantly: **each row represents an edge, and each column represents a node**.

Incidence matrices should be used over adjacency matrices if the graph is **not-simple**.

Incidence matrices only ever store two 1 values per row, since an edge can only connect two nodes. This increases the amount of redundant space compared to an adjacency matrix, or adjacency list.

Incidence lists represent graphs by storing a list of all nodes incident with each edge alongside each edge.
## Circuit Properties
For a graph to contain a Euler Circuit, it must
- Either be **connected** (there is a path between every pair of nodes), or it is made up of one **connected subgraph** and number of nodes with **degree 0**.
- Every node must have an even degree
Showing the above conditions is both necessary and sufficient to show that a graph contains a Euler circuit.

If you want to review the proof you can [[Lecture 18 - Paths and Circuits in Graphs#Proof of Conditions for Euler Circuit|here]].

Determining is a graph contains a Hamiltonian circuit is an NP-hard problem.
## Graph Search Algorithms
Assume $n$ is the number of nodes in the graph.

**Breadth First Search:** $O(n)$
```
Input: graph, target

Q = Empty Queue
Choose a starting vertex which we will label start

Mark start as visited
Enqueue(Q, start)
while S is not empty do
	curr = Dequeue(Q)
	if curr == target then
		Stop and output "Found"
	endif
	
	for each unmarked neighbour w of v do
		mark w as visited
		Enqueue(S, w)
	endfor 
endwhile
```
If BFS is asked to output a path, the path it outputs will be optimal. It is also complete meaning that it will find a path if it exists.

**Depth first search:** $O(n)$
```
Input: graph, target

S = Empty Stack
Choose a starting vertex which we will label start

Mark start as visited
Push(S, start)
while S is not empty do
	curr = Pop(S)
	if curr == target then
		Stop and output "Found"
	endif
	
	for each unmarked neighbour w of v do
		mark w as visited
		Push(S, w)
	endfor 
endwhile
```
If DFS is asked to output a path, the path it outputs may not be optimal. As implemented it is complete.

>If you want more in-depth properties and visualisations of these algorithms look to [[Lecture 5 & Lecture 6 - BFS and DFS]] from the COMP111 module. 