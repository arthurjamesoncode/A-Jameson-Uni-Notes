## Fixed Vectors
The cartesian product of sets $A$ and $B$ is the set of all ordered pairs $(a,b)$ where $a\in A$ and $b\in B$. We say $A_1\times \cdot\cdot\cdot \times A_n=A^n$.

This has been covered in [[Lecture 20 - Relations]] of the COMP109 module.

The cartesian product forms the basis of the **cartesian coordinate system**. 
- For all points $(a,b)$ in **2D** space, $(a,b)\in \mathbb{R}^2$. 
- For all points $(a,b,c)$ in **3D** space, $(a,b,c)\in \mathbb{R}^3$
- And so on for $\mathbb{R}^n$

For all points $A,B\in \mathbb{R}^2$ the fixed vector ${\overrightarrow{AB}}$ is defined as the line that starts at $(x_a, y_a)$ and ends at $(x_b, y_b)$. This can be generalised for $A,B\in \mathbb{R}^n$ as the the line that starts at $(a_1,\cdot\cdot\cdot,a_n)$ and ends at $(b_1,\cdot\cdot\cdot,b_n)$.

We say that 2 fixed vectors $\overrightarrow{AB},\overrightarrow{CD}$ where $A,B,C,D\in\mathbb{R}^2$ are equivalent if and only if
$$
x_b - x_a = x_d - x_c\text{ and } y_b - y_a = y_d - y_c 
$$
Again this can be generalised for $A,B,C,D\in\mathbb{R}^n$ as 
$$
\overrightarrow{AB}=\overrightarrow{CD}\iff b_i - a_i = d_i - c_i\; \forall i\in\mathbb{N},\; i\leq n
$$
## Free Vectors
Since equality for **fixed** vectors is defined as above, this leaves us considering **classes** of **equivalent fixed vectors** which are defined only by the coordinate differences, and not their positions.

We call these classes **free vectors**. These are likely the kind of vectors that you are familiar with from school physics, and can be implemented as tuples in programming languages.

So if we have a **fixed vector** $\overrightarrow{AB}$ where $A,B\in \mathbb{R}^n$ the corresponding **free vector** $\vec v$ is defined as 
$$
\begin{split}
\vec v & = (b_1 - a_1,\cdot\cdot\cdot,b_n-a_n) \\
& = (v_1,...,v_n)
\end{split}
$$
Free vectors are often represented as fixed vectors that start from the origin $(0,0)$ and finish at $(v_1,v_2)$. This is not always convenient. Obviously this example is 2D but you can generalise it to any dimension.

From now on when we say **vector** we mean **free vector** unless we specify **fixed vector**.

The connection between geometric and numeric/algebraic vector representations allow translations of real-life shapes and their movements into computations.

We can actually go further and represent any number of big data representations (words, sentences, variables, objects etc.) in the same way using $n$**-vectors**. 

We can start from any set of numbers $\mathbb{H}$, and an $n$-vector has $n$ components. This is the same as the definition given above.

It is worth noting there are various different notations for vectors. There is tuple notation, which is shown above. As well as square bracket column notation 
$$
\vec v = 
\begin{bmatrix}
v_1 \\
v_2 \\
... \\
v_n
\end{bmatrix}
$$
parentheses column notation  
$$\vec v = 
\begin{pmatrix}
v_1 \\
v_2 \\
... \\
v_n
\end{pmatrix}
$$
and angle bracket notation 
$$
\vec v = \langle v_1,v_2,...,v_n\rangle
$$
There are some other ones, but these are the ones you are most likely to encounter.
## Vector Attributes
### Length
The length (or magnitude) of a vector $\vec v=(v_1,...,v_n)$ is denoted by $|\vec v|$ and is given by 
$$
||\vec v|| = |\vec v| = \sqrt{v_1^2 + \cdot\cdot\cdot + v_n^2}
$$
This formula is derived by the Pythagorean theorem. 

The above is technically the **Euclidean ($L_2$) norm** for the length of a vector. Other norms exist including:
- $L_1$ The Manhattan distance (the sum of the components)
- $L_3$ The Cubic Norm (calculated like the Euclidean norm but replace the squares with cubes)
- $L_\infty$ The max norm (the maximum component)

To make which norm we use clear we may add a subscript so $||v||_2$ denotes the Euclidean norm of this vector.

There are infinite norms for a vector. In general the $L_p$ norm of an $n$-vector is given by
$$
||v||_p=(\sum^n_{i=1}|v_i|^p)^{\frac1p}
$$
### Angle
The angle between vectors $\vec u$ and $\vec v$, denoted by $\angle(\vec u,\vec v)$, is the fraction of the **anti-clockwise** turn from $\vec u$ to $\vec v$, where the angle of a full turn is $2\pi$ radians or $360\degree$. 

>From this point forwards we will discuss angles primarily in **radians**. Although occasionally will still mention degrees.

The **opposite angle** $\angle(\vec v, \vec u)$, is $$
\angle(\vec v, \vec u) = 2\pi - \angle(\vec u,\vec v)
$$
We call vectors parallel (or collinear) if the angle between them is 0 or $\pi$.

