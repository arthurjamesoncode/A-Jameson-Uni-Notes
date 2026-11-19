## Probability
Machine Learning is about the measuring of and reasoning about probability distributions. This lecture will cover the foundations of what is needed to understand the probability foundations.
### Random Variables
Random variables are functions which assign numerical values to the outcomes of a probability space.

For a detailed definition of what a probability space is look to [[Lecture 3 - Probabilities, Exclusivity, & Independence]] from the COMP229 module.

COMP229 also goes into more detail about random variables and I have already made notes for that module so I will just link to them with [[Lecture 6 - Discrete Random Variables]]. That lecture specifically covers discrete random variables, but they are easily generalised to continuous distributions.
### Marginal, Joint, and Conditional Probability
**Marginal Probability** is the the probability $P(A)$ of an event $A$ occurring. It is also called **unconditional probability**.

**Joint Probability** is the probability $P(A\cap B)$ of events $A$ and $B$ both occurring.

**Conditional Probability** is the probability $P(A|B)$ of an event $A$ occurring given another event $B$.

We can express conditional probability as a result of marginal and joint probability
$$
P(A|B) = \frac{P(A\cap B)}{P(B)}
$$

We can also create a joint probability distribution for multiple variables
![[joint_distribution.png]]
Each box represents the probability of both things occurring, for example $P(\text{A}\cap\text{Low})=0.07$.

Conditional probabilities can be easily computed by dividing the individual squares by the sums of the columns or rows.
### Independence and Conditional Independence
**The Chain Rule**, or the general product rule, allows the computing of any member of a joint distribution using only conditional probabilities.

It has a recursive definition given below
$$
P(A_n, ..., A_1) = P(A_n|A_{n-1},...,A_1)\cdot P(A_{n-1},...,A_i)
$$

We say that two events $A$ and $B$ are independent if, and only if,
$$
P(A|B) = P(A)
$$
We say that two events $A$ and $B$ are conditionally independent given $C$ if, and only if,
$$
P(A|B\cap C)=P(A|C)
$$
Conditional independence is a far more common property than true independence.
### Querying Probability Distributions
Probability queries ask "Given some observed evidence $E$, what is the probability distribution over the set of query variables $Y$".

These queries have two components:
- Evidence: A subset of variables $E$ and their instantiation $e$.
- Query Variables: A subset $Y$ of random variables.

The task is to determine the probabilities
$$
P(Y|E=e)
$$
While conditioned on $E=e$, we can consider the probabilities marginal over $Y$ while working with the distribution we obtain by conditioning on $e$.

We estimate the probabilities using the formula above
$$
P(Y=y_i|E=e)=\frac{P(Y=y_i,E=e)}{P(E=e)}
$$

A **MAP (Maximum A Posteriori ) query** is a query that asks what the most likely state of the variables is.

Let $x$ be in the range $[a, b]$ and $f$ be a function over $[a,b]$.
- $\max(f(x))$ represents the maximum value of $f(x)$ in the range.
- $\text{argmax}(f(x))$ represents the value of $x$ at which the maximum of $f(x)$ is obtained.

For example $\max(\sin(x))=1$, and $\text{argmax}(\sin(x))=\{y|y-\frac\pi4=0\mod 2\pi\}$.

When perform a MAP query we are are essentially using the argmax function
$$
MAP(W | e) = \text{argmax}(P(w,e))
$$
$W$ is the set of non-evidence variables, so the set of all variables minus $E$. We then want to get the most likely outcome given $E$.

Say we have a medical diagnosis problem with two variables 
- Diseases $D$
- Symptoms $S$

Depending on the input, the most likely probability would be different:
- $MAP(D,S)$ would be asking what the most likely combination of disease and symptom is.
- $MAP(S)$ would be asking what the most likely symptom is
- $MAP(D|S=s)$ would be asking what the most likely disease is given the evidence of a having the symptom $S$.

These can be computed given the joint probability distribution.
## Linear Algebra
Linear Algebra is the foundation of machine learning. As such it is important to understand the key concepts and definitions in linear algebra.
## Scalars and Vectors
A scalar is a single number. It is represented in a lower case italic e.g. $x$. 

You can have scalars from the real numbers or natural numbers. For example $x\in\mathbb R$ could be the length of a line, while $n\in\mathbb N$ could be the number of units.

Vectors $\vec v\in\mathbb R^n$ are an array of $n$ numbers. They are arranged in order, and each value is identified by an index. You can also have $\vec v \in \mathbb N$ or other sets of numbers.

Vectors are denoted either in lower case bold or with an arrow across the top. We can also denote them as lists or columns of numbers.
$$
\vec v =\mathbf v
$$

Generally, when working with matrices we consider vectors to be columns, and we consider the **transpose** of a vector to be the row version of it.
$$
\vec v = \begin{bmatrix}v_1\\ \vdots\\ v_n\end{bmatrix}\implies \vec v^T[v_1,\cdots,v_n]
$$
This is necessary to consider for matrix multiplication which requires the number of columns in the first matrix to match the number of rows in the second.
### Matrices
A matrix is a generalisation of vectors which allow for multiple rows/columns.

