## Vector Spaces in NLP
Continuing from [[Lecture 5 - Vector Spaces]], we will now go over an example of how we can use vector spaces in computer science.

The **vector space model** is an algebraic model for representing **text documents** in **Natural Language Processing (NLP)**

The **basis** is formed by the words in a **corpus**, which means a dataset of words or terms. Each item in this corpus forms a single **basis vector**. For example, the Google News corpus consists of 3million terms, which means the resulting vector space has 3 million axes.

We then represent each document as a vector, where non-zero terms represent that a term appears in the document. Often values are chosen by the **TF-idf** value of a term.

**TF-idf** is determined by the following formula $$
\text {TF-idf}=\frac{\text{No. of times term t appears in document d}}{\text {No. of terms in document d}}\times \frac{\text{No. of documents N}}{\text{No. of documents containing term t}}
$$
You can then us this vector to determine how similar various documents are by using the angle between these vectors, which you can calculate using the dot product.
## Linear Transformation
A linear transformation, also called a linear map, is a type of function $f$ from $\mathbb R^m\to \mathbb R^k$. 

A function $f:\mathbb R^m\to \mathbb R^k$ is a linear map if, and only if, for all $\vec u,\vec v\in\mathbb R^m$ and $s\in\mathbb R$ $$
f(s\vec v) = sf(\vec v)
$$and$$
f(\vec u + \vec v) = f(\vec u) + f(\vec v)
$$
Any linear map $f$ is determined by the images $f(\vec e_1),...,f(\vec e_m)$ of a **standard linear basis** $\vec e_1,...,\vec e_m$.

We can represent this a $k\times m$ matrix of the linear map $\mathbf{A}$ which consists of $m$ columns that are the values of $f(\vec e_1),...,f(\vec e_m)$ in the output dimension $k$.

