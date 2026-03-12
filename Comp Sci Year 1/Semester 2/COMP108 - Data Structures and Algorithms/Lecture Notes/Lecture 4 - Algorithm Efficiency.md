Despite the speed of computation by hardware being improved, efficiency still matters greatly when it comes to algorithms. 

Ambition for computer software grows with computer power, resulting in an increasing demand for speed of computation. When hardware is pushed to its limit, all we can do is increase the efficiency of our algorithms.

The benefits of efficient algorithms are fairly self explanatory.
## Time Complexity Analysis
How can be measure how **fast** an algorithm is?

One approach could be to code the algorithm, run the program and then time how long it takes to complete its task.

However there are 2 big problems with this process:
- It depends on the speed of the computer. There is no point of shipping an algorithm that works well on your computer, but is far too slow on your users computers.
- It can be a big waste of time to program the algorithm and test if the algorithm is too slow.

So instead of this, we identify some important operations/steps and count how many times these operations/steps must be executed. We can then express this number in terms of input size.

This has a few big advantages:
- It tells us how our algorithm scales with input size
- It does not require us to actually program and test the algorithm
- As we are not running it on any computer, it does not change with the hardware we run it on.

Imagine we have an algorithm that takes $n^2$ comparisons to sort $n$ numbers, and needs 1 second to sort 5 numbers (which takes 25 comparisons).

Now imagine that hardware's speed of computation increases by a factor of 100.

Now it takes us 1 second to make 2500 comparisons, which is what is required to sort $\sqrt{2500}=50$ numbers.

So while our speed of computation increases by 100, we can only sort 10 times as many numbers in the same time.

If we had an algorithm that took $n\log_2 n$ comparisons to sort numbers we actually get much much more out of our increased speed of hardware. 

Imagine it takes us 1 second to sort 4 numbers, which takes $4\log_2 4=8$ comparisons. Now imagine our hardware speed increases by 100. Now, in 1 second we can make 800 comparisons. Since $800 = n\log_2n$ we can solve for $n$ to find this allows us to sort roughly 116 items. 

This is 29 times more than 4. So now, our 100x speed improvement translates to being able to sort 29 times more things compared to 10x more when our algorithm took $n^2$ comparisons.
### Example
Take the following pseudocode algorithm:
```
sum ← 0, i ← 1 
while i <= n do 
begin 
	sum ← sum + i 
	i ← i + 1 
end
output sum
```

We need to identify an important operation, before we can count how may times it happens. In this case, we can identify **addition** as the important operation and start to count how many times we need to perform an addition.

We can see that the loop executes while `i <= n` and that `i` starts as 1 and increments by one every time the loop runs. This means the loop executes $n$ times. Since two additions, `sum + i` and `i + 1` happen each time the loop runs, this means that it performs $2n$ additions over the full run time.
## Comparing Algorithms
Consider a problem which can be solved by 5 algorithms $A_1,A_2,A_3,A_4,A_5$ using different numbers of operations (time complexity). Below you can see examples of the number of operations given as functions of $n$ where $f_1(n)$ gives the time complexity of $A_1$ and so on.
- $f_1(n) = 50n + 20$
- $f_2(n) = 10n\log_2n$
- $f_3(n)=n^2-3n+6$
- $f_4(n) = 2n^2$
- $f_5(n) = \frac{2^n}8-\frac{n}4+2$

Below you can see a table that shows how many operations each algorithm will take for various different sizes of $n$
![[function_comparison_table.png]]
You can see as well that, for very small $n$, $f_5$ is the fastest and, for the largest $n$, $f_1$ is the fastest.

So which is the fastest. There are 2 *correct* answers here. The first is that it depends on what $n$ is. We can see this to be true. The other is $f_1$, since it **scales** the best out of all of them.

Below you can see a graph of the various functions. Note that the $x$-axis is labelled with powers of two, not a uniform scale. This should explain why parabolas seem to be closer to straight lines than usual.
![[graphed_functions.png]]

