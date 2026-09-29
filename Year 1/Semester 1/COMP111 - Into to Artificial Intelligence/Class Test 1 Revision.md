## Agents
What we call actors in various situations.
### Environments
#### Fully Observable/Partially Observable
Fully observable environments are any environment where an agent can obtain, complete, up to date info about the environments state. Partially observable is any other environment. 
#### Deterministic/Stochastic
If an agents actions are all that determine what happens in an environment that environment is deterministic. If it is deterministic except for the actions of other agents it is called "strategic".
#### Episodic/Sequential
An episodic environment is one in which an agent can decide what action to perform without based only on the current state (or episode) without having to reason about interactions with future states. An example of episodic environment is "defect detection on an assembly line".
#### Static/Dynamic
Static environments are ones in which the state does not change while an agent is deliberating. Dynamic environments do change.
#### Discrete/Continuous
Discrete environments have a finite number of states they can occupy (such as chess) while continuous environments.
### Kinds of Agents
#### Simple Reflex Agent
Only needs to know the current state and has some algorithm (condition-action rules) for deciding on its action.
#### Model Based Reflex Agent
Like a simple reflex agent but maintains some kind of internal state. This remembers previous states, has some kind of idea what the actions do and how the world evolves.
#### Goal Based Agent
Like a model based agent but requires some knowledge of a goal state and what actions alter the world to achieve it.
#### Utility Based Agent
Like a goal based agent but uses a utility function to decide which of a number of favourable states are the most favourable.
Trade offs may be made between conflicting goals. 
## Search
I am pretty confident with how I understand all of these algorithms to work. I just want to make sure I remember the time and space complexities of each of them, and to note down how to evaluate frontiers.
### Complexities & Completeness
#### Variable Definitions
- b: maximum branching factor of a graph
- d: smallest depth of solution/goal
- m: maximum depth of the graph
- l: depth of the limit in DLS
#### BFS (Breadth First Search)
Time Complexity: (1 + b + b$^2$ + … + b$^d$)
Space Complexity: b$^d$ 
Is Complete
Is Optimal
#### DFS (Depth First Search)
Time Complexity: (1 + b + b$^2$ + … + b$^m$)
Space Complexity: bm
Is not complete (can have cycles)
Is not Optimal

#### DLS (Depth Limited Search)
Time Complexity: (1 + b + b$^2$ + … + b$^l$)
Space Complexity: bl
Is not complete (if solution is too deep compared to l)
Is not optimal (if solution is not as deep as l)

#### IDS (Iterative Deepening Search)
Time Complexity: 1 + (1 + b) + (1 + b + b$^2$) + … + (1 + b + b$^2$ + … + b$^d$)
Space Complexity: bd
Is Complete
Is Optimal

### Cost Based Algorithms
The point of this section is just to remind myself what each of them do.
#### Uniform Cost 
Performs a breadth first search but expands the path with the current lowest cost.
#### Greedy
Performs a breadth first search but expands the path whose next node has the lowest heuristic value.
#### A*
Combines greedy and uniform. Adds the total cost of the path to the heuristic value of the furthest node and expands the path with the lowest total.
## The Rest
Not going to lie I think the propositional logic and probabilities are going to be very easy. We keep working in discrete probability spaces which makes it easy and I should have a lot of time.