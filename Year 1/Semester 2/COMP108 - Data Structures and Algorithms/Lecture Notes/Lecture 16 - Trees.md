## Trees
A tree $T=(V, E)$ is a data structure which consists of a set of vertices $V$ and a set of edges $E$ such that for any pair of vertices $a,b\in V$ there is **exactly one path** between $a$ and $b$.

>We can use the terms vertex and node interchangeably when referring to trees.

You may notice that a [[Lecture 10 - Linked Lists|linked list]] actually fits this definition, making linked lists a special kind of **tree**. A tree with **no branches**.

You can see some examples of what a tree is and isn't below.

![[tree-examples.png]]

There are a number of equivalent statements to "There is exactly one path between any two vertices in T" and we will go through some now. Having a look at these can give us an idea of some of the properties of trees in general, and the consequences of these properties.

**"$T$ is connected and acyclic."**
	Connected means that there is at least one path between any two vertices in $T$. Acyclic means there are no cycles, which means there is at most 1 path between any two vertices in $T$. Together these statements mean that there is exactly 1 path between any two elements.
**"$T$ is connected and a removal of one edge disconnects $T$."**
	Again connected means that there is at least one path between each pair of vertices. If there were more than path between any two vertices, then removal of a single edge wouldn't be **guaranteed** to disconnect $T$, which makes this statement equivalent to the one before.
**"$T$ is acyclic and adding one edge creates a cycle."**
	If adding a single edge will create a cycle, it means that there must already be **one** path between every vertex in $T$ ($T$ is connected).
**"T is connected and $|E| = |V| - 1$"**
	It can be proven by strong induction that if $T$ is connected and acyclic then $|E| = |V| - 1$.

Let's quickly try and prove that "If a tree has $n$ vertices and $m$ edges then $m=n-1$".

**Base Case (a single vertex):**
A tree with a single vertex does not have an edge. Therefore $n=1$ and $m=0$, making the claim true in the base case.

**Inductive step:**
Assume that any arbitrary tree that has $n\leq k$ has $n-1$ edges, and assume that $T$ has $k+1$ vertices.

If we remove an edge from $T$, we disconnect $T$ and are left with two separate data structures. $T_1$ and $T_2$. If $T_1$ or $T_2$ weren't connected, then $T$ would not have been connected, and if $T_1$ or $T_2$ contained a cycle then $T$ would also have contained a cycle.

This means that $T_1$ and $T_2$ must also both be trees.

Let $n_1$ and $n_2$ be the number of vertices in $T_1$ and $T_2$ respectively. Since no vertex was removed, this means that $n_1 + n_2 = k+1$.

An edge is removed and $T_1$ and $T_2$ both have at least 1 vertex, which means that $1 \leq n_1,n_2 \leq k$, and so by our induction hypothesis $T_1$ contains $n_1-1$ edges and $T_2$ contains $n_2-1$ edges.

Before $T$ was disconnected, it contained all of the edges in $T_1$ and $T_2$ and 1 more, making the number of edges in $T$
$$
\begin{split}
|E| 
& = (n_1 - 1) + (n_2 - 1) + 1 \\
& = (n_1 + n_2) - 1 \\
& = k + 1 - 1 \\
& = k
\end{split}
$$

And so we have proven that if all trees with $n\leq k$ have $n-1$ edges, then a tree with $k+1$ vertices must have $k$ edges.

**Conclusion:**
Since we have shown the claim to be true for our base case and our inductive step, the claim must be true for all $n\in\mathbb N$.
## Rooted Trees
We have looked at the definition of a tree, and various properties that they hold, but what do they actually look like?

Well, usually, they consist of a single **root node**, from which every other element is descended. This establishes a **hierarchy of nodes**, based on their **depth** (or distance) from the root node.

This type of tree is used frequently for all sorts of purposes, such as:
- Family Tree
- File System
- Skill Trees in Games
You can see some example images below.

![[family-tree.png]]

![[file-tree.png]]

These types of trees are called **rooted trees** and, as stated, they imply some kind of hierarchy (or direction). There do also exist **unrooted trees**, which are still connected and acyclic, but don't necessarily imply a direction. These aren't nearly as common as rooted trees, but you can see an example of the difference below

![[Rooted_vs_unrooted_phylogenetic_tree.jpg]]

>Note that in the above image only the **leaves** (nodes with no children) are labelled, but every junction would technically be a node.
### Terminology
There is quite a bit of terminology that it is useful to know when dealing with rooted trees.

Consider the tree below.

![[tree_terminology.png]]

**Root:**
	We call the topmost vertex the **root** of the tree. 
	For example, In the figure above the **root** is $r$.

**Parent/Child:**
	If a node $x$ is directly connected to a node $y$ that exists below $x$, then we say that $x$ is a **parent** of $y$ and $y$ is a **child** of $x$. 
	For example, in the figure above, we can say that $a$, $b$, and $c$ are children of $r$ and that $d$ and $e$ are children of $a$.

