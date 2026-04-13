## Graph Theory & Graphs
Graph theory was introduced in the 18th century and studies the data structure of a **graph**. 

Graphs are a generalisation of trees made up of a set of nodes (or vertices) and a set of edges which indicate a connection between 2 nodes.

The above is the only requirement for something to be a graph. As a result, all trees are graphs but not all graphs are trees. 

There are 2 types of graphs:
- **Directed graphs** - Edges indicate a one way connection
- **Undirected graphs** - Edges indicate a two way connection

>Note that two way connections can still exist in a directed graph, it just requires that two edges instead of 1.

When we define an **undirected graph** $G=(V, E)$, $V$ is a set of vertices and $E$ is a set of **unordered** pairs. 

For example a graph could be defined as $G=(V,E)$ where
$$
\begin{split}
V&=\{a, b, c, d, e, f\}  \\ 
E&=
\{
\{a, b\},\{a,c\},\{a,d\},\\
&\;\;\;\;\;\;\;
\{a,e\},\{b,c\},\{b,d\}, \\
&\;\;\;\;\;\;\;
\{b,f\},\{d,e\},\{e,f\}\}
\end{split}
$$

We could then represent this graphically as
![[undirected_graph_example.png]]

>Note that since the pairs are unordered $\{a, b\}=\{b, a\}$. We use the curly brackets to denote this as the edge is actually defined by the set of 2 edges that it connects, and curly brackets indicate a set.

When we define a **directed graph** $G=(V, E)$, $V$ is a set of vertices and $E$ is a set of **ordered** pairs.

For example a graph could be defined as $G=(V,E)$ where
$$
\begin{split}
V&=\{a, b, c, d, e, f\}  \\ 
E&=
\{
(a, b),(a,c),(a,d),\\
&\;\;\;\;\;\;\;
(a,e),(b,c),(d,b), \\
&\;\;\;\;\;\;\;
(d,e),(f,b),(e,f)\}
\end{split}
$$

We could then represent this graphically as
![[undirected_graph_example.png]]
### Modelling With Graphs
Graphs can be used to model any set of interconnected objects.

In computer science we use graphs to model a number of different things:
- Computer Networks
- State Spaces of Games
- Resource Conflicts
- Precedence of Processes

Other subjects also use graphs to model various things:
- Evolutionary Relationships
- Food Maps
- Structure of Molecules
- Rail/Bus Maps
### Undirected Graphs
Undirected graphs are graphs in which there in which the set of edges is defined as a set of **unordered pairs**.

There are 2 kinds of undirected graph:
- A simple graph - There is at most 1 edge between vertices, and vertices can be connected to themselves.
- A multigraph - There can be more than one edge between two vertices and vertices can be connected to themselves.

We say that vertices which are connected to each other are **adjacent** and are **neighbours** of each other.

For example take the following graph
![[undirected_terms.png]]

In this graph, $e$ is the edge $\{u, v\}$. Since $e$ exists in this graph we can say that $u$ and $v$ are adjacent, and therefore neighbours of each other.

We can also say that $u$ and $v$ are the **endpoints** of $e$ or that $e$ is **incident** with $u$ and $v$, or that $e$ **connects** $u$ and $v$. All of these terms are mean the same thing in relation to an edge and the nodes it connects.

In an undirected graph the **degree of a vertex** is the number of edges incident with $e$. The only thing to be careful of is that a self loop counts twice.

In the graph above you could say that $u$ has a degree of $3$ while $x$ has a degree of $1$.

The **degree of a graph** is the maximum of the degrees of all it's vertices.
### Directed Graph
A directed graph is a graph in which the set of edges is given by a set of **ordered pairs**.

Consider the directed graph $G=(V,E)$ depicted below.
![[directed_graph_example.png]]

In directed graphs we say that a node $x$ is connected to another node $y$ if there exists an edge $(x,y)$. So in the given example, we can say that $a$ is connected to $b$. 

Note that we can not say that $b$ is connected to $a$ as $(b,a)$ doesn't exist.

We call the number of edges leading to a vertex $v$ the **in-degree** of $v$. We call the number of edges leading away from a vertex $v$ the **out-degree** of $v$.

So in the given example, we could say that $a$ has an **in-degree** of $0$ but an out degree of $4$ while $b$ has an **in-degree** of $3$ but an out degree of $1$.

Let's look at the in-degree an out degree of all the nodes from the example

| Vertex  | In-Degree | Out-Degree |
| ------- | --------- | ---------- |
| $a$     | 0         | 4          |
| $b$     | 3         | 1          |
| $c$     | 2         | 0          |
| $d$     | 1         | 2          |
| $e$     | 2         | 1          |
| $f$     | 1         | 1          |
| **Sum** | 9         | 9          |
Notice that the in and out degrees sum to the same value. 

