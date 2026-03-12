Note that, in order to group relevant content together, I have combined the notes for lectures 5 and 6.

In order to solve search related problems we require algorithms for exploring the search trees. As said at the end of [[Lecture 4 - Search]], these algorithms will be given in pseudocode.
## Generic Search Algorithm
Below we can see a generic search algorithm for exploring a search tree.

```
Input: 
	a start state s0
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state
	
Set frontier := {s0}
while frontier is not empty do
	select and remove from frontier a path s0,....,sk 
	if goal(sk) then 
		return s0,...,sk (and terminate)
	else for every successor s of sk add s0,...,sk,s to frontier
	end if
end while
```

As you can see, the inputs are:
- A start state, $S_0$
- A method to produce the successor states of a state
- A method to check if a state is a goal state, $goal(s)$

The algorithm maintains a set called **frontier** which contain all the paths currently being explored. At the start it only contains the path $s_0$. We can also call the frontier the **agenda**.

As long as frontier is not empty it selects and removes a path from frontier. We now say that this path is expanded. 

If the final state of the selected path is a goal state then the program terminates and returns this path. Otherwise it adds to frontier all paths obtained by expanding (adding a successor to) the selected path.

It then repeats these steps until frontier is empty or the goal has been reached.

This generic algorithm leaves a few steps open:
- Which path $s_0,...,s_k$ do we select and remove from the frontier. We can also say which path do we expand.
- Given a path $s_0,...,s_k$ in which order do we add the expansions $s_0,...,s_k,s$ to the frontier.

We don't generally specify the order in which we add $s_0,...,s_k,s$ (this is called "don't care non-determinism") but we do address the problem of which path we expand from the frontier. 

The two obvious strategies for this are:
- Breadth First Search, BFS, or to always expand the earliest path added to the frontier 
- Depth First Search, DFS, or to always expand the latest path added to the frontier
### Breadth First Search (BFS)
The algorithm for BFS is as follows:
- Start by expanding the start state - gives tree of depth 1
- Then expand all paths that resulted from previous step - gives tree of depth 2
- Then expand all paths that resulted from previous step - gives tree of depth 3
- and so on
 
In general you expand all paths of depth n before depth n + 1.

Take the maze below:
![[maze_start.png]]
If we apply a DFS to this maze we get the following paths
![[bfs_maze_1.png]]
![[bfs_maze_2.png]]
And so on until we have![[bfs_maze_3.png]]
After which we start to expand these paths to get something like
![[bfs_maze_4.png]]
And this then continues.

You can see full pseudocode for this below
```
Input: 
	a start state s0
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state

Set frontier := {s0}
while frontier is not empty do
	select and remove from frontier the path s0,....,sk that was 
	first added to frontier
	if goal(sk ) then 
		return s0,...,sk (and terminate)
	else for every successor s of sk add s0,...,sk,s to frontier
	end if
end while
```

You can see below an example of BFS with all the frontiers at each step.
![[bfs_table_example.png]]
### Depth First Search, DFS
The algorithm for DFS is as follows:
- Start by selecting start state
- Select one of the paths resulting from 1st step
- Select one of the paths resulting from 2nd step
- Select one of the paths resulting from 3nd step
- And so on

Generally, you always select the longest (also called deepest) path. This means that you follow one “branch” of search tree until the very end, before changing to a different branch.

Take the same maze from the BFS example
![[maze_start.png]]

Now instead of expanding all the paths around the start we expand them like so
![[dfs_maze_1.png]]
![[dfs_maze_2.png]]

Until we eventually get to
![[dfs_maze_3.png]]
After which we start to back track, and expand earlier paths.

The pseudocode for DFS is as follows:
```
Input: 
	a start state s0
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state
	
Set frontier := {s0}
while frontier is not empty do
	select and remove from frontier the path s0,....,sk that was
	last added to frontier 
	if goal(sk) then
		return s0,...,sk (and terminate)
	else for every successor s of sk add s0,...,sk,s to frontier
	end if
end while
```

You can see below an example of DFS with all the frontiers at each step.
![[dfs_table_example.png]]

## Properties of Search Algorithms
There are many different properties that we can use to compare search algorithms. These include:
- Completeness: does the algorithm always find a solution if one exists?
- Optimality: does the algorithm always find the shortest path to a solution?
- Time complexity: what is the maximum number of paths generated?
- Space complexity: what is the maximum number of paths in memory?

For completeness and optimality we can already classify BFS and DFS.

BFS is complete and optimal, as it always finds a solution and the solution it finds is always the shortest one.

DFS is not complete, as if there are cycles in the search graph it could never terminate, and it is not optimal, as there is no guarantee that the path found is the shortest one.

To compute the time and space complexity of these algorithms we need to know the following things about our graphs:
- $b$ - The maximum branching factor of the search tree. This is the maximal number of successor states that follow any single state.
- $d$ - The depth of the optimal solution. This is the length of the shortest path from the start state to a goal state.
- $m$ - The maximum depth of the search tree. This is the length of the largest path in the search tree. Can be infinite if the state space contains cycles and we have not accounted for repetitions.

Facts about search trees:
- The number of paths of length $x$ in a search tree with a maximum branching factor $b$ is $b^x$.
- The number of paths of length $\leq x$ in a search tree with a maximum branching factor $b$ is at most $1+b+b^2+...+b^x$

This means that breadth first search has:
- A time complexity of $1+b+b^2+...+b^d$, which is exponential.
- A space complexity of $b^d$, which is exponential.

This means that depth first search has:
- A time complexity of $1+b+b^2+...+b^m$, which is exponential.
- A space complexity of $bm$. This is because each path does not need to be stored in the frontier after it's "branch" has been fully expanded.
### Comparing BFS and DFS
The first, obvious, advantages of BFS are that it is complete and optimal, while DFS is not. This makes a raw DFS algorithm useless on any state space that contains cycles, or any problem where finding the shortest solution is vital.

They also have similar time complexities, $1+b+b^2+...+b^m$ vs $1+b+b^2+...+b^d$. BFS does slightly better here since $m\leq d$, but this doesn't make a huge difference to time taken.

When comparing space complexities, however, DFS massively outshines BFS. $b^d$ is much more than $bm$ at scale making DFS pretty cheap relative to BFS.

To sum up:
- BFS is complete and optimal, but expensive.
- DFS is incomplete and not optimal, but inexpensive in terms of space complexity.

There are adjustments we can make to these algorithms in order to mitigate their downsides, as well as other algorithms that fare better in various ways. We will learn all about this later on in the course.