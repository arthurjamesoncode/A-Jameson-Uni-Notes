In games where we play against an opponent, we can't be sure of the state after each action we take, as the opponents action also affects the state. The solution for this is developing a strategy that specifies a move for every possible move of the opponent.

We need a method for selecting good moves that give us the best chance of achieving a winning state no matter what the opponent does. In practice, we must use heuristics because of the combinatorial explosion.
## Problem Formulation
For some games we have a fully observable environment. The position is known completely. These are called games with perfect information. Consider, chess, backgammon and go and monopoly for example.

In other games we have a partially observable environment, where we can't see everything the opponent can. We call these games with imperfect information. 
For example poker, battleships, bridge.

Some games are deterministic, meaning that only our, and our opponent's, actions affect the state. For example, chess or go.

Other's are stochastic, meaning there is an element of chance. For example backgammon, poker, monopoly, bridge.

This module, we only consider games with the following properties:
- Deterministic
- Two-Player
- Zero-sum, meaning that either player wins and loses but both cannot win or lose at the same time
- Perfect information

So when formulating a problem we need:
- The search graph, given by all the successor states obtained by making a move.
- A utility function $u$. This replaces the set of goal states. If a state $s$ is a win condition then $u(s)=max$, otherwise is $s$ is a loss condition then $u(s)=min$. $min$ and $max$ are determined based on the game. In chess we would use $min=-1$, $max=+1$, in backgammon we would use $min=-192$, and $max=+192$.
- A start state $s_{start}$.
- A terminal test which determines if the game is over.

## The Game Tree
The game tree is a tree of possible states. Each level of the tree is labelled with the player to move and represents half a turn (or 1 players turn). It shows what happens for competing agents.

We label the players MIN and MAX:
- MAX wants to win (maximise utility)
- MIN wants MAX to lose (minimise utility)
- MAX is the hero
- MIN is the opponent

In theory, both players will play to the best of their ability. MAX wants a strategy to maximise utility assuming MIN will act to minimise MAX's utility. This gives rise to a **minimax value** of each state. This is the utility of a state considering both players play optimally.

Below we can see an example game tree for noughts and crosses.

