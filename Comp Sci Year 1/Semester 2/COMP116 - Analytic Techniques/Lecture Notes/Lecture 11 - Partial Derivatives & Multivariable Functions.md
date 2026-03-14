## Multivariable Functions
When attempting to model more complex things (including things in higher dimensions), we start to need more variables than just $x$.

Below you can see a graph given by $z=f(x,y)$
![[mulivariable_graph_example.png]]
You can see that this function, instead of being represented as a (curved) line, is now represented by a (curved) sheet. The $z$ value of this function is gotten through a combination of $x$ and $y$ terms.

Just like with **single-variable** functions $f(x)$, some choice of input will maximise the value of our **multivariable** function. The only difference is that now, we must consider two variables.

When we had just 1 variable, the idea of **critical points** were supported by consider the gradients of lines tangent to the curve at a given point. This analogy does not work now that we have more than 1 variable. We now must consider the **direction** that our function changes in.

So how do we find **critical points** for **multivariable** functions? 

The answer is by using **partial derivatives**.
## Partial Derivatives
A partial derivative is a derivative of a multivariable function, in which you treat all variables except one as a constant.

So for a function $f(x, y)$ the $x$ partial derivative is given by $$
f'_x(x,y)=\frac{\partial f}{\partial x}=\lim_{h\to0}\frac{f(x+h, y) - f(x, y)}{h}
$$but we can just use our standard rules for computing derivatives.

Essentially, we ignore how the change in the other variables affects the change in our function and only focus on how one specific variable affects the change. The choice of variable is denoted by the subscript (in this case $x$) in the $f'_x(x,y)$.

For example consider the function $$
z=f(x, y) = -(3x^2+2y^2+xy)
$$(this the function that generates the example image above)

If we want to want to find values of $x$ and $y$ that maximise $z$ we can do so by:
1. Assuming $y$ is fixed and finding a value of $x$ to maximise $z$ in terms of $y$
2. Assuming $x$ is fixed and finding a value of $y$ to maximise $z$ in terms of $x$
3. Solving these equations as **simultaneous equations**.

For steps 1 and 2, we can use **partial derivatives** to find these values. We can use the power, sum and constant rules to find these partial derivatives. 

Remember that if you are calculating $f'_x(x,y)$ of function $f(x)$ all non-$x$ terms are treated as constants, meaning their derivative is 0. For terms that contain both $x$ and $y$, you must give the derivative in terms of $y$. 

If we compute the $x$ and $y$ partial derivatives of $f(x, y)$ we get:$$
\begin{split}
f'_x(x,y) 
& = -(6x + y) \\ \\
f'_y(x,y)
& = -(4y + x)
\end{split}
$$
>Note that I use $f'_x(x,y)$ to represent the partial derivative of $f(x)$ with respect to $x$, but there is another common notation that is used being $\frac{\partial f}{\partial x}$. 
>
>The $\partial$ symbol is similar to $d$ but specifically represents that a derivative is a **partial** derivative and not a **whole** derivative.

Now to find the **critical points** of $f(x,y)$ we need to find values of $x$ and $y$ where both$$
\begin{split}
f'_x(x,y) 
& = 0 \\ \\
f'_y(x,y)
& = 0
\end{split}
$$
And so we have two equations we can solve simultaneously$$
\begin{split}
-(6x + y) 
& = 0 \\ \\
-(4y + x)
& = 0
\end{split}
$$
Which we can solve either by rearranging and substituting, or by multiplying 1 by a scalar to match coefficients of like terms allowing you to negate the like terms via subtraction.

Both of these methods are commonly taught GCSE methods, so I will not explain them deeper, but I will show how we can solve these two equations. $$
\begin{split}
-(6x + y) & = 0 \\
-6x & = y \\
\\
-(4(-6x) + x) & = 0 \\
-(-23x) & = 0 \\
23x & = 0 \\
x & = 0 \\
\\
y & = -6(0) \\
y & = 0
\end{split}
$$
And so the we know there is a critical point for this function when $x=0$ and $y=0$.
## The Gradient (Nabla)
The gradient function for a multivariable function is a vector that packages the partial derivatives together. We call this function the "nabla" and denote it by $\nabla f$.

So formally:$$
\nabla f(x,y) 
= \begin{bmatrix}
f'_x(x,y) \\
f'_y(x,y)
\end{bmatrix}
$$This can also be expanded to more dimensions.