>For a reminder on what a **standard basis** is look back at [[Lecture 5 - Vector Spaces#Span of Vectors|Span of Vectors]] from last lecture.

This might not immediately make sense, so we need to look at an example. 

Consider the vector space formed by vectors $\vec v\in\mathbb R^2$ and scalars $s\in\mathbb R$. Lets look at the most simple (but a bit pointless) linear transformation possible. $$
f(\vec v)=\vec v
$$which is when we transform a vector by doing nothing to it. While a bit pointless, this does serve to show what a matrix of a linear map represents.

We can quickly verify that this a linear transformation by observing that our two properties hold.

We have

$$
\begin{split}
f(s\vec v) 
& = s\vec v \\
& = sf(\vec v)
\end{split}
$$which shows our first property to be true, and
$$
\begin{split}
f(\vec u + \vec v) 
& = \vec u + \vec v \\
& = f(\vec u) + f(\vec v)
\end{split}
$$which shows our second property to be true.

In this case we have $e_1=(1,0)$ and $e_2=(0,1)$ forming our **standard basis** of our vector space.

We also know that $f(e_1)=(1,0)$ and $f(e_2)=(0,1)$, or in column notation:
$$f(e_1)=
\begin{pmatrix}
1 \\
0
\end{pmatrix}
,\;
f(e_2)=
\begin{pmatrix}
0 \\
1
\end{pmatrix}$$
If we combine these columns into 1 matrix we get $$A=
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
$$which gives us matrix representation of our linear map by$$
f(\vec v)=
A\vec v
$$
We call the matrix $A$ the $2\times 2$ **identity** matrix, as $A\vec v = \vec v$. We can get the $m\times m$ identity matrix by$$
A = 
\begin{pmatrix}
1      & \cdots & 0      \\
\vdots & \ddots & \vdots \\
0      & \cdots & 1
\end{pmatrix}
$$
### Matrix Multiplication By a Vector
Standard matrix multiplication has not been covered anywhere on this university course so far, but has been mentioned when doing [[Lecture 21 - Computer Representations of Relations#Boolean Matrix Multiplication|boolean matrix multiplication]] in the COMP109 module.

If you understand logical (boolean) matrix multiplication, you can understand standard matrix multiplication by substituting the **logical AND** operation with multiplication and substituting the **logical OR** operation with addition.

Otherwise I will go over how to multiply matrices together now.

Matrices are described as being $m\times n$, where $m$ is the number of rows and $n$ is the number of columns. We call the component in the $i$-th row and $j$-th column $c_{ij}$.

When multiplying matrices $A$ and $B$, the formula for each element of the resulting matrix is given by $$
c_{ij} = (a_{i1}\cdot b_{1j}) + (a_{i2}\cdot b_{2j}) + \cdot\cdot\cdot + (a_{in}\cdot b_{nj})
$$What this means in plain English is that we sum the products of the corresponding elements of the $i$-th row of the first vector, with the $j$-th column of the second vector. Giving us the value for 1 **cell** in our resulting matrix.

This means a couple of things.

Firstly it means that the order of multiplication matters. $A\cdot B$ is not the same as $B\cdot A$.

Second, this means that for us to multiply a matrix of size $a\times b$ with a matrix of size $c\times d$ it is only possible if $b=c$, as for the elements in a row of the first matrix to correspond with the elements in a column of the second, the second matrix must have the same number of columns as the first has rows.

So it is possible to multiply a $5\times4$ matrix with a $4\times 3$ matrix but not a $4\times 3$ matrix with a $5\times4$ matrix.

When multiplying matrices together you can look at the **inner** and **outer** dimensions of the matrix. As discussed, the **inner** dimensions must match. The **outer** dimensions, however, tell us the size of the resulting matrix.

So if we have two matrixes $A$ and $B$, where $A$ has a size of $x\times y$ and $B$ has a size of $y\times z$, the result of their matrix multiplication will be another matrix of the size $x\times z$.

The matrix $M$ representing a linear transformation $f: \mathbb R^m\to\mathbb R^k$ is always a $k\times m$ matrix as said above. For every vector $\vec v$ that can be transformed by $f$ it is true that $\vec v \in\mathbb R^m$, meaning that $\vec v$ can be represented as an $m\times 1$ matrix. 

To transform $\vec v$ using $M$ we have to perform the matrix multiplication $M\vec v$. Since we know $M$ is a $k\times m$ matrix and $\vec v$ is a $m\times 1$ matrix, we know the result of computing $M\vec v$ will be a $k\times 1$ matrix, also called a $k$ vector.

I recommend you practice matrix multiplication thoroughly, but I will only run through a single example here.

Let $$
M =
\begin{pmatrix}
2 & 1 \\
3 & 4
\end{pmatrix}
,\;
\vec v = 
\begin{pmatrix}
5 \\
4
\end{pmatrix}
$$
To compute $M\vec v$ we do:$$
\begin{split}
M\vec v 
& = 
\begin{pmatrix}
2 & 1 \\
3 & 4
\end{pmatrix}
\cdot
\begin{pmatrix}
5 \\
4
\end{pmatrix} \\
& = \pmatrix{2\cdot 5 + 1\cdot 4 \\ 3 \cdot 5 + 4\cdot 4} \\
& = \pmatrix{10 + 4 \\15 + 16}\\
& = \pmatrix{14 \\ 31}
\end{split}
$$
## Important Transformations
### Projection
What type of transformation do the following Matrices represent: $$
M_1=
\begin{pmatrix}
1 & 0 \\
0 & 0
\end{pmatrix}
,\;
M_2=
\begin{pmatrix}
0 & 0 \\
0 & 1
\end{pmatrix}
$$
To see what it means we can perform the following multiplications$$
\begin{split}
\begin{pmatrix}
1 & 0 \\
0 & 0
\end{pmatrix}
\pmatrix{x \\ y}
& = \pmatrix{1\cdot x + 0\cdot y \\ 0\cdot x + 0 \cdot y} \\
& = \pmatrix{x \\ 0} \\ \\
\begin{pmatrix}
0 & 0 \\
0 & 1
\end{pmatrix}
\pmatrix{x \\ y}
& = \pmatrix{0\cdot x + 0\cdot y \\ 0\cdot x + 1 \cdot y} \\
& = \pmatrix{0 \\ y} \\ \\
\end{split}
$$Which allows us to see that our vectors are projections onto the $x$-axis and the $y$-axis.
### Scaling
How could we define a matrix that can serve as a way to scale a vector?

If we recall what the identity matrix is, and we recognise that using an identity matrix is essentially like multiplying vector by 1, we can get an idea of how we can scale vectors.

Consider the $2\times 2$ and $m\times m$ identity matrices$$
A_2 = 
\begin{pmatrix}
1      &  0      \\
0      &  1
\end{pmatrix}
,\;
A_m = 
\begin{pmatrix}
1      & \cdots & 0      \\
\vdots & \ddots & \vdots \\
0      & \cdots & 1
\end{pmatrix}
$$
If we wanted to scale a vector uniformly, that means increasing the size of each component by the same amount, we can simply change the 1s in these matrices to the value we want to scale by. The result is a diagonal matrix, where only the diagonals contain non-zero elements.

So if we wanted to scale a 2 component vector by 2 we can do so using the matrix $$
A=\begin{pmatrix}
2      &  0      \\
0      &  2
\end{pmatrix}
$$and if we wanted to scale a 3 component vector by 5 we can do so using the matrix $$
A=\begin{pmatrix}
5 & 0 & 0 \\
0 & 5 & 0 \\
0 & 0 & 5
\end{pmatrix}
$$
If we wanted to scale **non-uniformly** we simply need to provide different values to the different diagonal cells of the matrix. For example, if we wanted to scale the $x$ value of a 2 component vector by 3 and the $y$ value of the same vector by 6 we could use the vector $$
A=\begin{pmatrix}
3      &  0      \\
0      &  6
\end{pmatrix}
$$
The general formula for an $m\times m$ **scaling** matrix is $$
A = 
\begin{pmatrix}
\lambda_1 & \cdots & 0      \\
\vdots    & \ddots & \vdots \\
0         & \cdots & \lambda_m
\end{pmatrix}
$$If $\lambda_1=\cdots=\lambda_m$ then the scaling is **uniform**, otherwise it is **non-uniform**.
### Reflections
If we wanted to **mirror** a vector $\vec v\in\mathbb R^2$ in the $x$ or $y$ axis how would we do that?

First, lets consider how this affects the $x$ or $y$ values of our vector:
- If we want to reflect our vector in the $y$-axis then we want our $x$ value to become the same but negative.
- If we want to reflect our vector in the $x$-axis then we want our $y$ value to become the same but negative.

So now, knowing this and our identity matrix, how can we create a matrix that does either of these reflections. The answer is exchange the 1s for -1s. So we get the vectors $$
A_y=
\begin{pmatrix}
-1 & 0 \\
 0 & 1
\end{pmatrix}
,\;
A_x=
\begin{pmatrix}
1 &  0 \\
0 & -1
\end{pmatrix}
,\;
A_{xy}=
\begin{pmatrix}
-1 &  0 \\
 0 & -1
\end{pmatrix}
,\;
$$where $A_y$ is a reflection in the $y$-axis, $A_x$ is a reflection in the $x$-axis and $A_{xy}$ is a reflection in both axis.

You can also reflect them in the line $y=x$ by moving the ones into different positions in the same column. For example:$$
A_{xy}=
\begin{pmatrix}
 0 & 1 \\
 1 & 0
\end{pmatrix}
,\;
$$
### Rotation
Again consider a vector $\vec v\in\mathbb R^2$, how can we rotate this vector anticlockwise around the origin by an angle $\beta$.

Recall the [[Lecture 4 - Vectors and Operations#Sin and Cos|Sin and Cos]] section of lecture 4 of this module. Here we used a unit circle in order to show a graphical representation of the values of $\sin$ and $\cos$ functions for a given angle. 
![[sin_cos.png]]

Note as well that the matrix representation of a linear map is the same as the collection of images of the **unit vectors** from our standard basis. Now to determine the matrix we need to represent a location, we just need to figure out what our new $x$ and $y$ will be after we rotate the following vectors:$$
\vec e_1=\pmatrix{1 \\ 0},\;\vec e_2=\pmatrix{0\\1}
$$which is the same as working out the endpoints of the vectors below:
![[rotation_e_images.png]]

Since the vectors are of the form $$
\vec e=\pmatrix{x \\ y}
$$we know that the images of the vectors are $$
\vec e_1=\pmatrix{\cos\beta \\ \sin\beta}
,\;
\vec e_2=\pmatrix{-\sin\beta \\ \cos\beta}
$$and so a rotation by the angle $\beta$ can be represented by the matrix$$
A=
\begin{pmatrix}
\cos\beta & -\sin\beta \\
\sin\beta & \cos\beta
\end{pmatrix}
$$
## Composition
The composition of two linear maps, is the single linear map created by applying both linear maps back to back.

The composition of linear maps $\mathbb R^m \to \mathbb R^k \to \mathbb R^n$ given by the matrices $A:\mathbb R^m\to \mathbb R^k$ and $B:\mathbb R^k\to \mathbb R^n$ is represented by the matrix product $BA$.

The order matters here $BA$ is not the same as $AB$.

>Note that applying $BA$ to a vector is the same as applying $A$ and then applying $B$. 
>
>The order can be confusing, as we are used to ordering from left to right, but there is a trick to help you remember. As we know $M\vec v$ is the result of applying a map $M$ to a vector $\vec v$, we can view $BA$ as the result of applying $B$ to $A$.

We can show that the order matters graphically as well.

Consider the two matrices $$
A=
\begin{pmatrix}
1 & 1 \\
0 & 1
\end{pmatrix}
,\;
B=
\begin{pmatrix}
0 & -1 \\
1 &  0
\end{pmatrix}
$$where $A$ represents a horizontal shear, and $B$ represents a rotation by $\frac{\pi}2$.

If we want to rotate and then shear, we apply $A$ to $B$ to get $AB$ $$
\begin{split}
AB 
& = \pmatrix{1 & 1 \\ 0 & 1}\pmatrix{0 & -1 \\ 1 & 0} \\
& = \pmatrix{(1\cdot0+1\cdot 1) & (1\cdot-1+1\cdot0) \\ (0\cdot 0+1\cdot1) & (0\cdot-1+1\cdot0)} \\
& = \pmatrix{1 & -1 \\ 1 & 0}
\end{split}
$$
If we want to shear then rotate, we apply $B$ to $A$ to get $BA$ $$
\begin{split}
BA 
& = \pmatrix{0 & -1 \\ 1 & 0}\pmatrix{1 & 1 \\ 0 & 1} \\
& = \pmatrix{(0\cdot1+-1\cdot0) & (0\cdot1+-1\cdot1) \\ (1\cdot1+0\cdot0) & (1\cdot1+0\cdot1)} \\
& = \pmatrix{0 & -1 \\ 1 & 1}
\end{split}
$$
We can see the effects of performing these transformations on a unit square below:
![[AB_graph.png]]
![[BA_graph.png]]
## Affine Maps
We have covered a lot of different transformation and linear maps/matrix representations, however we have still not dealt with **translations** one of the most simple geometric transformations.

If allow multiplication by a matrix and we then apply a **translation vector** $\vec s$ in order to translate the result, we perform the operation $$f(\vec v) = \vec v + \vec s$$
In this case, we call $f$ an **affine map**.

**Affine maps** are linear only if $\vec s =\vec 0$. This means they can be harder to work with as they don't allow us to use convenient matrix multiplication tricks.

There is a way around this however to turn translations into linear maps.

If we increase the dimension of our space by 1, we can turn a translation into a linear map.

Let $$\vec s = \pmatrix{p \\ q},\; \vec v = \pmatrix{x \\ y}$$Instead of computing $\vec v + \vec s$ we can use $\vec s$ and the $3\times 3$ identity matrix to construct the matrix $$
T=
\begin{pmatrix}
1 & 0 & p \\
0 & 1 & q \\
0 & 0 & 1
\end{pmatrix}
$$
Which allows us to perform the multiplication $$
\begin{split}
T\vec v 
& = 
\begin{pmatrix}
1 & 0 & p \\
0 & 1 & q \\
0 & 0 & 1
\end{pmatrix}
\pmatrix{x \\ y \\ 1} \\
& = \pmatrix{x + p \\ y + q \\ 1}
\end{split}
$$
Which allows us to treat translations as a linear map.
