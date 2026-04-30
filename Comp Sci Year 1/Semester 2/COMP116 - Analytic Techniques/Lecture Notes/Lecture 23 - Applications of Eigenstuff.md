## The Perron-Frobenius Theorem
Let $A$ be a matrix such that $A\in\mathbb R^{n\times n}$. The growth rate of raising $A$ to a power $k\in\mathbb N$ is controlled by the **dominant eigenvalue** of $A$. Often we also only care about **real** eigenvalues.

>Recall that the **dominant eigenvalue** is the value with the largest absolute value.

There is a good amount of value in being able to be sure that there is a **unique, real, positive eigenvalue**. The **Perron-Frobenius Theorem** gives us conditions sufficient for this to be true.

The Perron Frobenius Theorem states that, if $A\in\mathbb R^{n\times n}$ and $A_{i,j}>0$ for all $1\leq i,j\leq n$, then:
- There is a unique, real, positive eigenvalue $\lambda_{pf}$ associated with it.
- This eigenvalue has an eigenvector (called the **Perron vector**) $\vec v_{pf}$ which contains only real positive components.
- For any initial positive $\vec v_0\neq \vec 0$, the sequence of normalised iterations converges to the perron vector.

This last condition formally states that 
$$
\frac{A^k\cdot\vec v_0}{|A^k\cdot\vec v_0|} \to \vec v_{pf} \text{ when } k\to\infty
$$

There is a generalisation of this theorem to some **non-negative** matrices as well.

