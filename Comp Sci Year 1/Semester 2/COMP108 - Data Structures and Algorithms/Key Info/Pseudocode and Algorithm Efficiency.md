## Key Definitions

**Pseudocode** is code written to be human readable, which a computer cannot interpret. This module mostly works with pseudocode algorithms and so being able to read it is important. If familiar with real programming then pseudocode should be readable to you already, but if not go to [[Lecture 2 - Pseudo Code Part 1]] and [[Lecture 3 - Pseudo Code Part 2]].

**Algorithm efficiency** is the term for how resource efficient an algorithm is. This can be either in terms of **space complexity** or **time complexity**.

**Space complexity** refers to how much storage an algorithm requires to complete relative to the size of its input. (There is very little on space complexity in this module)

**Time complexity** refers to the amount of time (measured in operations) an algorithm requires to complete relative to the size of its input.

**Time complexity analysis** is the process of counting how many operations an algorithm performs relative to some input.

**Big O notation** is a notation to show time complexity, and specifically the order of growth of a function. The specifics of it's definition and process to calculate are expanded on below.
## Time Complexity Analysis
To perform time complexity analysis, we do so by counting a given operation. Since we ignore constants in the end result, an expression in Big-O notation, we mostly care about **loop iterations**.

We (usually) only care about time complexity analysis of the worst case scenario (greatest number of operations). 

If a loop iterates $cn$ times in the worst case where $c$ is a constant it has $O(n)$ time complexity. 

If two loops iterate one after each other the resulting time complexity is $a+b$ where:
- $a$ is the time complexity of the first loop
- $b$ is the time complexity of the second loop

If a loop contains another loop, the resulting time complexity is $a \times b$ where:
- $a$ is the number of times the outer loop runs the inner loop
- $b$ is the time complexity of the inner loop.
Note that $a$ is not the time complexity of the outer loop, since it may execute the inner loop less times than this due to some checked condition.

If you cannot determine the exact number of loop iterations in the worst case, remember that if it iterates somewhere between 0 and $n$ iterations each time the loop runs, then the number of loop iterations in the worst case will be $cn$ for some constant $c$, making the time complexity $O(n)$.
### Big O Notation
The formal definition for Big-O notation is
$$
f(n) = O(g(n))
$$
when
$$
\exists c\exists n_0 \text{ such that } \forall n\geq n_0 \text { we have } f(n) \leq cg(n)
$$
This definition can be used to prove that a given algorithm is of order $O(g(n))$ after calculating that the actual number operations for the algorithm is $f(n)$

In practice, we can find the big-O of a algorithm by simply **discarding any constants** and **discarding all but the dominant term(s)**.

The **dominant term** of a function is the term which places highest in the hierarchy defined below.
### Hierarchy of Functions
We can define the hierarchy of functions as follows, lowest **order of growth** to highest:
- **Constant** - 1
- **Logarithm** - $\log n$ 
- **Polynomial** - $n,n^2,n^3,...,n^k$
- **Exponential** - $2^n$

We can also expand this to add:
- $n\log n$ between $n$ and $n^2$
- $n^2\log n$ between $n^2$ and $n^3$
- etc.

$log_an$ and $log_bn$ always differ by a constant value so we don't need the base for time complexity analysis.

$log^kn$ has a lower order of growth than $\log n$ for all $k\in\mathbb N$.









