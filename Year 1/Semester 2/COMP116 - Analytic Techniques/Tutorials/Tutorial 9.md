## Question 1
**Question:** The characteristic polynomial of a matrix is found to be
$$
(x-2)(x-3)^3(x^2-1)
$$
**Answer:** $6\times 6$. The matrix is square and the dimensions are the same as the degree of the polynomial.
## Question 2
**Question:** An $n \times n$ matrix $A$ is such that it has an $n$-vector $\vec{x}$ which is an eigenvector, and $A \cdot \vec{x} = 0$. Which of the following statements most accurately describes this behaviour?

- **A.** The matrix $A$ is singular.
- **B.** The vector $\vec{x}$ is 0.
- **C.** All eigenvalues of $A$ belong to the Real numbers.
- **D.** The matrix $A$ has a dominant eigenvalue.
- **E.** The matrix $A$ has only the eigenvalue 0 which occurs with multiplicity $n$.

**Answer:** 
The defining property of an eigenvector $\vec v_{\lambda}$ of $A$ is that $A\cdot \vec v_{\lambda} = \lambda\cdot\vec v_{\lambda}$. Since $\vec x$ is not $\vec 0$, this must mean that $\lambda=0$ and $\vec x = \vec v_0$. Making 0, an eigenvalue of $A$.

From our characteristic polynomial we can see
$$
\begin{split}
\det(A-0\cdot I) &= 0 \\
\det(A) & = 0
\end{split}
$$

Any matrix with a determinant of 0 is singular. Therefore it must be true that $A$ is singular.
## Question 3
**Question:** Using the Power Method with Scaling and Rayleigh Coefficients find the dominant eigenvalue of the $2 \times 2$ matrix below:
$$A=\begin{pmatrix} 3 & 2 \\ 0 & 2 \end{pmatrix}$$
Give your answer correct to two decimal places.

**Answer:** To do this we first choose an initial guess for a 2-vector. We will pick $\vec v_0=(1, 1)$.

Now we can use this to compute $\vec w_{i+1}$
$$
\begin{split}
\vec w_1 
&= A\vec v_0 \\
&=\begin{pmatrix} 3 & 2 \\ 0 & 2 \end{pmatrix}\pmatrix{1 \\ 1} \\
&=\pmatrix{5 \\ 2}
\end{split}
$$
Which we can normalise to get $v_1$. We can use any norm ($L_1, L_2, ..., L_\infty$) to normalise. As such we will use $L_\infty$ since this takes the maximum element and is the simplest to compute.
$$
\begin{split}
\vec v_1 
&= \frac{w_1}{|w_1|} \\
&=\frac15\pmatrix{5 \\ 2} \\
&=\pmatrix{1 \\ \frac25}
\end{split}
$$
We can then repeat these steps
$$
\begin{split}
\vec w_2
&= A\vec v_1 \\
&= \pmatrix{ 3 & 2 \\ 0 & 2}\pmatrix{1 \\ \frac25} \\
&= \pmatrix{3.8 \\ 0.8} \\
\\
v_2
&= \frac{w_2}{|w_2|} \\
&= \frac{1}{3.8}\pmatrix{3.8\\0.8} \\
&= \pmatrix{1\\\frac4{19}}
\end{split}
$$
Normally you would keep going until some user defined number of iterations or the output stops changing. I have a bit of a life, and so I am not doing that here. We will now just treat this iteration as a good approximation.

Now we have a decent approximation of this vector, we can calculate our eigenvalue using this vector like so
**Multiply $A \vec{x}_2$:**

$$\vec{y}_3 = \begin{pmatrix} 3 & 2 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} 1 \\ 0.2105 \end{pmatrix} \approx \begin{pmatrix} 3.421 \\ 0.421 \end{pmatrix}$$