This will always happen. This is because if we increase the total **out-degree** by adding any outgoing edge to a node, that edge will need to point somewhere, therefore also increasing our total **in-degree** regardless of where it ends up pointing.
### Proofs Using Graphs
When hoping to prove something about a group of related objects, we can make our lives easier by considering a corresponding graph.

Consider the following Scenario and claim
- **Scenario:** In a room full of people where some people shake hands with others, people will either have shook hands with an odd number of people and some an even number of people.
- **Claim:** The number of people who have shook the hands of an odd number of people must be even.

If we understand the people in this room as nodes, and the shook hands relation as an edge that connects 2 people we can view this as a question about graphs.

Our room is now a **simple undirected graph**, since there is no direction associated with a handshake, shaking hands with someone multiple times doesn't add extra edges, and you can't (really) shake your own hand.

Our claim is now "In an undirected graph, the number of vertices with an odd degree must be even". 

Now that we have a good way to model this, we can prove this by induction on the number of nodes $n$ and number of edges $e$ in the graph.

**Base Case:** $n+e=1$
In this case we have only one node, which has a degree of 0. This means we have 1 node with an even degree and 0 nodes with an odd degree. 

Therefore our claim is proved true for our base case.

**Inductive Step:** Assume our claim is true for $n+e=k$
When $n=k$ we know that the number of odd-degree vertices must be of the form $2m$ where $m\in\mathbb Z$.

To increase the value of $n+e$ by 1 we can either add a new node, which is disconnected from any existing node or add an edge between two existing nodes. 

If we add a new disconnected node, the degree of any node in our current graph does not change. This means that the number of odd-degree vertices doesn't change and therefore remains odd meaning that the claim remains true for $n+e=k+1$ in this case.

If we add an edge between two existing nodes $a$ and $b$, the only degrees which change are the degree of $a$ and degree of $b$, which both increase by 1. These nodes can either be:
- Both even-degree
- Both odd-degree
- One even-degree, one odd-degree

If both were even-degree before adding the edge, then both will be odd after adding the edge. Therefore the number of odd-degree vertices increases to $2m+2=2(m+1)$. Since $m+1$ is an integer, this number is also even and the claim holds true for $n+e=k+1$ in this case.

If only one was even-degree before adding the edge, then 1 will become odd-degree and 1 will become even-degree meaning the number of odd-degree matrices doesn't change and the claim holds true for $n+e=k+1$ in this case.

If neither were even-degree before adding the edge, then both will become even after adding the edge. This means that the number of odd-degree vertices decreases to $2m-2=2(m-1)$. Since $(m-1)$ is an integer, $2(m-1)$ is even and the claim holds true for $n+e=k+1$ in this case.

Since the claim holds true in this exhaustive list of cases, we know that as long as the claim holds true for $n+e=k$ it will also hold true for $n+e=k+1$.

**Conclusion:**
As we have shown that this holds true for our base case of $n+e=1$ and also shown that it holds for our inductive step, we have shown that the claim holds true for an undirected graph of any size.
## Representing Graphs
So far, we have seen how to represent graphs graphically and as a collection of 2 sets. 

These methods of representing graphs work, and are perfectly accurate, but aren't necessarily the easiest for a computer to understand.

To get around this we use four main methods of representing graphs:
- Adjacency Matrix
- Adjacency List
- Incidence Matrix
- Incidence List

Adjacency matrices and adjacency lists represent matrices by showing which vertices are adjacent to each other, while incidence matrices and incidence lists represent matrices by shown which edges are incident with which vertices.

Adjacency matrices and lists are usually more convenient to work with when we have **simple graph** (at most 1 edge between 2 nodes), but if you allow for more edges between nodes then we need to use an incidence matrix or incidence list, as now edges are defined by more than just which nodes they connect.

We will go over each of these in detail now, along with how their use differs for directed and undirected graphs.
### Adjacency Matrix
For a simple undirected graph with $n$ vertices the adjacency matrix $M$ is an $n\times n$ matrix. $M(i, j)$ denotes the $j^{th}$ element of the $i^{th}$ row, or the cell in the $i^{th}$ row and $j^{th}$ column. 

>Matrices have been covered before in various modules, I am assuming familiarity with them, although you don't need much to understand the content her. If you want more information you can visit [[Lecture 21 - Determinants & Intro to Spectral Theory#Matrices|here]]. 

In an undirected graph, if vertex $i$ and vertex $j$ are adjacent then the $M(i,j)$ is a 1, otherwise it is a 0.