The angle between 2 vectors is computed assuming they start from the same point.

We will cover how to calculate the angle between vectors slightly later in this lecture.

Below you can see a depiction of the angle between 2 vectors $\vec u$ and $\vec v$
![[vector_angles.png]]
## Vector Operations
### Multiplication by a Scalar
When we multiply by a constant (or scalar) value $s\in \mathbb{R}$, we create a new vector given by multiplying each component of the vector by $s$. So: $$
s\vec v = (sv_1,\cdot\cdot\cdot,sv_n)
$$
The resulting vector is:
- of the length $|s| \cdot |\vec v|$;
- on the same straight line that contains $\vec v$;
- in the same direction as $\vec v$ if $s > 0$;
- in the opposite direction as $\vec v$ if $s<0$

### Vector Addition
The vector sum of two vectors $\vec u=(u_1,\cdot\cdot\cdot,u_n)$ and $\vec v=(v_1,\cdot\cdot\cdot,v_n)$ is given by summing all the corresponding components with each other. So: $$
\vec u + \vec v = (u_1 + v_1,\cdot\cdot\cdot, u_n + v_n)
$$
Geometrically this can be obtained by placing the vectors head to tail and drawing a new vector from the free tail to the free head. This is called the **parallelogram rule** as when you place both $\vec u$ followed by $\vec v$ and $\vec v$ followed by $\vec u$ it forms a parallelogram. (See below)
![[parallelogram_rule.png]]

You can add multiple vectors at the same time using the same method. (See below)
![[multiple_vector_additions.png]]
### Sin and Cos
Before we cover dot product and cross product we should remind ourselves about the $\sin$ and $\cos$ functions.

You may be familiar from school that $$
\sin(\alpha)=\frac{O}{H} \text{ and } \cos(\alpha) = \frac{A}{H}
$$where $\alpha$ is an **non-right** angle in a **right-angled** triangle, $O$ is the length of the side opposite $\alpha$, $A$ is the length of the side adjacent to $\alpha$ and $H$ is the length of the hypotenuse.

A more consistent way to think about it at university level is to take a unit circle, drawn around the origin of a 2D cartesian coordinate grid, and draw a vector from the origin to any point on on the circle.

If $\alpha$ is the anticlockwise angle between the $x$-axis and the vector then
- $\cos(\alpha)=$ the $x$ coordinate of the head of the vector;
- $\sin(\alpha) =$ the $y$ coordinate of the head of the vector;

You can see how this works below
![[sin_cos.png]]

This uses the formulas we are familiar with from school geometry but allows us to find $\sin(\alpha)$ and $\cos(\alpha)$ for values of $\alpha\in[0,2\pi)$ that we can't fit into a right angled triangle.

>$\alpha\in[0,2\pi)$ means a value within the range $0\to 2\pi$ inclusive of 0 but not inclusive of $2\pi$. 
>
>In general square brackets are used to show that a side of a range is inclusive and parentheses show that a side of a range is not inclusive.

$\sin$ and $\cos$ values are periodic with period $2\pi$. With $\cos$ in particular, the value at $0$ and $2\pi$ is it's maximum value meaning that $\cos(\alpha) = cos(2\pi - \alpha)$. Sin has a similar, but different, property in that $\sin (\alpha) = -\sin(2\pi - \alpha)$.

This module's exams are non-calculator because, as computer scientists, it's vital that we use computers as little as possible (sarcasm). 

This means that you also have to memorize some values of these functions. The values are the $45\degree$ or $\frac\pi4$ intervals up to $360\degree$ or $2\pi$.

It you remember the table below, and remember that $\tan\theta=\frac{\sin\theta}{\cos\theta}$, then you will be set.

| $\theta$       | $\sin\theta$      | $\cos\theta$      | $\tan\theta$ |
| -------------- | ----------------- | ----------------- | ------------ |
| $0$            | $0$               | $1$               | $0$          |
| $\frac\pi4$    | $\frac{\sqrt2}2$  | $\frac{\sqrt2}2$  | $1$          |
| $\frac\pi2$    | $1$               | $0$               | $undefined$  |
| $\frac{3\pi}4$ | $\frac{\sqrt2}2$  | $-\frac{\sqrt2}2$ | -1           |
| $\pi$          | 0                 | -1                | 0            |
| $\frac{5\pi}4$ | $-\frac{\sqrt2}2$ | $-\frac{\sqrt2}2$ | 1            |
| $\frac{3\pi}2$ | -1                | 0                 | $undefined$  |
| $\frac{7\pi}4$ | $-\frac{\sqrt2}2$ | $\frac{\sqrt2}2$  | -1           |
| $2\pi$         | 0                 | 1                 | 0            |
This actually isn't that hard to remember. 

For both $\sin$ and $cos$:
- When $\theta$ is a multiple of $\frac\pi2$ they are always either $1$, $-1$, or $0$
- When $\theta$ is not a multiple of $\frac\pi2$ but is a multiple of $\frac\pi4$ the value is always $\pm\frac{\sqrt2}2$.