>Understanding the proof of this theorem is not necessary. You also do not need to understand which **non-negative** matrices it can be generalised to. But you can read about this [here](https://en.wikipedia.org/wiki/Perron%E2%80%93Frobenius_theorem). 
>
>The gist (from what I read) is that a weaker similar theorem exists for all non-negative matrices, but for a special type of matrix called an *irreducible* matrix, there is a non-trivial generalisation of this theorem.
>
>Importantly, when asked to use the power method (see below) do not worry if given a non-negative matrix instead of a positive one. It should be a matrix for which this method still works.
### The Power Method
The third result of the Perron-Frobenius theorem gives rise to the power method.

The power method is simple:
- Choose an initial, non-zero guess for $\vec v_0$. The simplest guess is to choose a vector made of all 1s.
- Set $i=0$
- Compute $\vec w_{i+1}$ using the formula $\vec w_{i+1}=A\vec v_i$.
- Normalise to find $\vec v_{i+1}$ using the formula $\vec v_{i+1}=\frac{\vec w_{i+1}}{|\vec w_{i+1}|}$
- Set $i=i+1$
- Repeat these computations until $\vec v_i$ stops changing, or $i$ reaches a user defined max value.

>Note the step to normalise $\vec v$. We don't actually care about which norm we take to compute this value. You can read about the type of norms [[Lecture 4 - Vectors and Operations#Length|here]]. 
>
>In practice, it is often best to take the $L_\infty$ norm, since this takes the maximum component of the vector and is comparably easier to compute than taking the other norms.

This method allows us to find approximations to the dominant eigenvectors $c\vec v$ where $c\in\mathbb R$. How about finding their eigenvalues?

Well we can do that by using the **Rayleigh Quotient**.

The **Rayleigh Quotient** is
$$
\frac{\vec v^T A\vec v}{\vec v^T\vec v}=\lambda
$$
where $\lambda$ is the associated eigenvalue for $\vec v$.

>Note that $\vec v^T$ is the **transpose** of $\vec v$. This just means that instead of a **column** vector, it is a **row** vector. It is necessary to use the transpose because of the rules of **matrix multiplication**, and specifically the order in which we can multiply matrices.
>
>If $v$ is a $n$ component **row vector** and $A$ is an $n\times n$ matrix, we can only compute $Av$. If we transpose $v$ to get $v^T$ we can now compute $v^TA$.

Since $\vec v$ is the dominant eigenvector of $A$, $\lambda$ must be the dominant eigenvalue of $A$.

If $A$ has an inverse (is non-singular) then we can also find the smallest eigenvalue of $A^{-1}$, this will be $\frac1\lambda$.

If we were to find the dominant eigenvalue of $A^{-1}$ using this method (we'll label it $\lambda_{-1}$), we can find the smallest eigenvalue of $A$, by doing $\frac1{\lambda_{-1}}$.

>There is a ton of content in this lecture so I am not going to typeset examples of using the power method. You should go over some on paper to make sure you understand this.
## Spectral Graph Theory
As seen in [[Lecture 17 - Intro to Graphs]] from the COMP108 module, graphs can be represented by matrices. This will be touched on again here, but I recommend going to the COMP108 lecture notes if you are struggling.

In particular, any $n\times n$ matrix $A$ is an adjacency matrix for a directed graph $G_A$. $G_A$ will have $n$ nodes and there will be a edge from node $i$ to node $j$ where $A_{i,j}\neq 0$. Notably the rows point to the columns in a directed graph.

You can see an example below from Wikipedia below.
![[graph_and_matrix.png]]

A graph is connected if there is a path between any node to any other node, regardless of the direction of the edges. A **directed** graph is **strongly-connected** if there is a **directed path** between any two nodes.

There are a number of connections between the spectra of these adjacency matrices, and the properties of the graphs they represent. We will be focusing on two properties:
- Number of Edges
- Chromatic Numbers

>You don't need to understand the proofs of these connections, but you do need to know them.
### Number of Edges
The number of edges $|E|$ in a graph $G$ represented by an adjacency matrix $A$ is exactly
$$
|E|=\frac12\sum^n_{k=1}(\lambda_k(G))^2
$$
Where $\lambda_k$ represents the $k^{th}$ eigenvalue of $A$.

Lets take the matrix
$$
A=\pmatrix{0 & 1 & 1 \\ 1 & 0 & 1 \\ 1 & 1 & 0}
$$

The spectrum of this matrix is
$$
\sigma(A) = (2, -1, -1)
$$

And it represents the undirected graph
![[spectrum_edges.drawio.png]]
We can see that this has 3 edges in total.

If we apply our formula for $|E|$ we can see
$$
\begin{split}
|E|
&= \frac12\sum^n_{k=1}(\lambda_k(G))^2 \\
&= \frac12 \cdot (2^2 + (-1)^2 + (-1)^2) \\
&= \frac12(6) \\
&= 3
\end{split}
$$
Which you can observe matches the number of edges of our drawn graph.
### Chromatic Number
The smallest number of colours needed to colour every node of $G$ such that no two linked nodes have the same number is called the **chromatic number** of $G$. 

We can use the eigenvalues of the matrix representation $A$ to determine some bounds for this chromatic number, which we will label $C(G)$. 

In particular
$$
1 + \frac{\lambda_{max}(G)}{|\lambda_{min}(G)|}\leq C(G) \leq \lambda_{max}(G) + 1
$$

Note that we use $\lambda_{max}$ and $\lambda_{min}$ specifically because we are working with their real values, not absolute values. I.e. $\lambda_{min}$ is **most negative*** eigenvalue and $\lambda_{max}$ is the **most positive** eigenvalue.

The slides give an example question on chromatic numbers: "The matrix of an undirected graph having 10 nodes has a dominant eigenvalue $𝜆_{max} = 2.5$ and a smallest eigenvalue $𝜆_{min} = −2$. What are the maximum and the minimum numbers of distinct colours required properly to colour the nodes of this graph (that is, so that no two nodes joined by an edge are given the same colour)?"

This question is poorly worded, and I think Paul E. Dunne might have meant for this to have a different answer to what Olga has put.

I think the question was intended to just ask for the bounds of the chromatic number but the, but the question actually asks two things:
1. What is the maximum number of colours you could use to colour a graph so that every linked node is of a different colour?
2. What is the minimum number of colours you could use to colour a graph so that every linked node is of a different colour?

>I just went back to the lecture recording and I have been proven right. The original solution given was the bounds for the chromatic number.

The answer to the first question is trivial. It is simply the same number of nodes as the graph. In this case 10.

The answer to the second question is (a little) difficult to derive. We can only find the bounds for the chromatic number from the information given. However, since a chromatic number must be an integer, if the lower bounds ceiling is the same as the upper bounds floor then we know the chromatic number.

Let's find the bounds of this number. It must be at least
$$
\begin{split}
1 + \frac{\lambda_{max}(G)}{|\lambda_{min}(G)|} 
&= 1 + \frac{2.5}{2} \\
&= 2.25
\end{split}
$$
and at most
$$
\begin{split}
1 + \lambda_{max}(G)
&= 1 + 2.5 \\
&= 3.5
\end{split}
$$
Since we know that this must be an integer between 2.25 and 3.5, we know that the chromatic number of this graph must be 3.
## PageRank Algorithm
There are a lot of search engines with which we can browse the web. The most popular search engine by far is Google. So why does Google dominate so much?

Generally people evaluate search engines by:
- If their query returned quickly
- If all the results they were looking for could be found
- If results are relevant to the search
- If the order of the results makes sense

According to users, google did best overall job with these categories. 

Other search engines performed reasonably well with respect to the first 3 criteria, but google far outperformed all of them in terms of ordering results. For example Altavista (an old search engine) often returned 70+ pages before the relevant links people would be searching for.

The secret to this is the **PageRank** algorithm which we will now go over.

The problem is simple: "How do we order a selection of pages by how **important** they are?"

Let's consider a selection of pages returned by a search query. These pages contain **links**. We can represent these pages as a **directed graph** where there is an edge from one node/page to another if that page links to it.

Now that we have this representation, we could try and order the pages by **how many links** to each page appear. 

This, while not terrible, still has some problems. Mainly there is no difference between the different sources of the link. A link from "www.google.com" and a link from "www.shadywebsitedontgohere.com" (not a real URL) are treated the same.

So now, we need to also consider the *importance* of the source of the link.

Let's define some notation.

We will use $p_i$ to represent the $i^{th}$ page and $r_i$ to represent it's final rank. Will also use $P_{i\to k}$ to denote the set of pages $p_i$ which link to $p_k$.

Now we can define the rank of the $k^{th}$ page as 
$$
r_k=\sum_{p_i\in P_{i\to k}}r_i
$$
This is better but there is still a problem with this. For every page $p_i$ points to, the full rank is added. This means that pages far down the chain of links will have much higher ranks.

To fix this, we need to evenly distribute the rank of $p_i$ to all the pages $p_k$ that $p_i$ points to. To do this we can divide by the number of outgoing links.

 We will use $P_{j\leftarrow i}$ to denote the set of pages $p_j$ which are linked to by $p_i$.

So now we have this
$$
r_k=\sum_{p_i\in P_{i\to k}}\frac{r_i}{|P_{k\leftarrow i}|}
$$
### Modelling with Matrices
We've seen how we can model a directed graph using matrices. Let's try and model the graph of selected pages using matrices.

We have our set of pages $P$, which are the nodes of our graph
$$
P=\{p_1,p_2,...,p_n\}
$$
We have our set of links $L$, which are the edges of our graph
$$
L=\{(p_i, p_j)\; |\; p_i \text{ links to } p_j \}
$$
And a way to calculate the rank of each page
$$
r_k=\sum_{p_i\in P_{i\to k}}\frac{r_i}{|P_{j\leftarrow i}|}
$$
Our aim is to get an $n$-vector of ranks
$$
\vec r = \pmatrix{r_1\\ r_2\\\vdots\\r_n}
$$
We can define an $n\times n$ transition matrix $W$ with
$$
w_{ij}=\cases{
\begin{split}
0\;\;& \text{if } (p_j,p_i)\notin L \\
\frac1{|P_{k\leftarrow j}|}\;\; & \text{if } (p_j,p_i)\in L
\end{split}
}
$$
Where $P_{k\to j}$ is the set of pages linked to by $p_j$.

For example take the directed graph below
![[pagerank_digraph_example.png]]

This corresponds to the following **transition matrix**:
$$
W=
\begin{pmatrix}
0 & 0 & \frac13 & 1 & 0 \\
\frac12 & 0 & 0 & 0 & 0 \\
\frac12 & 1 & 0 & 0 & 0 \\
0 & 0 & \frac13 & 0 & 1 \\
0 & 0 & \frac13 & 0 & 0
\end{pmatrix}
$$
Notice that all of the columns of this matrix add up to one, we call matrices of this kind **column stochastic** matrices. The rows show the **importance transferred into** the corresponding row-node by the column node. 

Given this matrix we want to be able to derive the rank vector $\vec r$.

The way we do this is by finding a value for $\vec r$ which satisfies
$$
W\cdot \vec r = \vec r
$$
I.e. We are looking for an eigenvector of $W$ for the eigenvalue 1. 

>Exactly why this works is a little complicated and so I will separate that bit from the method itself. Look to the next section for the reasoning.

Now we can find $\vec r$ using the **power method**.

In the given example, we find the vector
$$
\vec r = \pmatrix{1\\\frac12\\1\\\frac23\\\frac13}
$$
And so we can see that page 1 and 3 rank joint highest, and page 5 ranks the lowest. 
### Why look for an eigenvector?
$\vec r$ represents the relative **importance** of each page compared to the others.

Imagine someone who is surfing just this selection of $n$ pages, clicking links at random. We could have a probability vector $\vec p$ with $n$ components which represents the initial probability of being on any given page.

If we compute $W\vec p$, the result will be a new probability distribution which represents the probability of them being on each page after a single, random click. $W^n\vec p$  will be the probability distribution of being on any given page after $n$ clicks.

Now we can view the final scores used for ranking these pages as the probability distribution of being on each page after infinite clicks. Or
$$
\vec r = \lim_{n\to\infty}W^n\vec p
$$

We also need the ranks to be stable, meaning that they won't depend on how long someone is surfing the web. In particular, the probability distribution of being on each page **shouldn't change** after **1 more click**. 

That means we need to find a value of $\vec r$ for which $W\vec r=\vec r$, meaning that $r$ must be an eigenvector of $W$ for the eigenvalue 1.

>Note that here we talk about $\vec r$ being a probability distribution. Normally, this would mean that all of it's components sum to one. However since $\vec r$ is an eigenvector, so is $c\vec r$ where $c\in\mathbb R$. 
>
>There is no guarantee that the components of $c\vec r$ sum to one, and therefore the vector we find may not actually be a probability distribution. Look to the found vector in the example above for an example of this.
>
>However, this doesn't matter since we don't care about the absolute probability, just the relative probability compared to the other components. So the max of any vector $c\vec r$ is still the max ranked page.
>
>You could also make it a unit vector by dividing by the sum of its components. Although, as said, this is pointless since we can just compare components.

This is essentially applying the **power method**, with the assumption that the dominant eigenvalue of $W$ is 1. That means, for this to work, it is crucial that 1 is not only an eigenvalue of $W$, but that it is the dominant eigenvalue of $W$.

But why can we be sure that $W$ has a dominant eigenvalue of 1?

This is because $W$ is a **column stochastic** matrix, meaning all of the columns sum to 1. 

It can be shown that column stochastic matrices always have a **spectral radius** of 1, meaning that their largest eigenvalue is 1, but this may not be unique. You can see some proofs of this [here](https://math.stackexchange.com/questions/40320/proof-that-the-largest-eigenvalue-of-a-stochastic-matrix-is-1).

In the PageRank algorithm, these matrices are forced to have a unique, dominant eigenvalue of 1, by transforming it into the **Google Matrix**. You can read about this [here](https://en.wikipedia.org/wiki/Google_matrix), but it's not really needed for this course. 
