## Paths and Circuits
In an undirected graph, a path from a vertex $u$ to a vertex $v$ is a sequence of edges which connect $u$ and $v$.

Formally we would define a **path** of length $n$ between $u$ and $v$ as 
$$
(e_1, e_2, ..., e_{n-1}, e_n)
$$
where
$$
\begin{split} 
e_1 &= \{u, x_1\} \\
e_i &= \{x_{i-1}, x_i\} \\
e_n &= \{x_{n-1}, v\}
\end{split}
$$
for all $1<i<n$.

In an undirected graph, the existence of a path from $u$ to $v$ implies the existence of a path from $v$ to $u$.

If $u$ and $v$ are the same ($u\equiv v$), then the path is called a **circuit** or **cycle**.

A **simple circuit** is any circuit that travels at least 3 edges and doesn't repeat any edge or vertex. Importantly, a simple circuit does not need to travel through every edge or vertex in the graph
## Euler Circuit
A Euler Circuit is a special type of circuit which visits each edge of a graph exactly once. Vertices however can be repeated.

>They are named after [Leonhard Euler](https://en.wikipedia.org/wiki/Leonhard_Euler) in honour of his solution to the [Seven Bridges of Königsberg](https://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg)problem. The history of this is gone into a little bit in the lecture, and I recommend you read about it, but I don't think we need to know the origins in detail

For example consider the graph below
![[has_euler_circuit.png]]

We can see that if we visit the nodes in the order given below to form a Euler circuit as every edge is travelled along exactly one.
$$
(a, c, b, d, e, c, d, a)
$$

Importantly, not every graph has a Euler circuit. Take the following example:
![[no_euler_circuit.png]]

This is the same as the graph above but with the $\{c,d\}$ edge removed. Removing that edge makes it impossible to form a Euler circuit from this graph.

So how can we determine if a graph has a Euler circuit or not?

Well first lets think about what needs to be true for a Euler circuit to exist at all:
- There must be a way to reach every edge from any node connected to an edge.
- The starting node must have another edge leading back to it.
- If you *enter* a node from an edge, there must be another untravelled edge from which you can leave.

The first condition is simple, a graph must either be **connected** (there is a path between every pair of nodes), or it is made up of one **connected subgraph** and number of nodes with **degree 0**.

>The second part of that condition is a bit pedantic. Feel free to understand this as only **connected** graphs can contain Euler circuits.

The next two are slightly harder but they imply that the degree of each vertex must be even. 

These two conditions together are actually sufficient to show that a graph contains a Euler circuit, and we can prove this.
### Proof of Conditions for Euler Circuit
**Claim:** A undirected, connected graph of size $n$ contains a Euler circuit if, and only if, every vertex has an even degree.

We will prove this by proving two smaller claims: 
- "Any graph that contains a Euler circuit only contains even-degree vertices"
- "Any connected graph that only contains even-degree vertices contains a Euler circuit"
We can prove both of these claims by assuming the first property, and then showing that the second property is a consequence of this.

We will start by proving that "Any graph that contains a Euler circuit only contains even-degree vertices and is connected".

Let $G$ be a connected, undirected graph containing a Euler circuit. We will start on a node of $G$, which we will call $a$, which acts as the start of our Euler circuit.

We leave $a$ at the start of the circuit, but we must return to it at the end or else it is not a circuit. 

Any node we visit in the meantime (including $a$) we must also leave meaning that the degree of each node is $2n$ where $n$ is the number of times we visit the node. Observe also that degree of $a$ is $2m+2=2(m+1)$ where $m$ is the number of times we visit $a$ not including starting or ending there. 

So every node either has a degree of $2n$ or $2(m+1)$. Since $n$, and $m+1$ are integers, we know that the degree of every node in a graph with a Euler circuit must be even.

Next we will show that "Any connected graph that only contains even-degree vertices contains a Euler circuit".

Note that, since every node has an even degree, it is not possible to get stuck at any node other than the first node. 

To show this let $2k$ be the number of untravelled edges incident with a node which is not the starting node where $k\in\mathbb Z$. 

If we travel to the node, this number decreases by 1 leaving us with $2k-1$ untravelled edges while we are on this node. We then must also leave this node and so we have $2k-2=2(k-1)$ untravelled paths remaining.

This means that we can go to and leave any non-starting node exactly $k$ times, and therefore cannot get stuck on it.

In the case of the start node we can get stuck. Let $2k$ be the number of untravelled edges from the start node. When we leave it in the beginning we are left with $2k-1$ paths. This means that eventually the start node will be left with 1 untravelled edge while we are not on the node, and so when we eventually travel that edge back to the start we will be stuck.

Now that we know where we can get, we can trace an arbitrary circuit around this graph. There are a 2 cases for this circuit:
- It travels every edge (is already a Euler circuit)
- It does not travel every edge.

In the first case there is already a Euler circuit.

In the second case, we know that at least one of the vertices travelled through has an even number of **untravelled edges**. If we remove the travelled circuit (only keeping untravelled edges and vertices connected to them), we are left with a smaller graph that still only has even-degree vertices.

Since the graph is connected, at least one of these vertices on the sub-graph will be shared with the completed circuit.

Acting on this subgraph we can draw another circuit. For the same reasons above, we can only get stuck on our new starting node.

What this means is that if we go back to our starting node on the main graph and follow the path we defined up to the new start we chose, we can then extend our circuit by adding in the new circuit we drew starting from this point.

Again there are two cases for this extended circuit:
- It travels every edge
- It does not travel every edge

If it travels every edge then we have found a Euler circuit, but if it does not travel every edge we can simply repeat the process outlined here to extend the circuit until it does. 

This proves that any connected undirected graph only containing even-degree vertices will contain a Euler circuit. 

>I haven't included any images in this proof, which I find necessary to keep it general, but I think some graphical explanation can help understand this. 
>
>I recommend going to the lecture video on canvas to see Prudence explain this with some example graphs.
## Hamiltonian Circuit
Another type of circuit we will be briefly touching on are **Hamiltonian circuits**. 

Let $G$ be an arbitrary undirected graph.

A Hamiltonian circuit is a circuit containing every vertex of $G$ exactly once. It may not or may not visit all edges of $G$.

The problem of determining whether a graph contains a Hamiltonian circuit is much harder than the Euler circuits.

>The problem of determining if a graph contains a Hamiltonian circuit is [NP-hard](https://en.wikipedia.org/wiki/NP-hardness). 
>
>The only algorithms so far defined to do this all take exponential time, but as of yet it has not been proven that a polynomial time solution is impossible.
>
>If you ever solve this problem, you will win a $1,000,000 prize from the [Clay Mathematics Institute](https://www.claymath.org/millennium-problems/), and probably awarded with the Turing Award.
## Searching Algorithms
The rest of this lecture is spent going over 2 basic searching algorithms we can use with graphs:
- Breadth First Search (BFS)
- Depth First Search (DFS)

These algorithms have been covered before in COMP111, so for properties and visualisations of these algorithms you can look to [[Lecture 5 & Lecture 6 - BFS and DFS]] from COMP111.

Here we will simply be covering ways to implement these in pseudocode using some data structures that we have looked at.
### DFS
Lets start with DFS. What data structure could we use to implement this.

Well DFS evaluates the paths expanded most recently before any other paths. This suggests to us that we use a last in first out data structure, or a stack.

Knowing this we can start to write out our pseudocode
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
### BFS
Now lets look at BFS. What data structure could we use to implement this.

Well BFS evaluates the paths expanded first before any other paths. This suggests to us that we use a first in first out data structure, or a queue.

Knowing this we can start to write out our pseudocode
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