Matrices $A\in \mathbb R^{n\times m}$ are 2D arrays of numbers with $n$ rows and $m$ columns. They are denoted by bold letters and each element of a matrix is identified by 2 indices, the first being the row and the second being the column.

So for a matrix with $n$ rows and $m$ columns it would be written like
$$
\mathbf A=\begin{bmatrix}\mathbf A_{1,1} & \cdots & \mathbf A_{1,m} \\ \vdots & \ddots & \vdots \\ \mathbf A_{n,1} & \cdots & A_{n,m} \end{bmatrix}
$$

The transpose of a matrix $\mathbf A$ is denoted by $\mathbf A^T$ and is the result of swapping the rows and columns of the matrix (the same as a reflection along the top left diagonal).
$$
\mathbf A^T=\begin{bmatrix}\mathbf A_{1,1} & \cdots & \mathbf A_{n,1} \\ \vdots & \ddots & \vdots \\ \mathbf A_{1,m} & \cdots & A_{n,m} \end{bmatrix}
$$
### Tensors
Tensors are an extension of matrices to $n$ dimensions. These cannot be laid out in a regular grid for $n>2$ and cannot be visualised at all for $n>3$.

They are also denoted with a bold typeface, and each element is denoted by $n$ different indices. 

For example for a 4th dimensional tensor element $(i,j,k,l)$ is denoted by $A_{i,j,k,l}$.

## Linear Transformation
If we apply a square matrix $\mathbf A$ to a vector $\vec v$, the matrix applies a **linear transformation** to the vector
$$
\mathbf {A}\vec v = \vec b
$$
It is a requirement of matrix multiplication that $\mathbf{A}\in\mathbb R^{n\times n}$ and $\vec v,\vec b\in\mathbb R^n$.

Linear transformations were covered in a lot of detail in [[Lecture 6 - Linear Transformations]] of 116, so if you need a refresher go to there.
### Identity Matrix & Inverse Matrices
The identity matrix is the $n\times n$ matrix which doesn't change an $n$ vector it is applied to. It has the format
$$
A = 
\begin{pmatrix}
1      & \cdots & 0      \\
\vdots & \ddots & \vdots \\
0      & \cdots & 1
\end{pmatrix}
$$
where the diagonal is 1s and the rest of the cells are 0s.

If
$$
\mathbf A\vec v = \vec b
$$
then there may be a matrix $A^{-1}$ such that 
$$
\vec v = \mathbf {A^{-1}}\vec b
$$

This is called the inverse matrix. Exactly how to find the inverse matrix, if it exists, for 2 by 2 matrices is covered in [[Lecture 21 - Determinants & Intro to Spectral Theory]] from COMP116. 
## Norms
Norms are ways of measuring the **magnitude** of a vector. They are functions which map vectors to non-negative scalar values.

They are any function $f$ which satisfy the following 3 axioms:
- $f(\vec x)=0\implies \vec x=\vec 0$
- $f(x+y)\leq f(x)+f(y)$
- $\forall s\in\mathbb R,\; f(sx)=|s|f(x)$

The most common are:
- $L^1$ norm: Manhattan Distance
- $L^2$ norm: Euclidean Distance
- $L^\infty$ norm: Max component of the vector

We denote the $L^p$ norm of $\vec v$ with
$$
||\vec v||_p
$$
If written with no subscript it is assumed to be the Euclidean norm.

The general formula for $L^p$ norm of $\vec v$ is
$$
||\vec v||_p= (\sum_i|x_i|^p)^{\frac1p}
$$

In particular, norms are used in machine learning to identify the difference between things that we recognise as vectors, which is basically everything including:
- Images
- Natural Language Documents
- Feature Lists
- etc.
## Scientific Python
This course uses python to create and train AI models. To do this we need to have a strong understanding of what packages are used an how to use them. This portion serves as an overview of the most fundamental scientific python package.

`numpy` is a fundamental package for scientific computing. It has an object for $n$ dimensional arrays and has many capabilities for linear algebra, etc.

It is also a building block of other libraries such as `scipy`.
### Basics
It is imported with
```python
import numpy as np
```

You can create a `numpy` array with
```python
A = np.array([[1,2,3],[4,5,6]])
```

If we print this array it gives the output
```
[[1 2 3]
 [4 5 6]]
```

By default the array infers a specific data type (all elements must be of the same data type) but you can force an array to use a certain data type by passing it in an as optional argument
```python
Af = np.array([1,2,3], float)
```

To take a certain slice of the array, you use standard python syntax of
```python
array[start:stop:step]
```

However unlike python lists, you can access separate axes inside the same square brackets using commas. For example:
```python
array[rowStart:rowStop:rowStep, colStart:colStop:colStep]
```
Avoiding adding multiple brackets as you would do for a standard python list.

`np.arrange(start, stop, step)` generates evenly spaced values within a the interval $[start, stop)$ based on the specified step size.

