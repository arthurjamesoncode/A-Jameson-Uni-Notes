## Equivalence of Free Vectors
There are a number of equivalence relations on vectors:
- $\vec u \sim \vec v\iff |\vec u| = |\vec v|$
- $\vec u \sim \vec v \iff$ $\vec u$ and $\vec v$ are **colinear**.
- $\alpha\sim \beta \iff \alpha - \beta$ is divisible by $2\pi$.

The set of equivalence classes for these are:
- One class for each number in $\mathbb R$
- One class for each angle in $[0, 2\pi)$ (could represent as the unit circle)
- Again one class for each angle in $[0, 2\pi)$

There is another equivalence relation on vectors.
$$
\vec u \sim \vec v \iff \exists s\in\mathbb R \setminus \{0\}  \text{ such that } \vec u = s\vec v
$$

If we allow $s=0$ this doesn't work since symmetry would not be satisfied, but otherwise this is an equivalence relation.

So what does the set of equivalence classes look like for this relation?

Well if we can create a vector of any length using a scalar, we know that length doesn't matter and therefore we can again just look at the unit circle.

Unlike the examples that are based on angles though, there is an extra class. Since collinearity and angles require a **non-zero** vector, but this relation doesn't. As a result this relations equivalence classes is the union of:
- The unit circle
- The origin
## Vector Operations
When two vectors are added we do this by summing their corresponding components
$$
\vec u + \vec v = (u_0 + v_0,\cdots,u_n + v_n)
$$

The scalar (or dot) product of two vectors is given by the sum of the products of each corresponding component
$$
\vec u \cdot \vec v = \sum_{i=0}^n u_iv_i
$$
this is the same as the products of their magnitudes multiplied by the cosine of the angle between them
$$
\vec u \cdot \vec v = |\vec u| \cdot |\vec v| \cdot \cos\alpha  
$$

What this means is that the dot product measures two things:
- How long the vectors are,
- How aligned they are in terms of angle.

There are a few special cases that are worth remembering:
- If two vectors are **orthogonal/perpendicular** the dot product between them is 0.
- If two vectors are **parallel/colinear** then the dot product between them is the product of their magnitudes.

The angle between vectors can be be found by rearranging the dot product formula to be:
$$
\alpha = \arccos\frac{\vec u\cdot\vec v}{|\vec u|\cdot|\vec v|}
$$

For any vectors $\vec u$ and $\vec v$ the **Cauchy Inequality** states that 
$$
|\vec u \cdot \vec v| \leq |\vec u| \cdot |\vec v| 
$$

This follows from the above since we know that $\cos\alpha$ takes values from 0 and 1.
## Closing Problem
Problem "Compute the pairwise scalar products of $\vec u = (2, 1)$, $\vec v = (1, 2)$ and $\vec w= (−1, 2)$."
$$
\begin{split}
\vec u \cdot \vec v 
&=2\cdot1 + 1\cdot 2 \\
&=4 \\
\\
\vec u \cdot \vec w
&=2\cdot -1 + 1\cdot 2 \\
&=0 \\
\\
\vec v \cdot \vec w 
&=1\cdot -1 +2\cdot 2 \\
&=3
\end{split}
$$
