## Critical Points
A critical point of a function given by $f(x)$ is a point at which the line tangent to the curve given by $y=f(x)$ is completely horizontal, or more formally is equal to $y=c$ where $c$ is some constant value.

If we remember the form of linear functions, we remember that they all fit the form $y=mx+c$ where $m$ is the gradient and $c$ is the $y$-intercept.

So now consider the equation for the line $y=c$. What is the value of $m$ in this equation?

The answer of course is 0, since there is no $x$ term in $y=c$.

Now recall that the **first derivative** $f'(x)$ of a function $f(x)$ gives us the gradient of the line tangent to the curve $y=f(x)$ then to find a **critical point** of $f(x)$ we need to find a value of $x$ such that $f'(x)=0$.

And so the formal definition for the **critical points** of a function are any points $(x, f(x))$ such that $f'(x)=0$.

You can see many examples of critical points in many different functions.

In quadratic functions you can see both **maximum** points and **minimum** points:
![[maximum.png]]
![[minimum.png]]

In **cubic** functions you can also see **inflection points**, where the curve flattens out before continuing in the same direction:
![[inflection.png]]

More complicated functions can have multiple **local** maxima and minima as well:
![[local_criticals.png]]
We say a maximum is **local** if it's the peak of a curve, but there exists values of $x$ for which $f(x)$ is greater than at this point. Local minimums are the same but reversed.

>Technically, when you find a point where $f'(x)=0$, you can only be sure that it is a **local** maximum or minimum. You have to find all of the points where $f'(x)=0$ to deduce which are local/total minimums or maximums.

Although some functions have no critical points at all
![[no_criticals.png]]
## Determining Critical Points
So far we've looked at a number of different types of critical points, and we've determined that functions can have:
- A single **minimum** point;
- A single **maximum** point;
- A mix of **minima** and **maxima**;
- **No** critical points.

We often want to determine:
- How many critical points a function has;
- Where these critical points are;
- Are these points **maxima** or **minima**.

So how do we do this for a given function $f(x)$

Well first we need to determine the candidates. To do this we simply need to find all solutions to the equation $$
f'(x) = 0
$$
The number of solutions also tells us the number of critical points. If no solution exists then we know that there are **no** critical points.

So how do we go about determining whether these are **minimum, maximum, or inflection** points?

Well to do that we need to determine the **second derivative**.
### Second Derivative
The second derivative of a function $f(x)$ is the derivative of $f'(x)$ denoted by $f''(x)$.

The second derivative is another function of $x$, same as $f(x)$ and $f'(x)$. You can continue to find the derivative of these functions to find the third derivative $f'''(x)$ and so one.

We saw notation for the derivative of $f(x)$ that looked like this$$
f'(x) = \frac{dx}{dy}
$$Similarly we can denote the second derivative of $f(x)$ like this$$
f''(x)=\frac{d^2y}{dx^2}
$$
You can continue this notation to higher degrees. So $$
\frac{d^ky}{dx^k}
$$represents the $k^{th}$ derivative.

The second derivative represents **the rate at which the rate of change is changing**. 

If you think of a distance time graph for an object, then the rate of change (first derivative) is the **velocity** of the object. The second derivative is the rate that the velocity is changing, in this case it gives the **acceleration** of an object.

We can use this to determine the type of a critical point:
- If $f'(x)=0$ and $f''(x)<0$ then $(x,f(x))$ is a (possibly local) **maximum**.
- If $f(x)=0$ and $f''(x)>0$ then $(x,f(x))$ is a (possibly local) **minimum**.
- If $f'(x)=0$ and $f''(x)=0$ then $(x,f(x))$ it can be an **inflection point**, or **minimum** or **maximum**.

You can understand this intuitively by thinking in terms of **distance**, **velocity** and **acceleration**. Remember in this model that:
- $x$ is time
- Distance is $f(x)$
- Velocity is $f'(x)$
- Acceleration is $f''(x)$

If we have negative **acceleration** at $x$ and we know that our **velocity** is 0, then we know that directly before $x$ we had **positive** velocity (and so distance was increasing) and directly after $x$ we will have negative velocity (and so distance will start decreasing). This tells us that we have a **maximum**.

Similarly, if we have positive **acceleration** at $x$ and we know that our **velocity** is 0, then we know that directly before $x$ we had **negative** velocity (and so distance was decreasing) and directly after $x$ we will have **positive** velocity (and so distance will start increasing). This tells us that we have a **minimum**.

If, instead, If we have no **acceleration** at $x$ and we know that our **velocity** is 0, then we are stopped and not accelerating. We have no way of knowing whether what we were doing before or after $x$ and therefore it can still be any kind of critical point.

In this case we can often still determine the type of critical point, but this requires us to compute the **third** derivative or higher.
### Example
Let's try and work out an example problem.

Consider the function $f(x)$ given by $$
f(x) = x^4 - 3x^2 + 1
$$
How can we determine the critical points of this function?

Well we first must find $f'(x)$, which we can do by using the product, sum and constant rules from [[Lecture 8 - First Derivative#Rules for Finding First Derivatives|last lecture]]:$$
f'(x)=4x^3-6x
$$
Now we need to find the solutions to this function$$
\begin{split}
4x^3-6x  & = 0 \\
x(4x^2-6) & = 0 \\ \\
x & = 0 \\ \\
4x^2 - 6  & = 0 \\
4x^2 & = 6 \\
x^2 & = \frac32 \\
x & = \pm\sqrt{\frac32}
\end{split}
$$
And so we have three solutions:$$
x=0,\; x = \sqrt{\frac32},\; x = -\sqrt{\frac32} 
$$
Now how can we determine whether the points which correspond to these $x$ values are **maxima**, **minima**, or **inflection points**.

Well now we must find $f''(x)$. Again we can do this by applying the product and sum rules:$$
f''(x)=12x^2-6
$$
Now if we substitute in our solutions to $f'(x)=0$ then we can determine the type of each critical point:$$
\begin{split}
f''(0) 
& =12(0)^2-6 \\ 
& = -6 \\ \\
f''(\sqrt{\frac32}) 
& = 12(\sqrt{\frac32})^2 -6 \\
& = 12(\frac32) - 6 \\
& = 18 - 6 \\
& = 12 \\ \\
f''(-\sqrt{\frac32})
& = 12(-\sqrt{\frac32})^2 -6 \\
& = 12(\frac32) - 6 \\
& = 18 - 6 \\
& = 12 \\
\end{split}
$$
And so:
- since $f''(0)<0$, the critical point at $x=0$ is a **maximum**;
- since $f''(\sqrt{\frac32}) > 0$, the critical point at $x=\sqrt{\frac32}$ is a **minimum**;
- since $f''(-\sqrt{\frac32}) > 0$, the critical point at $x=-\sqrt{\frac32}$ is a **minimum**;

Lets have a look at the graph of $f(x)$ to see how it looks.
![[example_graph.png]]
As you can see, it has 2 minimums and a single local maximum.
### Other Examples
The rest of the lecture looks at some more example functions, and works out the location and type of their critical points.

I think for the purposes of these notes that 1 example explained in depth is enough but I will leave the other functions below. Computing their critical points, and determining the type of them is a useful exercise.

These problems are bit harder, but you should be fine as long as you know the content of this note and the [[Lecture 8 - First Derivative#Rules for Finding First Derivatives|rules]] from last lecture.

**Question 1:** $$
f(x) = 25(\log x)^3-15(\log x)
$$
**Question 2:**$$
B_1(t)=0.06te^{-0.9t}
$$(This function is a simplified model of the blood alcohol concentration of an adult after consuming a single UK unit of alcohol)