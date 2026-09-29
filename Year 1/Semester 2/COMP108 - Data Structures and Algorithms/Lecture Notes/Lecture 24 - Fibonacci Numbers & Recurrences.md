So far we have looked at a number of divide and conquer algorithms which all divide by splitting the problem in 2. This is not necessarily always the case. Some algorithms don't divide by two but just look at a slightly smaller version of the problem. 

These algorithms still follow the divide and conquer pattern, and this lecture is going to be spent going over some examples, as well as a tool (recurrence) for deriving the time complexity of these recursive algorithms.
## The Tower of Hanoi
The tower of Hanoi is a simple puzzle which goes as follows:

"You are given three pegs labelled $A$, $B$, and $C$. there are some discs, all of different sizes, on peg $A$, but peg $B$ and $C$ are empty. 

You can only move 1 disc at a time, and you cannot place a larger disc on top of a smaller disc.

What is the smallest possible number of moves to move every disc from $A$ to $C$ in terms of the number of discs $n$, and how can we write an algorithm to move these discs for us?"

We will start by finding a answer to the first part.
### Counting the Moves
Below you can see a figure depicting this problem when we start with 3 discs.
![[hanoi3.png]]

Trying to solve this is a bit tricky and so what we are going to do is look at how the problem grows in complexity. To do this we will start by considering the most simple case: $n=1$.

![[hanoi1.png]]

The number of moves here is obvious, it takes only 1 move moving it from $A$ to $C$. But what about when $n=2$?

![[hanoi2.png]]

Well now it gets a little more complicated. Our goal is to move all the discs to $C$ but lets start by considering how we move the bottom disk to $C$.

We can do that in $2$ moves, first moving the top disk to $B$, and then the bottom disk to $C$. Leaving us with the following

![[hanoi2_1.png]]

Now our problem is just the same as before. We need to move 1 disk from one post (before $A$, now $B$) to another post $C$. This takes 1 more move and so this takes 3 moves in total.

Now lets consider the case when $n=3$.

![[hanoi3.png]]

We still need to first move the bottom disk to $C$. This means that we need to move both the smaller disks to $B$ first to free up the bottom disk. Moving 2 disks to another post is a problem we have already solved, it takes 3 moves. 

We can do this and end up with:
![[hanoi3_1.png]]

Then it takes 1 move to move the bottom post to $C$, and another move 3 moves to move the two discs on $B$ onto $C$.

Let's think about this problem when we start with $n$ disks on $A$:
- We always need to move the bottom disk on $A$ to $C$ before any others. This means that we must always first move $n-1$ discs to $B$.
- After moving $n-1$ discs to $B$, we then must move the last disk to $C$ adding a single operation
- Finally, we need to move those $n-1$ discs onto $C$

If you notice that we can find this by relying on the smaller cases we've already found, you can start to realise that a **recursive** algorithm may be able to find out how many moves it takes for the general case. 

We have our base case, which is when $n=1$, and we have a recursive step. Letting us put together an algorithm like so
```
HanoiMoves(n)
begin
	if n == 1 then
		return 1
	endif
	
	return (2 * HanoiMoves(n-1)) + 1
end
```