```python
np.arrange(0,1,0.2)
#array([0, 0.2, 0.4, 0.6, 0.8])
```

`np.linspace(start, stop, num)` generates a specific number of evenly spaced numbers over a specific interval. This like arrange but the step is determined by the length of the interval and the number of points.

`np.zeros(shape)` creates an array of the shape specified in the tuple shape filled with 0s. Shape is a tuple of the format `(row_length, column_length, ...)` dictating the number of axes and shape of them.

There is also `np.ones` which does the same but fills with ones.

`np.diag(array)` does two things:
- Creates a square 2D array with the specified diagonal values if given a 1D array
- Extracts the diagonal values if given a 1D array
It can also take a standard python list instead of a 1D array and have the same effect.

`np.reshape(shape)` changes the shape of an array without changing the data. The sum of all the elements of `shape` must equal the size (total number of elements) of the array.

`np.resize(size)` changes the size of an array. This removes final values or appends 0s depending on the new size.

`np.random.random(size)` creates an array with size `size` and fills it with random floating point numbers drawn from a continuous uniform distribution over $[0,1]$.

`np.random.normal(loc, scale, size)` creates an array of size `size` and fills it with random values taken from a normal distribution where `loc` is the mean and `scale` is the standard deviation.

>You can do random sampling with many more distributions. To see the full list and details you can look [here](https://numpy.org/doc/stable/reference/random/generated/numpy.random.normal.html).

`np.savetxt(filename, array)` saves the 1D or 2D array in `array` out to a plain text file with filename of `filename`. This only works with 1D and 2D arrays since these are the only ones really visualisable in text. For higher dimensions you would typically save them as binary files, since there's no benefit to seeing them in text.

`np.loadtxt(filename)` returns the array loaded from `filename`.
## Array Properties, Attributes, and Operations
Arrays in `numpy` are mutable and passed by reference. That means you can reassign values of arrays, but that if you assign an array to a new variable mutating the new variable will mutate both.

```python
A = np.zeros((2,2))
# array([[0,0]
#         0,0])
C = A
C[0,0] = 1

print A
# [[1, 0]
#  [0, 0]]
```

Attributes:
- `A.shape` returns the shape tuple of `A`.
- `A.ndim` returns the number of dimensions of `A`
- `A.size` returns the total number of elements in `A`
- `A.T` returns the transpose of `A`
- `A.dtype` returns the data type of the elements in `A`

We can do some basic operations of arrays. For arrays of the same shape, these are done **elementwise**, meaning that a new array is generated where each position is the result of applying that operation to the two corresponding elements.

**Importantly** `A*B` is not the matrix multiplication of the matrices, but the element wise multiplication of them.

The standard operations possible are:
- `+`
- `-`
- `*`
- `/`
- `**`
There assignment variation such as `+=` are also valid.
### Array Broadcasting
When operating on arrays of different shapes, `numpy` still performs element wise operations but does so by stretching the smaller array to fit them.

`numpy` compares shapes to see if the shapes of the arrays are compatible. This is in two steps. First:
- If one shape has less dimensions than the other shape, prepend that shape with 1s until it has the same number of dimensions. So if the shapes are `(4,3,2)` and `(2)` then the second shape would become `(1,1,2)`.
- Check each corresponding dimension to see if they are compatible.

The dimensions are compatible if:
- They are of equal size
- One of them is of size 1

Below you can see this in action. These are equivalent operations because of array broadcasting.  
![[array_broadcasting.png]]

- The first one shows an array of shape `(4,3)` being summed to an array of shape `(4,3)`
- The second one shows an array of shape `(4,3)` being summed to an array of shape `(1, 3)`
- The third one shows an array of shape `(4,1)` being summed to an array of shape `(4,1)`

Note that the first one is only equivalent to the others because the rows of the first array are identical, and the columns of the second array are identical. If the data was different they would not be the same.

Array broadcasting allows multiplication by scalars, or arrays of smaller dimensions.
### Vector and Matrix Operations
`numpy` has a number of functions for operating on vectors and matrices.

For all examples, assume `u` and `v` to both be vectors of `n` dimensions

`np.inner(u, v)` and `np.dot(u, v)` computes the inner product or dot product of the vectors `u` and `v`.

If instead passed matrices instead of vectors `np.dot(A, B)` computes the standard matrix multiplication $AB$ while `np.inner(A, B)` computes $AB^T$. 

`np.outer(u, v)` computes the outer product of the vectors `u` and `v`. This is the matrix $A\in\mathbb R^{n\times n}$ where $A_{i,j}=u_i*v_j$.
### Looping Over Arrays
You can loop over an $n$ dimensional array with $n$ nested for loops.
```python
for axis0 in A:
	for axis1 in axis0:
		...
```

If you want to loop over all the elements in an array without regard for axis you can do so with
```python
for elements in A.flat
```
### Linear Algebra
`numpy` has a number of linear algebra functions. To use these you need to use
```python
import numpy.linalg
```

I'm just going to paste a photo since these are all self explanatory is you know the concepts and too long to write about if you don't.

![[linalg.png]]

