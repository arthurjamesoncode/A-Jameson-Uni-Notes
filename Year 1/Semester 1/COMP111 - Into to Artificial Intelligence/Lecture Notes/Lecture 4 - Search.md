Consider a goal based agent, with a goal and a set of actions it can perform to try and reach the goal. The difficulty with this agents task is to decide what actions, and in what order, the agent must make to reach this goal.

The agents job here is to compute a sequence of actions that leads to the goal and possibly satisfies some other criteria, such as being the shortest possible sequence. We call this other criteria the **optimality criterion**.

In order to design an agent to solve a problem, we need a well formulated problem. The following are all things we need to describe as part of the **problem formulation**:
- The goal
- The relevant states of the world
- The possible actions of the agent
- The optimality criterion

Once we have formulated a problem, the process of looking for the sequence of actions to solve it is called **search**.
## Problems We Can Solve With Search
The following are examples of problems we can solve using search. It should be said that these are in no way extensive, they are simply examples we will revisit to attempt to illustrate how search works.
### 8 Puzzle
The 8-puzzle is a sliding puzzle that consists of a frame of numbered square tiles in random order with one tile missing. The object of the puzzle is to place the tiles in order by making sliding moves that use the empty space.

![[8_puzzle_start_goal.png]]
### Holiday in Romania
We are on holiday in Romania; currently in Arad. How can we use the map below to determine the quickest route to Bucharest.

![[holiday_in_romainia_start.png]]
### Hoover World
The hoover world is an abstract space composed of 2 rooms which may or may not contain dirt. There is one hoover which can move from left to right or right to left and suck up dirt. The goal state is for all rooms to have no dirt in them.

![[hoover_world.png]]
### The 8 Queens Problem
This is a problem from chess.

How can we place 8 queens on a chessboard such that no queen attacks any other.
![[8_queens.png]]
## Problem Formulation
In order to formulate our problem first we need to determine the set S of possible states of the problem.

Once we have this we can determine the search graph from:
- The set $S$ of states
- A start state $s_{start}$ from $S$
- A set $S_{goal}$ of states from $S$, these are the goal states
- A set $A$ of actions that can be performed to take the agent from one state in $S$ to another. Often these actions aren't given names, we just say which states are reachable from a state by a single action.
- A cost function that determines how expensive an action is. If all actions are equally expensive we just set $cost(a)=1$ for all actions $a$.

We call a sequence of actions that, when performed from the start state $S_{start}$, allow the agent to reach a goal state in $S_{goal}$ a solution. A solution is considered optimal if there is no less expensive solution.

Let's determine the search graph for our four example problems.
### 8 Puzzle
![[8_puzzle_start_goal.png]]

Our search graph is as follows:
- States $S$: every possibility of having the 3 × 3 grid filled with numbers 1–8 and a blank. 
- Start state $s_{start}$: a single state. For example, the one shown on the left. 
- Set $S_{goal}$ of goal states: the state shown on the right. 
- Four actions: move the tile to left of empty square to right; etc..
- Cost function: all actions have the same cost. (We set cost=1 for each action.) We want a shortest sequence of actions that leads from $S_{start}$ to the goal.

### Holiday in Romania
![[holiday_in_romainia_start.png]]

Our search graph is as follows:
- Set $S$ of states: being in a city from the map of Romania: in Arad, in Zerind, in Oradea, etc
- Start state $s_{start}$: in Arad; 
- Set $S_{goal}$ of goal states: in Bucharest; 
- Actions: drive from $a$ to $b$ for neighbouring cities $a$ and $b$, for example drive from Arad to Zerind. Note that there is no single action that takes you from a city to a non-neighbouring city (for example, from Arad to Oradea); 
- Cost function: km you drive. 

Notice how, in this case, the map from the previous slide is already a representation of the search graph.
### Hoover World
![[hoover_world_states.png]]

Our search graph is as follows:
- Set $S$ of states: the 8 situations depicted in the image above; 
- Start state $s_{start}$: any state;
- Set $S_{goal}$ of goal states: states 7 and 8;
- Actions: move left/right, suck up the dirt, do nothing;
- Cost function: assume all actions equally expensive (cost=1).
### 8 Queens
![[8_queens.png]] 
Our search graph is as follows:
- Set $S$ of states: any arrangement of 0 to 8 queens on the board; 
- Start state $s_{start}$: empty chess board;
- Set $S_{goal}$ of goal states: 8 queens on chess board such that no queen attacks another; 
- Actions: add a queen to an empty square; 
- Cost function: all actions equally expensive (cost=1).
### Abstraction
As the real world is incredibly complex, we must abstract the state space and actions possible when solving problems.

An abstract state is the same as a **set** of real states, an abstract action is the same as a complex combinations of real actions. For example "Arad $\to$ Zerind" represents a complex set of possible routes, detours, rests, etc.

To make sure we can realise these abstract solutions any *real* state "in Arad" must get to a *real* state "in Zerind". The abstract solution is the same as the set of real paths that are solutions in the real world.

These abstractions make the problem easier than it would be without abstractions.
### Size of the Search Graph
In all the examples given, the state space is relatively small. In most real problems the state space is much bigger. You can see the figure below for an idea of how it increases.

![[state_space_sizes.png]]

Generally we assume we can't store the whole search graph. It's imaginary. The general approach in a real problem would be to define the start state and goal states, and then create a function that transforms the state given a current state and an action.
## Search Trees
In this module, we assume:
- The start state $s_{start}$ is given;
- A description of the actions is given in the following form: if in state $s$, then states $s_1, . . . ,s_n$ can be reached by an action (they are called successor states of $s$ and $s$ is called a predecessor state of all the states $s_1,...,s_n$);
- A description of the goal states is given. 

The above gives us a search tree, starting at the start state.

Search is the systematic exploration of the search tree consisting of all possible paths of states starting with the start state using the actions available until a path to a goal state is reached.

Note that we typically don't store the whole search tree resulting from the search. It is imaginary in the context of most problems.
### Holiday in Romania Search Tree
Take our holiday in Romania example. If we start in Arad we can list all the paths of various lengths:

Our paths of length 1 are:
- Arad

Our paths of length 2 are:
- Arad, Sibiu
- Arad, Timisoara
- Arad, Zerind

Our paths of length 3 are:
- Arad, Sibiu, Arad
- Arad, Sibiu, Figaras
- etc, (8 Paths total)

We can lay out these paths in a tree structure with Arad as the root of the tree. See below.
![[holiday_in_romania_tree.png]]

>Notice how this abstract tree includes repetitions. Because of this, the tree would expand infinitely. Hence the need for it to be imaginary.

The root of the search tree is always the start state.

We can describe search algorithms by stating how the search tree is explored by the algorithm.

When we apply actions to a state, we generate longer paths by adding successor states to that state. This is called expanding a path or expanding a state. See below for an example of how we do this.

![[expanding_state.png]]
### Note on Pseudocode
In this module we will be discussing algorithms for how the search tree is being explored. These algorithms will be given in pseudocode, which is just an informal, high level description of how the algorithms work.

Pseudocode is intended for human reading rather than machine reading, and it's purpose here is just to keep the module programming language agnostic.

These algorithms often abstract from implementation details and leave certain steps that you would need to program unspecified.