From this graph you can see how all of these functions **scale** as $n$ increases. $f_5$ clearly scales the worst out of all of them since by values of $n$ as small as 32 its already leaving the graph. This is because $f_5$ is an **exponential** function.

We can also see that there is a far smaller difference between the **polynomial** functions.

While polynomial functions don't differ as much as exponential ones, there is still a pretty significant difference between polynomials of different orders. It's hard to see this on the graph above because of the uneven labels, but you can see it more clearly if we look at the graph below.

![[comparison_graph.png]]

You can also view the table below to see how various function scale.

![[scale_table.png]]
### Hierarchy of Functions
We can define a hierarchy of functions based on their **order of growth** (how well they scale).

So we can define the hierarchy as follows, lowest **order of growth** to highest:
- **Constant** - 1
- **Logarithm** - $\log n$ 
- **Polynomial** - $n,n^2,n^3,...,n^k$
- **Exponential** - $2^n$

We can also expand this to add:
- $n\log n$ between $n$ and $n^2$
- $n^2\log n$ between $n^2$ and $n^3$
- etc.

What about $\log^3 n=(\log n)^3$ and $n$? Assuming we are using $\log_2$, since $n=2^{\log_2 n}$ we are comparing $(\log_2 n)^3$ and $2^{\log_2 n}$. As $n^3$ is lower in the hierarchy than $2^n$ we know that $\log_2^3 n$ is lower in the hierarchy than $n$. 

From the same logic we know that for all $k$: $\log^k n$ is lower in the hierarchy than $n$.

We can actually do away with the base of $\log$ entirely when doing time complexity analysis. This is because we can use the change of base formula to change the base of a logarithm.

The change of base formula is:$$
\log_a(b) = \frac{\log_c(b)}{\log_c(a)}
$$which means to change from $log_2(x)$ to $log_3(x)$ we can do it like this $$
\begin{split}
\log_3(x) 
& = \frac{\log_2(x)}{\log_2(3)} \\
& = \frac{1}{\log_2(3)} \times \log_2(x)
\end{split}
$$As $\frac{1}{\log_2(3)}$ is a constant, this means that logarithms of different bases only differ by a constant multiplication and therefore the differences between them are negligible at scale.
### Big-O Notation
If we consider the function $f(n)=2n^3 + 5n^2+4n + 7$, we can recognise that the term with the highest power is $2n^3$. This is the term that, alone, takes the highest spot in our hierarchy (I will call these terms the **greatest** term from now on).

The **greatest term** of a function $f(n)$, in this case $2n^3$, dominates the growth rate of $f(n)$. This is the idea behind **Big-O** notation.

Statements in Big-O notation take the form $$
f(n) = O(g(n))
$$and are read as "f of n is of order g of n", or similar.

The rough definition of this means that $f(n)$ is at most a constant times $g(n)$ for all large $n$. You can think about this as simplifying a function to its **greatest term** and removing all constants.

So:
- $n^3 + 3n^2 + 3 = O(n^3)$
- $4n^2\log n + n^3 + 5n^2 + n = O(n^3)$
- $2n^2 + n^2\log n=O(n^2\log n)$  
- $6n^2 + 2^n = O(2^n)$

Big-O notation is our main way of comparing the efficiency of various algorithms. 

The formal definition of Big-O notation is this $$
f(n) = O(g(n))
$$where $$
\exists c\exists n_0 \text{ such that } \forall n\geq n_0 \text { we have } f(n) \leq cg(n)
$$
We can use this to prove that certain functions have certain big O notations.

Take the function $$
f(n)=n^2 + 4n
$$If we choose $c=2$ and $n_0=4$ then we can observe that $$
n^2 + 4n  \leq n^2 + n^2 \;\;\;\; \forall n\geq 4
$$and $$
n^2 + n^2 = 2n^2
$$