**Ancestor/Descendant:**
	If a node $x$ is connected directly or indirectly to a node $y$ that exists below $x$, then we say that $x$ is an **ancestor** of $y$ and that $y$ is a **descendant** of $x$. 
	For example, in the figure above, $k$ is a descendant of $a$ and $c$ is an ancestor of $q$. 
	All nodes in the tree except the root are **descendants** of the root, and the root is an **ancestor** of all other nodes in the tree.

**Degree:**
	When referring to a vertex, the **degree of the vertex** is the number of children it has. When referring to a tree, the **degree of the tree** is the max degree of all the vertices in the tree.
	For example, in the figure above, we would say that $c$ has a degree of 2 and $b$ has a degree of 1.
	We would also say that the degree of the whole tree is 3 since $r$ has a degree of 3 an no other node has a higher degree.

**Leaf:**
	A vertex with no child (also called a vertex of degree 0) is called a **leaf**.
	For example, in the figure above, the leaves are $d$, $k$, $p$, $g$, $q$, and $s$.

**Internal Vertices:**
	A vertex that is not a leaf is called an **internal vertex** or **internal node**.

**Subtree:**
	If we take any non-root node in a tree, that node will be the **root** of its own **subtree**. 
	If you look at the figure below, it breaks down the figure above into it's root node and 3 subtrees. $T_1$ is rooted at $a$, $T_2$ is rooted at $b$ and $T_3$ is rooted at $c$.

![[subtree-example.png]]
## Binary Trees
A binary tree is a tree with a degree of 2 or lower. They can always be split up into:
- A **root node**,
- A **left subtree**,
- A **right subtree**.
Where the left and right subtrees may be empty.

>There also exists an idea of a **full binary tree** (also called a **proper binary tree**) which is a binary tree in which every node has exactly 2 or 0 children. In this course we won't be dealing with them.

There are a few common ways of traversing a binary tree:
- **Preorder** Traversal (VLR) - We first visit the **vertex**, then the **left subtree**, and finally then the **right subtree**.
- **Inorder** Traversal (LVR) - We first visit the **left subtree**, then the **vertex**, and finally the the **right subtree**.
- **Postorder** Traversal (LRV) - We first visit the **left subtree**, then the **right subtree**, and finally the vertex.

>Note that whenever we traverse a tree with one of these ways, we always traverse the **left subtree** BEFORE the **right subtree**. 
>
>This makes remembering which is which really easy since the prefix just refers to where the vertex goes. Vertex first is **PRE**-order, vertex second is **IN**-order and vertex last is **POST**-order.

Below you can see an example tree and the order in which we visit each node.

![[tree_construction_from_given_inorder_and_preorder_traversals_8.webp]]

>This figure does also mention **level order traversal**, which functions like a **breadth first search**. You simply traverse each level of the tree from left to right
### Binary Search Trees
A common type of binary tree is a binary search tree. This is a binary tree in which the nodes conform to some order. 

Typically for a vertex that holds a value $x$:
- The **left child** has a value $<x$,
- The **right child** has a value $>x$.
If your tree allows duplicate values, then it would be typical to for the left child to hold values $\leq x$.

>Whether the left or right child is less than or greater to $x$ doesn't matter. All that matters is that there is an order to the tree. Although going against convention to order it backwards would be a strange choice with little benefit in most situations.
>
>Similarly, if your tree allows duplicates it doesn't matter which side the values equal to $x$ go to. The only thing that matters is that they only go to one side.

This lets us efficiently search for a given value $g$ by just comparing it to value of the current node $x$
- If $g=x$ then we have found our value.
- If $g>x$ then we check the left subtree,
- If $g<x$ then we check the right subtree.

>Note that in a binary search tree, an **inorder traversal** will always give back the numbers in ascending order, or whichever order they have been sorted into.

Binary search trees, are primarily used because they make performing a [[Lecture 5 - Array Basics & Searching#Binary Search|binary search]] very easy. A slight caveat to this is that for binary search to maintain $O(\log n)$ of binary search we need our tree to be **balanced**.

A **balanced** tree is a tree in which the **depth** of any 2 leaves doesn't differ by more than 1, and the only nodes with 1 child are direct parents of leaves. What this means that you can be sure that when you select a left or right child you are cutting the search space in half.

If a binary search tree **isn't balanced** then you have no guarantee that you are cutting the search space in half.

Lets consider the most extreme example, where the root node has the smallest value in the tree, and each subsequent descendant has the next smallest value of the tree. For an example look at the figure below.

![[list-tree.drawio.png]]

This is (technically) a **valid but unbalanced** binary search tree. You may notice that this tree is actually identical in structure to a **sorted linked list**.

Obviously when searching for an element in the tree starting at the root, if it is greater than 10 we must just move to the next element and so one. We only discard **one node** each time, when for binary search we want to discard **half** of the nodes at each step.

Below you can see a **balanced** version of the same

![[balanced-tree-example.drawio.png]]

Now performing a binary search on this tree starting at the root, the choice of which child to go to always cuts the tree in (roughly) half.