**Calculate Rayleigh Coefficient ($\lambda_3$):**
$$\lambda_3 = \frac{\vec{x}_2^T \vec{y}_3}{\vec{x}_2^T \vec{x}_2} = \frac{(1 \cdot 3.421) + (0.2105 \cdot 0.421)}{1^2 + 0.2105^2} \approx \frac{3.5096}{1.0443} \approx \mathbf{3.3607}$$
And so we can give the answer $3.36$.
## Question 4
**Question:** Which of the following is an eigenvector of the matrix below for the eigenvalue 1?
$$\begin{pmatrix} 0.125 & 0.5 & 0.25 \\ 0.5 & 0 & 0.75 \\ 0.375 & 0.5 & 0 \end{pmatrix}$$
- A. $(2, 2.5, 2)$
- B. $(2, -1, -1)$
- C. $(2, -4, 2)$
- D. $(1, -2, 4)$
- E. $(2, 1, -2)$

**Answer:** Easiest way to do this is to just multiply all these vectors by the matrix and see if it holds. 

Since the eigenvalue is 1, we need the resulting vector to be identical, as such we can stop calculating if any element is not the same.

**A) YES**
$$
\begin{split}
\begin{pmatrix} 
0.125 & 0.5 & 0.25 \\ 
0.5 & 0 & 0.75 \\ 
0.375 & 0.5 & 0 
\end{pmatrix}
\pmatrix{2 \\ 2.5 \\ 2}
&=\pmatrix{\frac14+\frac54+\frac12 \\ 1 + 0 + 1.5 \\ \frac68 + \frac54 + 0 \\ } \\
&=\pmatrix{2\\ 2.5 \\ 2 } \\
\end{split}
$$
Since A is yes, we don't need to calculate any other options.
## Question 5

**Question:** A 5 node (directed) graph is described by the adjacency matrix $G$ with

$$G = \begin{pmatrix} 0 & 1 & 0 & 1 & 1 \\ 1 & 0 & 1 & 0 & 0 \\ 0 & 1 & 0 & 1 & 1 \\ 1 & 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 0 & 0 \end{pmatrix}$$

Which of the following is an eigenvalue of $G$?

- A. 0
- B. $i$
- C. 5
- D. 10
- E. 25

**Answer:** A - The determinant is 0 and so 0 must be an eigenvalue of A.
## Question 6

**Question:** Consider the two 5 node graphs $G$ and $H$ with adjacency matrices:

$$G = \begin{pmatrix} 0 & 1 & 1 & 1 & 1 \\ 1 & 0 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 & 0 \end{pmatrix}, H = \begin{pmatrix} 0 & 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 & 0 \\ 0 & 1 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \end{pmatrix}$$

- A. Draw the graphs.
- B. Use Wolfram Alpha tool to find the spectra $\sigma(G)$ and $\sigma(H)$.
- C. What can be concluded about using graph spectra as a method of describing graphs?

## Question 7

**Question:** Compare the slides below with the Lecture 24 slides. How many factual inconsistencies can you spot?

### Exploiting Spectra
- Given an $H \times W$ image $P$, let $M$ be the corresponding matrix.
- Notice that, unlike our previous examples, $M$ will typically not be a square matrix.
- This is unimportant.
- **Key result:** "any $H \times W$ matrix, $M$, can be described as the product of three matrices — $U, S, V$ with $U$ an $H \times W$ matrix, $S$ a $W \times W$ matrix, and $V$ a $W \times W$ matrix: $M = U \cdot S \cdot V$"

### So what are $U, S, V$?
- Given $M$ form the matrices: $M \cdot M^T$ and $M^T \cdot M$.
- These are square matrices and they are symmetric.
- All of their eigenvalues are Real numbers.
- Their spectra are "identical": $(\lambda_1, \lambda_2, \dots, \lambda_i, \dots, \lambda_n)$
- $S: s_{ij} = 0$ if $i \neq j$; $s_{ii} = \sqrt{\lambda_i}$.
- $U$: $k$-th column an eigenvector of $M \cdot M^T$ with $\lambda_k$.
- $V$: $k$-th row an eigenvector of $M^T \cdot M$ with $\lambda_k$.

### The Three Matrices
- We appear to be using more space.
- Originally we had $HW$ integers.
- Now we have: $HW + W^2 + W^2 = W \cdot (H + 2W)$.
- The "trick" is what we can do with the matrix $S$.
- If we could "throw away" some rows and columns in $S$ then we would also have to "throw away" columns in $U$ and rows in $V$: otherwise the matrix product would be ill-formed.
- If we keep only $k$ rows and columns: $S_k$.
- We end up with space: $k \cdot (H + k + W) \ll HW$.