The $x$ component of this vector represents the rate of change in the $x$ direction of the function, and the $y$ component of this vector represents the rate of change in the $y$ direction of this function.

When packaged into a vector like this, we gain an overall **magnitude** and **direction**:
- The **direction** of the vector is the **direction of the steepest slope**.
- The **magnitude** represents **how steep the steepest slope is.**

When $\nabla f$ is 0, we know that the **surface** of the function is flat. This is what gives us our simultaneous equations for determining the critical points.
## Identifying Types of Critical Points
When we identified the types of critical points for **univariate** (single variable) functions, we used the second derivative. So we need something similar for multivariate functions.

However since we have 2 derivatives of $f(x,y)$ both of which have 2 variables, we actually need to compute both $\nabla f'_x(x,y)$ and $\nabla f'_y(x,y)$. Since both of those are vectors, we can combine them into a single matrix, which we call the **Hessian:**$$
\mathbf{H} =
\begin{bmatrix}
f_{xx} & f_{xy} \\
f_{yx} & f_{yy} 
\end{bmatrix}
$$
There is some new notation here so: 
- $f_{xx}$ means the second partial derivative of $f$ with respect to $x$ both times;
- $f_{xy}$ means the second partial derivative of $f$ with respect to $x$ first and then $y$;
- $f_{yx}$ means the second partial derivative of $f$ with respect to $y$ first and then $x$;
- $f_{yy}$ means the second partial derivative of $f$ with respect to $y$ both times.

[Clairaut's Theorem](https://en.wikipedia.org/wiki/Symmetry_of_second_derivatives) states that as long as a function and it's derivatives are "well behaved", that the order of differentiation does not matter. Practically, for this module, this means that you can treat $f_{xy}$ and $f_{yx}$ as virtually identical.

An easy way to remember the layout is:
- The left column corresponds to $\nabla f'_x(x,y)$
- The right column corresponds to $\nabla f'_y(x,y)$

When a function has 2 variables the **Hessian** is given by a $2\times 2$ matrix. Similarly if we have $n$ variables then the **Hessian** is given by $n\times n$ variables.

When we were working with **univariate** functions, we looked at whether the value of $f''(x)$ was negative, positive or zero.

Now that we are working with **multivariate** functions, we instead use the **determinate** of $\mathbf{H}$ for our comparison.

The **determinant** of a matrix is a single scalar value that can be computed by the matrix. The exact properties of and reason for the determinant of a matrix are not needed for the time being, but you will need to know how to compute it given a $2\times 2$ matrix for the calculus problems in this module.

The formula for the determinant $D$ of a $2\times 2$ matrix $M$ given by $$
M=
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
$$is $$
D= ad - bc
$$
In the case of the **Hessian** since each component is a function $f(x,y)$, the determinant is also a function, $D(x,y)$. This function, will return a single, scalar value and this value is what we use to determine the type of the critical points of $f(x,y)$, along with the value of $f_{xx}$.

So we can determine the type of critical point like so:
- $D(x,y) < 0$ means that the point is a **saddle point** (explained below);
- $D(x, y) > 0$ and $f_{xx}(x,y) > 0$ means that the point is a (local) **minimum**;
- $D(x, y) > 0$ and $f_{xx}(x,y) < 0$ means that the point is a (local) **maximum** 
- $D(x, y) > 0$ and $f_{xx}(x,y) = 0$ is **not possible**. 
- $D(x, y) = 0$ is **inconclusive**, and we will need to computer higher order derivatives. You can understand this with the same intuition expressed in [[Lecture 9 - Critical Points & Second Derivative#Determining Critical Points|last lecture]].

In 3D space:
- A **saddle point** means that the surface curves upwards in one direction and downward in another. It is named this because it looks similar to a saddle.
- A (local) **minimum** is a point which curves upwards in all directions.
- A (local) **maximum** is a point which curves downwards in all directions.

Below you can see some images showing these kinds of critical point. 

The first three are images of the graph of $z=x^2-y^2$ and show a **saddle point** from multiple angles.
![[saddle_3-4.png]]![[saddle_front.png]]![[saddle_side.png]]

The next image shows a **minimum** from the graph of $z=x^2+y^2$.![[surface_minimum.png]]

And this last image shows a **maximum** from the graph of $z=-x^2-y^2$.
![[surface_maximum.png]] 