>Note that this algorithm, while recursive, doesn't really follow the divide and conquer pattern. It simply reduces the sample size, rather than splitting it into multiple parts.
>
>Look to the next section on [[Lecture 24 - Fibonacci Numbers & Recurrences#Making the Moves|making the moves]] for an actual example of divide and conquer.

This algorithm gives an $O(n)$ way to find the number of moves but we don't actually need this algorithm to determine the number of moves. The number of moves will always be $2^{n}-1$, which we can usually calculate in $O(1)$ time.

However, since we have shown that this algorithm works for determining the number of moves we can actually use this algorithm to prove this property by induction.

**Claim:** $HanoiMoves(n)=2^n-1$

**Base Case:** $n=1$
When $n=1$ $HanoiMoves(n)=1$. 

Since $1=2^1-1$, we know that the claim holds in this case.

**Inductive Step:** Assume truth for $n=k$
Assume $HanoiMoves(k)=2^k-1$

By definition 
$$
\begin{split}
HanoiMoves(k+1)
& = 2 \cdot HanoiMoves(k) + 1 \\
& = 2 \cdot (2^k - 1) + 1 \\
& = 2^{k+1}-1
\end{split}
$$
As $2^{k+1}-1$ is of the form $2^n-1$, we have proved that if the condition holds for $n=k$ it must also hold for $n=k+1$.

**Conclusion:**
Since we have shown that the claim holds for both the base case and inductive step, we have proven that the claims for all $n\in\mathbb{Z}^+$.
## Making the Moves
So we now need to make a way to make all of these moves. I think building and coding a robot arm is a bit out of scope of this module so we will settle for simulating them.

Now our problem is simpler: Create an algorithm which can generate the in-order list of moves which would need to be made to optimally solve the tower of Hanoi starting with $n$ discs.

The moves will be represented as strings of the form `"SOURCE to DESTINATION"`, but the exact implementation of how we store and add to this list doesn't matter, for the sake of the pseudocode I will use `list.add(element)` to add an element and `list1.addAll(list2)` to add all elements of `list2` to `list1`. I will also use `+` to concatenate strings.

We are going to write a recursive algorithm, so we should figure out what information each **recursive call** needs. Which is:
- The number of discs to move ($n$)
- The post they need to be moved from (`source`)
- The post they need to be moved to (`dest`)
- The other post (`spare`)

At each step:
- if $n$ is 1, then return a list containing only `source + " to " + dest`
- otherwise, we need to
	- get the list of moves to move $n-1$ disks from `source` to `spare`
	- add `source + " to " + dest` to the list
	- concatenate the list of moves to move $n-1$ disks from `spare` to `dest`

This is a complete algorithm which will write into some more formal pseudocode.
```
Hanoi(n, source, dest, spare)
begin
	list = empty list
	move = source + " to " + dest
	
	if n == 1 then
		list.add(move)
		return list
	endif
	
	before = Hanoi(n-1, source, spare, dest)
	after = Hanoi(n-1, spare, dest, source)
	
	list.addAll(after)
	list.addAll(before)
	list.add(move)
end
```
This algorithm is a **divide and conquer** algorithm.

Notice that this algorithm does 3 things:
- Get the list before moving the largest disk (divide part 1)
- Get the list after moving the largest disk (divide part 2)
- Return a new list consisting of the moves before, moving the largest disk, and the moves after (conquer)

We have also shown in the last section that the time complexity of this algorithm is $O(2^n)$ and cannot be lowered further.
## Fibonacci Numbers
The Fibonacci numbers is a sequence of numbers in which every number is the sum of the two that precede it.

The $n^{th}$  Fibonacci number is denoted by $F_n,$ the first two numbers in this sequence are $F_1=1$ and $F_2=1$. Sometimes you will see a $0^{th}$ element included $F_0=0$.

The formal definition for function $F:\mathbb N\to\mathbb N$ which provides $F_n$ is
$$
F(n)=
\cases{
\begin{split}
0 &\; \text{ if } n=0 \\
1 &\; \text{ if } n=1 \text{ or } n=2 \\
F(n-1) + F(n-2) &\; \text{ if } n > 2
\end{split}
}
$$

>In the slides, prudence doesn't include the 0 case and Prudence's 1 case is $\text{if } n=1 \text{ or } n=0$. This doesn't really change anything about the problem, but just note that she indexes them differently.

We can write some pseudocode for this function like so
```
F(n)
begin
	if n == 0 OR n == 1 then
		return 1
	endif
	
	return F(n-1) + F(n-2)
end
```

You can see from this that is a natural **divide and conquer** algorithm. The problem is **divided** into finding the $(n-2)^{th}$ Fibonacci Number and the $(n-1)^{th}$ Fibonacci number and then **conquered** by adding them.

While this is a **divide and conquer** algorithm, it's not a particularly efficient one if put into most programming languages. The reason for this is that a lot of work is done twice. We can look at how fast this is by using a **recurrence**.

>We have already seen how this can be inefficient when looking at [[Lecture 9 - More Complex Recursion#Multiple Recursion|multiple recursion]] in the COMP105 course, including a way to make this more efficient. We will see another way to make this algorithm more efficient in the [[Lecture 25 - Dynamic Programming|next lecture]].
## Recurrence
A recurrence is an equation or inequality that describes a function in terms of its value on smaller inputs. We have actually already seen a recurrence today already, the definition for the Fibonacci numbers $F(n)$.

We can define another recurrence $T:\mathbb N\to\mathbb N$ which gives us the time taken to compute the the $n^{th}$ Fibonacci number like so:
$$
T(n)=
\cases{
\begin{split}
1 &\; \text{ if } n \leq 2 \\
T(n-1) + T(n-2) + 1 &\; \text{ if } n > 2
\end{split}
}
$$
If $n$ is 1 or 2 then we know we just need to return a value, and so that only takes a single operation. If $n$ is greater than 2 however, we still need to return a value, adding 1 to our total, but we also need to add the time it takes to find the $(n-1)^{th}$ value and the $(n-2)^{th}$ value.

You may notice that we can also find recurrences for our other divide and conquer algorithms. For example for merge sort
$$
T(n)=
\cases{
\begin{split}
1 &\; \text{ if } n=1\\
2\cdot T\Bigl(\frac n2\Bigr) + n &\; \text{ if } n > 2
\end{split}
}
$$
Here, if we only have a list with 1 item ($n=1$), then we just return that list. Otherwise, we need to find the time it takes for merge sort to sort both halves of the list ($2\cdot T(\frac n2)$ ), and add that to the time it takes to merge both sorted lists ($n$).
### Solving a Recurrence
To solve a recurrence $T(n)$, we want to obtain a function in terms of the input $n$, but independent of the function $T(n)$. 

Essentially, a recurrence, by definition, includes the function on both sides of the equation and to solve it means to derive an equivalent **equation** or valid **inequality** which only references the function on the left hand side.

In terms of **time complexity analysis** and **big-O notation**, we only care about proving that $T(n)$ is greater than some function. This means deriving an inequality from a recurrence is a powerful tool for time complexity analysis.

>The above is a slight oversimplification of what big-O is, you can see the formal definition again [[Lecture 4 - Algorithm Efficiency#Big-O Notation|here]].

Let's see how we can figure out the time complexity of this function by trying to solve this recurrence.

Let $n\in\mathbb N,\;n>2$

Our recurrence equation is
$$
T(n) = T(n-1)+T(n-2)+1
$$

If we substitute the definition for $T(n-1)$ into this equation we get
$$
\begin{split}
T(n) 
&= (T(n-2)+T(n-3)+1)+T(n-2)+1 \\
&= 2\cdot T(n-2) + T(n-3) + 1
\end{split}
$$
Since $T$ is a $\mathbb N\to\mathbb N$ function, it must be that $T(n-3)\geq0$. Which means we can derive the inequality
$$
T(n)>2\cdot T(n-2)
$$

We can now use this inequality to try and solve this recurrence. First, let's go a few levels deeper:
$$
\begin{split}
T(n)
&>2\cdot T(n-2) \\
&>2\cdot (2\cdot T(n-4)) &= 2^2\cdot T(n-4)\\
&>2\cdot (2\cdot T(n-6)) &= 2^3\cdot T(n-6)\\
&\;\;\vdots \\
&>2^k\cdot T(n-2k)
\end{split}
$$
Now we have a nice looking inequality that we can hope to solve. Since we know that $n\in\mathbb N$, we know that it must either be odd or even. We then know that if we keep subtracting 2s we will eventually end up at our base case, allowing us to remove the recursive definition and replace it with one of these.

Let's first look at the case that $n$ is even. Observe that
$$
n-2\Bigl(\frac {n-2}2\Bigr) = 2
$$
Since $n$ is even, $n-2$ must also be even. This means that $\frac{n-2}2\in\mathbb N$ and so we can choose $\frac{n-2}2$ as our value for $k$, so:
$$
\begin{split}
T(n)
&>2^{\frac{n-2}2}\cdot T(2) \\
&>2^{\frac{n-2}2}
\end{split}
$$
By ignoring constants we can find out that, when $n$ is even, $T(n)$ has a big-O of $O(2^n)$.

Now let's consider the case that $n$ is odd. Observe that
$$
n - 2\Big(\frac{n-1}2\Big)=1
$$
Since $n$ is odd, $n-1$ must be even. This means that $\frac{n-1}2\in\mathbb N$, and so we can choose $\frac{n-1}2$ as our value for $k$, so:
$$
\begin{split}
T(n)
&>2^{\frac{n-1}2}\cdot T(1) \\
&>2^{\frac{n-1}2}
\end{split}
$$
By ignoring constants we can find out that, when $n$ is odd, $T(n)$ has a big-O of $O(2^n)$.

Since in both cases the time complexity is found to be $O(2^n)$ we know that this must be the time complexity of our recursive algorithm.