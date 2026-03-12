In the last lectures [[Lecture 5 & Lecture 6 - BFS and DFS]], we covered 2 basic, uninformed tree search algorithms.
- Breadth-first search - which is complete and optimal but is expensive in terms of space complexity
- Depth-first search - which is inexpensive in terms of space complexity but incomplete and not optimal

Today we will cover variations of these algorithms that aim to fix some of their shortfalls and some improvements to search algorithms in general.
## Depth Limited Search, DLS
DLS is similar to DFS but it terminates, without finding a solution, after reaching a predetermined depth limit $l$. The idea here is that DFS's space complexity is desirable but that exploring all paths all the way to the end is not, so a limit is introduced in order to stop that. 

Below you can see the algorithm in pseudocode.

```
Input: 
	a start state s0
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state
	non-negative integer DepthLimit

Set frontier := {s0}
while frontier is not empty do
	select and remove from frontier the path s0....sk added
	last to frontier 
	if goal(sk) then 
		return s0 . . .sk (and terminate)
	else If k < DepthLimit, then for every successor s of sk
		add s0 . . .sk s to frontier
	end if
end while
```

![[holiday_in_romainia_start.png]]
If we look at the holiday in Romania example from before (see above) we can see that, as there are only 20 cities on the map. This means there are no paths with longer 19 cities which do not repeat a city. So we could choose a limit of 20.

If we look even more closely we can see that Bucharest can be reached from any other city in less than 10 steps. So we could choose a limit of 10.

If you use a DLS approach having some way to understand what an approximate limit should be is very important. If your limit is too small you will never find a solution. If your limit is too big you run into similar problems as with DFS.

Properties of DLS:
- DLS is not **complete**, as if the limit is too short it will not find a solution
- DLS is not **optimal**, as, if the limit is greater than the shortest path to the goal, there is no guarantee the path found will be the shortest.
- DLS has a time complexity of $1 + b + b^2 + ··· + b^l$. This is the same as DFS but using the limit in place of the maximal depth.
- DLS has a space complexity $bl$. Again this is the same as DFS but using the limit in place of the maximal depth.
## Iterative Deepening Search, IDS
DLS is meant to address the shortfalls of DFS, however it still is not complete or optimal. Iterative deepening search is a complete version of it.

Essentially the basic idea of IDS is:
- Complete a DLS with $l=0$. If a solution is found, return it.
- If no solution is found, then complete a DLS for depth $l+1$. If a solution is found, return it.
- Otherwise, repeat the second step until a solution is found.

So it's essentially a repetitive DLS. 

This is useful is the search space is large and the maximum depth of the solution is not known.

You can see below what happens at each stage of an IDS algorithm.

Stage 1:
![[ids_1.png]]
Stage 2:
![[ids_2.png]]
Stage 3:
![[ids_3.png]]
And so on.

Below you can see the algorithm in pseudocode.

```
Input: 
	a start state s0
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state

Set DepthLimit := 0
repeat
	Result := depth_limited_search(DepthLimit)
	if Result is a path s0...sk then
		return s0...sk (and terminate)
	else DepthLimit := DepthLimit + 1
	end if
until False
```

Notice how we simply call DLS as a function passing in our new depth limit each time.

Properties of IDS:
- IDS is complete, as it always finds a path to the goal state.
- IDS is optimal, as it always finds the shortest path to the goal state.
- The time complexity of IDS is $1 + (1 + b) + (1 + b + b^2 ) + · · · + (1 + b + b^2 + · · · + b^d )$. This is because IDS has to re-traverse the tree upon each limit increasing.
- The space complexity of IDS is $bd$, where $d$ is the shortest path a goal state.

Since we have to traverse the tree again upon each iteration, the time complexity of IDS is higher than that of any of the other algorithms we have looked at so far.

Compared to BFS, IDS takes a relatively small of extra time, but saves a lot of memory.

For example:
	Let $b=10$, $d=5$.
	BFS, in the worst case, would need to examine $1+10+...+10^5=111,111$ paths and would need to store $10^5=100,000$ paths.
	IDS, in the worst case, would need to examine $1+(1+10)+(1+10+10^2)+...+(1+...+10^5)=123,456$ paths and need to store $10*5=50$ paths.

In that example, IDS takes 11% longer, but needs to store $\frac{1}{2000}$ of the paths that BFS does.
## Algorithmic Improvements
### Avoiding Repeated States
So far in this course we have not done anything to handle repeated states. You may have noticed that "Arad" comes up many times in the tree for the Romania example.

![[holiday_in_romania_tree.png]]

Expanding these states, at best, in the case of BFS, wastes time, and at worst, in the case of DFS, causes infinite loops to exist.

In order to avoid these problems we can do the following:
- Do not return to the state we have just come from
- Do not create a path if the current state already exists in the current, selected path
- Do not create a path if the current state has occurred in a path created earlier

There is a trade off between the cost of extra search and the cost of checking for repeated states.

>Usually, in most high level languages, you could have a set, hash table, or a similar data structure of visited states. Since these structures have a lookup time complexity of O(1) the cost of checking for repeated states is quite low.

## Bi-Directional Search
If we do a bi-directional search, that means that we search for the start state from the goal state as well as search for the goal state from the start state.

This means we would need to reverse the set of actions so that we can determine the predecessor of the goal state, and it's predecessors, as well as the successor states of any given state.

This means we complete 2 searches up to depth $\frac{d}{2}$. You can then combine paths that contain the same state in order to create a full path from the start to the goal.

We can see how this is much more efficient:
	Let $b=10$, $d=6$
	BFS will examine $1+b+...b^6=1,111,111$ paths
	Bi-directional BFS will examine $2\times(1+b+b^2+b^3)=2,222$ paths.

So in this example bi-directional search is just over 500 times faster.

You can also combine different search strategies in different directions.

There are still some problematic properties of Bi-Directional Search:
- Must be able to generate predecessors of states.
- There must be an efficient way to check whether a new state appears in the other search.
- For large $d$ (lol), still impractical!
- For two bi-directional breadth-first searches, with branching factor $b$ and depth of the solution $d$ we have memory requirement of $b^{d/2}$ for each search which is still exponential.