![[game_tree_example.png]]
## Minimax Algorithm
The **minimax** value of a state depends on a few things:
- The minimax value of a terminal state is given by the utility function. 
- The minimax value of a MAX-state (when it is MAX's turn) is the maximum of the utilities of it's immediate successors.
- The minimax value of MIN-state (when it is MIN's turn) is the minimum of the utilities of it's immediate successors.

At the start of the algorithm, we need to calculate the minimax values of each state starting at the terminal states. In practice this is often impossible, so a heuristic would be used (however in our examples we will only see trees with guaranteed values).

Once we have the values we can construct the game as a minimax tree. Whenever it is MAX's turn, it takes the maximal value of it's successors. Whenever it is MIN's turn it takes the minimum value of its successors. Below you can see a sample minimax tree with all the minimax values labelled.

![[minimax_example_1.png]]

Notice that, in the minimax tree, upwards pointing triangles represent MAX's turn, and downwards pointing triangles represents min's turn.

As an exercise, try to find the minimax value of **a** in the diagram below.

![[minimax_example_2.png]]

The best way to do this is to go through each layer and write down the values at each point. Most of the time, if you have the tree on paper in front of you, you can label them directly. This is what I would recommend doing in your exams.

We know the minimax value of the terminal states, so now we use them to write the minimax values of the states in layer 3. As it is MIN's turnby just taking the minimum of the terminal successor states. So, for example $h$ would take the minimum of $1$ and $2$ and $l$ would take the minimum of $8$ & $7$.

The values of the states in layer 3 are:
- $h=1$
- $i=3$
- $j=5$
- $k=7$
- $l=7$
- $m=5$
- $n=3$
- $o=1$

Now, knowing these values we can use them to write the values of the states in in layer 2. Here it is MAX's turn so we now take the maximum of their successor states. So, for example, $d$ would take the maximum of $h$ and $i$, and $g$ would take the maximum of $n$ and $o$.

The values for the states in layer 2 are:
- $d=3$
- $e=7$
- $f=7$
- $g=3$

We then repeat for layer 1, recognising that it is MIN's turn. So $b$ is the max of $d$ and $e$ and $c$ is the max of $f$ and $g$.

The values for the states in layer are:
- $b=3$
- $c=3$

Finally to get the minimax value at layer 0, or our root minimax value, we take the maximum of its immediate successors, $b$ and $c$. Since $b=3$ and $c=3$, $a = 3$.

So the minimax value of $a$ is $3$.

### Properties of Minimax
The minimax algorithm, as described above, is optimal when playing against an optimal opponent. If an opponent plays sub-optimally, the minimax algorithm will do even better, however there may be a different strategy that outperforms the minimax algorithm.

For time and space complexity, I need to remind you that $b$ means the maximum branching factor of a tree and $m$ means the maximum depth of the tree.

The time complexity of minimax, when implemented in a depth first fashion is $b^m$, and the space complexity is $bm$.
### $\alpha-\beta$ Pruning
For chess, it's reasonable to assume $b\approx35$ and $m\approx 100$ for most games. This gives us about $10^{154}$ paths to explore, which is clearly infeasible.

We deal with this mostly through using heuristics that can approximate the minimax value of successor states, but also we don't actually need to explore every path.

If we know that a state **cannot** give us a more suitable value (a greater value if it is MAX's turn, or a smaller value if it is MIN's turn), then we do not need to fully compute the value of all successor states of that state.

Look at the tree below.
![[a-b_pruning.png]]

Since the algorithm is implemented in a depth first way, the minimax value of the leftmost successor is found first by evaluating the full subtree. 

After this, since we know MAX always takes the greatest value, we know that the value of our root is guaranteed to be $3$ or greater.

When evaluating the second successor, after checking it's first successor, we know, since MIN always takes the smallest value, that this successor can only have a value of $2$ or less. This means that it is not necessary to evaluate the rest of its successors. As max will always choose $3$ over $2$ or less.

The algorithm then goes on to evaluate the rest of the tree like so:
![[a-b_pruning_2.png]]
![[a-b_pruning_3.png]]
![[a-b_pruning_4.png]]

As we can see, since 14 and 5 are greater than 3, and it is evaluating states from left to right, we must still evaluate the whole of the right subtree before we can confirm the value of our root node.

### Cut-offs and Heuristics
As said above, for some games, like chess, the game tree is too massive for us to compute the full minimax algorithm over it, so to solve this we use cut-offs and heuristics.

Essentially the idea is that explore the game tree to some reasonable depth, which we call a cut-off. The problem is that utilities are only defined at terminal states, so instead of using true utility we apply to these states a heuristic *evaluation* function that estimates a utility value.

Once we have these for our cut offs states, we can recursively apply them to the rest of our states just as we would with true utilities.

It's worth noting that, if one of the states before the cut-off depth is a terminal state, then we use our utility function instead of our heuristic *evaluation* function.

An example of a heuristic evaluation function for chess could be to assign each of the pieces a numerical value and then calculate the different between the material of white and the material of black.

So if we gave the pieces the values:
- $pawn=1$
- $knight=3$
- $bishop=3$
- $rook=5$
- $queen=9$

And we call the sum of white's pieces $w$ and the sum of black's pieces $b$. Then we could assign $$
Evaluation(s)=\frac{w-b}{w+b}
$$
In order to estimate the value of the state for white.

This function is quite bad however, since it gives the same weight to a piece regardless of it's position on the board. The knights below clearly do not have the same value since they control different amounts of squares.
![[chess_knights.png]]

We could then improve our evaluation function by multiplying the value of a piece by the number of squares it attacks. While again, quite simple, you can see how we can heuristics functions we use to estimate utility.

Modern chess engines use much more complicated heuristics informed by machine learning.