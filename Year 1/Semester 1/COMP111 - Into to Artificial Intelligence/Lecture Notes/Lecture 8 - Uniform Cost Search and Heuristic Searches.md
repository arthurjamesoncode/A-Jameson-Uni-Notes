## Uniform Cost Search
During problem formulation, we need a cost function. This is a function that applies a cost to each action. The total cost of a path is the cost of the actions taken at each step.

As an example, recall the "holiday in Romania" search graph (pictured below). Here the actions available to our agent are to drive to any neighbouring city, and the cost function simply returns the distance between the current city and this neighbouring one.
![[holiday_in_romainia_start.png]]

Uniform cost search is a modification to breadth first search that expands the cheapest path first. 

In the "holiday in Romania" graph, since, after expanding Arad, we have "Arad $\to$ Zerind, Cost 75", "Arad $\to$ Sibiu, Cost 140", and "Arad $\to$ Timisoara, Cost 118", a uniform cost algorithm would expand the cheapest of these which is "Arad $\to$ Zerind, Cost 75". After this the frontier would contain "Arad $\to$ Zerind $\to$ Oradea, Cost 146", "Arad $\to$ Sibiu, Cost 140", and "Arad $\to$ Timisoara, Cost 118". At this step the uniform cost search would expand "Arad $\to$ Timisoara, Cost 118" as now that is the cheapest path.

This, intuitively, slightly increases performance in most cases since choosing the cheapest path at each step makes it more likely that you choose the best path.

If we have a problem where the cost of every step is 1, then uniform cost search is exactly the same as breadth first search.

Below you can see a general pseudocode algorithm for uniform cost search
```
Input: 
	a start state s0
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state
	cost(s0,...,sk) for every path s0,...,sk

Set frontier := {s0}
while frontier is not empty do
	select and remove from frontier the path s0....sk with cost(s0,...,sk) minimal
	if goal(sk) then
		return s0,...,sk (and terminate)
	else for every successor s of sk add s0,...,sk,s to frontier
	end if
end while
```

Below you can see a detailed example with the frontier stored at each step.
![[uniform_cost_example.png]]

Uniform cost search is complete and optimal, as it is guaranteed to find the cheapest solution assuming the path costs grow monotonically, which just means that no action has a negative cost.

If path costs don't grow monotonically, then an exhaustive search is required.

In terms of time and space complexity, it is identical to BFS. You can check here [[Lecture 5 & Lecture 6 - BFS and DFS]] for specifics.

Whatever search technique we use, there is exponential time complexity. We can tweak the algorithm to try and reduce it but whatever we do we can't reduce it to polynomial.

It takes problem specific knowledge in order to make the search more efficient. The simplest form of this is called a heuristic.
## Heuristics
We often need to use more specific information about a state space to solve it using a search. If we can estimate how promising a path is based on our knowledge then we can select the most promising one first. 

If we are good at estimating what path is the most promising, we can greatly cut down the number of paths expanded and make our algorithm run much faster.

Heuristics are a simple way to estimate how promising each specific path is. 

We have a heuristic function $h: States \to \mathbb{R}$, which looks at a state and estimates how expensive it will be to go from that state to the goal. This could be anything from the distance to the goal in a straight line to a randomly selected number, the only constraint is that $h(goal)=0$  Obviously some heuristic function will do a better job at estimating than others.
## Greedy Search
Greedy search is a search algorithm similar to uniform cost except, instead of expanding the least expensive path so far, it expands the path that *appears* closest to the goal based on our heuristic function $h$.

Below you can see the algorithm for greedy search written in pseudocode.
```
Input: 
	a start state s0 
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state
	h(s) for every state s
	
Set frontier := {s0}
while frontier is not empty do
	select and remove from frontier the path s0....sk with h(sk) minimal 
	if goal(sk) then
		return s0,...,sk (and terminate)
	else for every successor s of sk add s0,...,sk,s to frontier 
	end if
end while
```

Below you can see a detailed example with all of the frontiers as it expands them
![[uniform_cost_example.png]]

We can also see how a greedy algorithm solves our Romania example. Below we can see the search graph from before with all the straight line distances to Bucharest.