In a directed graph, $M(i, j)$ being 1 indicates that the vertex $i$ is connected to (points to) the vertex $j$.

Note that if a graph is undirected then the adjacency matrix will always be symmetrical along the top-left diagonal.

Below you can see an example **undirected graph** 
![[adjacency_undir_graph.png]]

Which corresponds to the following adjacency matrix:
![[adjacency_undir_matrix.png]]
Note that, since this represents an undirected graph, it is symmetrical along the top-left diagonal.

If instead we look at an example **directed graph**:
![[adjacency_digraph.png]]

We can see that this corresponds to the following adjacency matrix:
![[adjacency_dir_matrix.png]]
Note here that $a$ points to $b$, but $b$ doesn't point to $a$, and so $M(a,b)$ is 1, but $M(b,a)$ is 0.

Adjacency matrices are very strong when you need to be able to quickly look up if two nodes, $i$ and $j$, are adjacent as you can retrieve the entry at $M(i,j)$ in constant time ($O(1)$). This is much faster than the process to determine if two nodes are adjacent when using an adjacency list.

Their main problem is the space required to store them. Adjacency matrices always store exactly $n^2$ entries, where $n$ is the number of nodes in the graph. In a **sparse graph** (a graph with very few connections between nodes) the adjacency matrix still stores $n^2$ entries. Much more than an adjacency list of the same graph.

Practically, adjacency matrices can be represented by nested arrays.
### Adjacency List
If we represent a graph as an adjacency list, we store a list of adjacent vertices next to each vertex.

If we look at the example undirected graph below:
![[adjacency_undir_graph.png]]

We can see that it corresponds to the following adjacency list
![[adjacency_undir_list.png]]

In an directed graph, each vertex's list only includes the nodes that it points to.

If we look at the following directed graph:
![[adjacency_digraph.png]]

We can see that it corresponds to the following adjacency list.
![[adjacency_dir_list.png]]

Adjacency lists are particularly strong at **sparse graphs**, but not quite as good at **dense** ones. This is because they need to store much less than an adjacency matrix of the same graph.

The main disadvantage of using an adjacency list over an adjacency matrix is the time it takes to determine if two nodes are adjacent. The only option for checking with an adjacency matrix is to perform a search on the list of one of the nodes. If unsorted this would be an $O(n)$ operation, but could be $O(\log n)$ operation if sorted. Both of these are still much slower than an adjacency matrix.

One way to implement this would be to store a **map** (for example a `hashMap` in Java) which maps each node to an array (or the head of a linked list) which stores all of the adjacent nodes.
### Incidence Matrix
Incidence matrices are very similar to adjacency matrices, but instead track which edges are incident with which nodes.

If a graph has $m$ edges and $n$ nodes then it's incidence matrix will be an $m\times n$ matrix.

$M(i,j)$ being 1 indicates that edge $i$ is incident with node $j$.

In an undirected graph, if $a$ and $b$ were the endpoints of $i$ then both $M(i,a)$ and $M(i,b)$ would be 1.

Take, for example, the following undirected graph with it's edges labelled:
![[incidence_undir_graph.png]]

We can see that this corresponds to the following incidence matrix:
![[incidence_undir_matrix.png]]
Notice that each row has exactly two 1s in it, since each edge connects two nodes.

In a directed graph, if $i$ leads out from $a$ and into $b$ then $M(i,a)$ would be $-1$ and $M(i, b)$ would be $1$.

Take, for example, the following directed graph with it's edges labelled:
![[incidence_digraph.png]]

We can see that this corresponds to the following incidence matrix:
![[incidence_digraph_matrix.png]]
Notice now that every row has exactly one 1 and one -1, since each edges leads out of 1 node and into another.

Incidence matrices may need to be used over adjacency matrices if the graph is **not simple** (allows more than 1 edge between two nodes).

Incidence matrices have the similar advantages and disadvantages over incidence lists as adjacency matrices have over adjacency lists. However the advantages are less pronounced and the disadvantages are more pronounced as every edge only needs to store 2 nodes, regardless of the size of the graph.
### Incidence List
Incidence lists represent graphs by storing a list of all nodes incident with each edge alongside each edge.

In an undirected graph, the nodes incident with the list are stored in any order.

Take, for example, the following undirected graph with it's edges labelled:
![[incidence_undir_graph.png]]

We can see that this corresponds to the following incidence list:
![[incidence_undir_list.png]]

In a directed graph, the first node stored with each edge is the node it leads away from while the second is the node it leads to.

Take, for example, the following directed graph with it's edges labelled:
![[incidence_digraph.png]]

We can see that this corresponds to the following incidence list:
![[incidence_dir_list.png]]