Knowing this, all you have to remember is the shapes of these graphs, which you can see below:
![[sin_cos_graph.png]]
From this graph you can see that $$\sin\theta = \cos(\theta+\frac\pi2)$$and that $\sin$ starts at $0$, rises to $1$ before dropping to $-1$ and then finishes at $0$ when $\theta = 2\pi$.

Simply remembering that is sufficient to be able to know the value of $\sin$ and $\cos$ given any $\theta$ which is a multiple of $\frac\pi4$.

>One other identity that is useful to remember is $\cos^2\theta + \sin^2\theta=1$. For this module this is specifically useful for identifying is a vector is a unit vector or not.
### Scalar/Dot Product
The **scalar product** of two vectors $\vec u,\vec v\in\mathbb{R}^n$, also called the **dot product** is given by:$$
\vec u \cdot \vec v = |\vec u| \cdot |\vec v| \cdot \cos(\alpha)
$$where $\alpha$ is the angle from $\vec u$ to $\vec v$.

Another formula, which always give the same result, is $$
\begin{split}
\vec u \cdot \vec v 
& = u_1v_1 + u_2v_2 + \cdot\cdot\cdot + u_nv_n \\
& = \sum^n_{i=1}u_iv_i
\end{split}
$$This second formula is much easier to compute in general, and does not require us to know the angle between two vectors.

There are a few important properties of the **dot product**:
- It is always a **scalar**, meaning a number and not a vector (this is where it gets its name).
- It has a max value of $|\vec u| \cdot |\vec v|$ when the vectors are parallel, meaning that $\alpha = 0$
- It has a minimum value of $-(|\vec u| \cdot |\vec v|)$ when the vectors are antiparallel, meaning that $\alpha=\pi$. Two vectors are antiparallel if they are parallel but have opposite directions.
- It has a minimum absolute value of $0$ when the vectors are orthogonal (also called perpendicular), meaning that $\alpha=\frac{\pi}{2}$.
- It is a **commutative** operation, meaning that the order of the operands does not matter. This is shown below.

To prove that **dot product** is commutative we just need to show that $$\cos(\angle(\vec u,\vec v)) = \cos(\angle(\vec v,\vec u))$$We know that $$
\angle(\vec v,\vec u) = 2\pi - \angle(\vec u,\vec v)
$$Since we know that $$
\cos(\alpha) = cos(2\pi - \alpha)
$$It must be the case that $$
\cos(\angle(\vec u,\vec v)) = \cos(\angle(\vec v,\vec u))
$$As this is true, and as multiplication is a commutative operation, we know that $$
|\vec u| \cdot |\vec v| \cdot \cos(\alpha) = |\vec v| \cdot |\vec u| \cdot \cos(2\pi -\alpha)
$$where $\alpha=\angle(\vec u,\vec v)$. Therefore **dot product** is a commutative operation.

We can also use a combination of both of these formulas to calculate the angle between two vectors as substituting and rearranging shows us the following:$$
\begin{split}
|\vec u| \cdot |\vec v| \cdot \cos(\alpha) & = \vec u \cdot \vec v  \\
|\vec u| \cdot |\vec v| \cdot \cos(\alpha) & = \sum^n_{i=1}u_iv_i  \\
\cos(\alpha) & = \frac{\sum^n_{i=1}u_iv_i }{|\vec u| \cdot |\vec v|} \\
\alpha       & = \cos^{-1}(\frac{\sum^n_{i=1}u_iv_i }{|\vec u| \cdot |\vec v|})
\end{split}
$$
### Vector/Cross Product
The **vector product** of two vectors $\vec u, \vec v\in \mathbb{R}^3$, also called the **cross product**, is given by: $$
\vec u \times \vec v = |\vec u| \cdot |\vec v| \cdot \sin(\alpha)\cdot \vec n
$$where $\alpha$ is the angle from $\vec u$ to $\vec v$ and $\vec n$ is a unit vector perpendicular to the plane containing vectors $\vec u$ and $\vec v$.

There are a few important properties of **cross products**:
- They are always a **vector** orthogonal to both $\vec u$ and $\vec v$. This is because $\vec n$ is by definition orthogonal to both vectors and $|\vec u| \cdot |\vec v| \cdot \sin(\alpha)$ is always just a scalar.
- It has a **maximum magnitude** of $|\vec u|\cdot|\vec v|$ when vectors $\vec u$ and $\vec v$ are perpendicular.
- It has a **minimum magnitude** of $0$ when vectors $\vec u$ and $\vec v$ are parallel.
- It is **anti-commutative**, meaning that the order of operations does matter. $\vec u \times \vec v\neq\vec v \times \vec u$. In fact $\vec u \times \vec v = -\vec v \times \vec u$. This will be shown below.

The proof for **cross product** being anti-commutative is very similar to the proof that **dot product** is commutative. For that reason I will not show the whole thing, as the only real thing of interest is that $$\sin (\alpha) = -\sin(2\pi - \alpha)$$I am sure you can piece together how $\vec u \times \vec v = -\vec v \times \vec u$ follows from this.

>You do not need to be able to compute the cross product of two 3D vectors for this module. You simply should be aware of it's properties and why we use it.