![[romania_heuristic.png]]

We can see that greedy search takes the steps below.
![[greedy_1.png]]
![[greedy_2.png]]
![[greedy_3.png]]
![[greedy_4.png]]

Greedy search can sometimes find solutions very quickly if the heuristic is good, but it doesn't always find the best solution. Sometimes it won't be able to find a solution at all if the heuristic function leads to infinite loops.

This means that greedy search is incomplete and not optimal. This is true even with a decent heuristic since greedy only looks the latest state in a path and ignores the total cost of each path.
## A* Search
A* is another heuristic search algorithm that was developed in 1968 in Stanford by the team that constructed Shakey, the robot.

The basic idea of it is to combine uniform cost search and greedy search. Essentially we sum both the cost so far and the estimated cost to the goal. 

So we have a function $f(s_0,...,s_k)=cost(s_0,...,s_k) + h(s_k)$, and we expand the path for which this is minimal. This aims to minimise the overall cost.

Below you can see the pseudocode algorithm for A* search.
```
Input: 
	a start state s0
	for each state s the successors of s
	a test goal(s) checking whether s is a goal state
	g(s0,...,sk) for every path s0,...,sk
	h(s) for every state s

Set frontier := {s0}
while frontier is not empty do
	select and remove from frontier the path s0,...,sk 
	with g(s0,...,sk) + h(sk) minimal
	if goal(sk) then
		return s0,...,sk (and terminate)
	else for every successor s of sk add s0,...,sk,s to frontier
	end if
end while
```

Below you can see a detailed example of the A* algorithm, with all the frontiers at each step.
![[a_star_example.png]]

We can also apply this to our Romania example. Below you can see the search graph again with the straight line distances to Bucharest on the side.

![[romania_heuristic.png]]

You can how A* traverses this graph below.
![[a_star_1.png]]
![[a_star_2.png]]![[a_star_3.png]]![[a_star_4.png]]![[a_star_5.png]]![[a_star_6.png]]

A* is complete and optimal given an **admissible** heuristic function $h$ is used. A heuristic $h$ is admissible if $h(s)\leq h^*(s)$ where $h^*(s)$ is the true distance to the goal.

Essentially a heuristic is admissible as long as it never overestimates the distance to the goal. A straight line is always the shortest path from A $\to$ B so using a straight line is a good example of an admissible heuristic when the problem involves physical space.

We can see some more examples if we look at the 8 puzzle again.

![[8_puzzle_start_goal.png]]

Here we have a couple options of good admissible heuristics:
- $h_1(s)=$ The number of misplaced tiles
- $h_2(s)=$ The sum of the Manhattan distance of each tile from it's desired location. Manhattan distance is the sum of the horizontal and vertical displacement so the Manhattan distance of the 1 tile in the start state from it's desired location is 4, since it is 2 tiles right and 2 tiles down from where it should be.

We know $h_1$ is admissible since if a tile is misplaced it takes at least 1 move to get it to the correct place, meaning that $h_1$ will never exceed the number of moves to the goal state. 

We know $h_2$ is admissible since it always takes as many or more moves to get a tile into the correct place as the Manhattan distance from the correct place.

We can see the importance of heuristic choice by looking at the data below. We can see the average number of paths examined over 100 instances of the 8 puzzle game.

When the shortest path to the goal is 14:
- Iterative Deepening Search - Examines 3,473,941 paths
- A* with $h_1$ - Examines 539 paths
- A* with $h_2$ - Examines 113 paths

When the shortest path to the goal is 24:
- Iterative Deepening Search - Examines ≈54,000,000,000 paths
- A* with $h_1$ - Examines 39,135 paths
- A* with $h_2$ - Examines 1,641 paths

As you can see, using either of these heuristics drastically decreases the number of paths our algorithm needs to examine. It is more than 6,000 times as efficient when choosing $h_1$ and more than 30,000 times as efficient when choosing $h_2$.

Choosing the better heuristic can still have a huge impact. When the shortest path is 24, choosing $h_2$ is more than 20 times as effective as choosing $h_1$