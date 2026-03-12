The models we have looked at so far in this module, (Numbers, Polynomials, Vectors, and Matrices) are fairly "fixed". This often is not enough.

We can evaluate polynomials at a given point, but we do not have any tools to analyse how that polynomial changes as the value changes.

Differential Calculus is the way for us to study change.
## Relations
A relation defined on two sets $A$ and $B$ is a new set of ordered pairs **relating** items from $A$ to items from $B$. The first item of each pair is from $A$, and the second is from $B$.

>We have covered relations is some amount of detail in COMP109. Look to [[Lecture 20 - Relations]] and it's successors if you want to learn more. This is a simple recap of what is needed for this module.

The cartesian product of 2 sets $A\times B$, is the set of all possible ordered pairs $(a, b)$ where $a\in A$ and $b\in B$.

We say a relation $R$ is a relation on a set $A\times B$ if $R\in A\times B$.

For example:
Let$$
A=\{1,2\},\;B=\{x,y,z\}
$$Then $$
A\times B=\{(1,x),(2,x),(1,y),(2,y),(1,z),(2,z)\}
$$
So the set $$
C=\{(1,y),(2,x),(2,z)\}
$$is a relation on $A\times B$ but the set $$
D=\{(1,2),(2,1)\}
$$is not.
## Functions
A function is a relationship between 2 sets $f: A\to B$, such that **each element** of $A$ maps to **exactly one** element of $B$.

We can write a function $f: A\to B$ as $f(x)$ where $x\in A$ and $f(x)\in C$.

We call the set $A$ the domain of $f$ and we call set $B$ the codomain of $f$.

There is also a subset of $B$, made up of all the possible outputs of $f(x)$ called the range, which is denoted by $f(A)$.

$x$ is the input or argument and $f(x)$ is the output or image.

>Again we have covered functions in some detail in COMP109. View [[Lecture 15 - Set Cardinality Continued and Intro to Functions]] and its successive lectures for more information.

Lets look at some example formulas and see if they are functions or not:
- $f:\mathbb R \to\mathbb R$ given by $f(x)=x$ is a function as every element of $\mathbb R$ maps to exactly 1 element of $\mathbb R$ using the formula.
- $f:\mathbb R \to \mathbb R$ given by $f(x)=x^2$ is a function as every element of $\mathbb R$ maps to exactly 1 element of $\mathbb R$ using the formula. It is worth noting that in this case multiple different elements can map to the same output, and not all elements of $\mathbb R$ can be mapped to. This makes the function, **non-injective** and **non-surjective** but does not stop it from being a function.
- $f:\mathbb R \to \mathbb Z$ given by $f(x)=x$ is not a function as some elements of $\mathbb R$ can not map to any elements of $\mathbb Z$ using this formula.
- $f$ given by $f(x)=\frac 1x$ is not a function as $\frac 10$ is not defined. If we restrict this function by giving it the domain and co domain of $\mathbb R\setminus \{0\}\to\mathbb Z$. 
### Important Functions
In this course we will consider a number of functions which have the domain $\mathbb R$, (called functions on $\mathbb R$).

We will also consider functions which cannot take $\mathbb R$ as a domain due to some undefined results. For these functions we will consider the **natural domain** of the function, which is the largest subset of $\mathbb R$ for which the formula gives a well defined function. 

So for example, the function $$
f(x)=\frac 1x
$$has a **natural domain** of $\mathbb R\setminus \{0\}$, as it gives us well defined values for all $x\in\mathbb R$ except for $x=0$.

The important functions for this course are:
- **Polynomial** functions - $x$, $x^2 + 3x + 2$, $x^3-9$, etc. 
- **Trigonometric** functions - $\sin\theta$, $\cos \theta$, $\tan\theta$.
- **Logarithmic** and **Exponential** functions - $\log x$, $\ln x$, $\exp x$.
- **Rational** functions - $\frac{f(x)}{g(x)}$
- **Radical** functions - $f(x)=\sqrt{x}$

>Note that $\ln x$ is the natural logarithm function, it is equivalent to $\log_e x$.
>
>Similarly $\exp x$ is the natural exponent function, it is the same as $f(x)=e^x$.

All of these functions have **very** different behaviours:
- Some are "well behaved" for **all** $x\in\mathbb R$;
- Some are "undefined" for **particular** $x\in\mathbb R$
- Some can produce any $f(x)\in\mathbb R$
- Some will only produce $f(x)\in[y,z]$ or some collection of intervals.

### Domains and Ranges of Important Functions

**Polynomial** functions are well behaved for all $x\in\mathbb R$, and all will have $\mathbb R$ as the domain and codomain. However only some with have a **range** of $\mathbb R$.

**Trigonometric** functions are a bit tricky. 

For both $\sin\theta$ and $\cos\theta$, they only produce values in the range $[-1,1]$ but are well defined for all $\theta\in\mathbb R$.

However $\tan\theta$ which is defined as $\frac{\sin\theta}{\cos\theta}$, can produce any $\tan\theta\in\mathbb R$ but is not well defined for whenever $\cos\theta=0$, which occurs when $$
\theta=\frac{\pi}{2}+n\pi,\;\forall n\in\mathbb Z
$$
This means that the domain of of $\tan\theta$ is $$
\mathbb R\setminus\{\frac{\pi}{2}+n\pi,\;\forall n\in\mathbb Z\}
$$and its range is $\mathbb R$.

**Logarithmic** and **exponential** functions are also tricky. We'll only consider $\ln x$ and $\exp x$ in this explanation, but know that the same is true for all $f(x)=\log_n x$ and $f(x)=n^x$ for all $n>1$. I don't know if we will cover these functions when $n<1$ or $n<0$ in this module, if we do, I will try and remember to come back and edit this with link.

$\exp x$ can produce any value in the range $(0,\infty)$, and can take any $x\in\mathbb R$. As we know that $\ln x$ is the inverse of $\exp x$ we know that $\ln x$ can take any value in the range $(0,\infty)$, and can produce any $f(x)\in\mathbb R$.

>Reminder that $(x,y)$ means the interval of real numbers between $x$ and $y$, non inclusive. So $\exp x$ can not be 0 or $\infty$.

**Rational** functions, are defined as the division of 2 functions $$h(x)=\frac{f(x)}{g(x)}$$and are restricted by the values of $x$ when $g(x)=0$.

So the domain of the rational function $h(x)$ is $$\mathbb R \setminus \{x, \text{ where } g(x) = 0\}$$and the range of $h(x)$ is $$\mathbb R \setminus\{asymptotes\}$$
An asymptote is a line which the function approaches, but cannot reach. For example $\frac 1x$ has an asymptote at $x=0$ as we cannot divide by 0.

**Radical** functions are any functions including a root and are a bit too varied to say the domain and codomain for all of them. So instead we'll focus on the functions described by 
$$
f(x) = \sqrt[^k]{x} = x^{\frac1k}
$$
where $k\in\mathbb Z$.

For odd $k$ these functions can produce results for all $f(x)\in \mathbb R$ and take all $x\in\mathbb R$, for even $k$ these functions can only produce results for all $f(x)\in[0,+\infty)$, and can only take $x\in[0,+\infty)$.
## Linear Functions in Calculus
Linear functions are functions that have the form $$
y=f(x)=mx+b
$$
These functions have a **domain** of $\mathbb R$, and a range of $\mathbb R$, and, when graphed, produce a straight line.

The parameter $m$ defines the **gradient** or **slope** of the line, and the parameter $b$ is defines the **y-intercept** or **offset** of the line.

Given any two distinct points, $(x_1,y_1),\;(x_2,y_2)$ there is a **unique** linear function that connects the two.

Given any single point $(x,y)$ and a gradient $m$, there is a **unique** linear function with gradient $m$ that contains the point $(x,y)$.

At a very informal level, **differential calculus** describes the behaviour of th gradient of lines related to functions.
### Computing Linear Functions
To calculate the gradient of the line connecting two points $(x_1,y_1),\;(x_2,y_2)$ we use the formula:$$
m = \frac{y_2-y_1}{x_2-x_1}
$$You can understand this as the difference in $y$ divided by the difference in $x$. So $$
m=\frac{\triangle y}{\triangle x}\text{ or }m=\frac{dy}{dx}
$$might be something you see to describe how we calculate $m$.

To find the $y$ intercept we simply substitute in the values from one of our points and solve the equation for $b$. $$
\begin{split}
x_1(\frac{y_2-y_1}{x_2-x_1}) + b  = y_1 \\ \\
b  = y_1 - x_1(\frac{y_2-y_1}{x_2-x_1})
\end{split}
$$Now knowing both our $m$ and $b$ values, we have the formula for our line.

You can see how this works if we do a specific example. Let's find the line containing both $(5,6)$ and $(4,3)$.

First we calculate $m$:$$
\begin{split}
m 
& = \frac{3-6}{4-5} \\
& = \frac{-3}{-1} \\
& = 3
\end{split}
$$Then using $m$ we substitute in $(5,6)$ to find our $b$, our $y$-intercept.$$
\begin{split}
3(5) + b & = 6 \\
b & = 6 - 15 \\
b & = -9
\end{split}
$$and so now we know that function for the line containing both $(5,6)$ and $(4,3)$ must be $$
y = f(x) = 3x - 9
$$
### Velocity as an Example
Velocity is a good example when it comes to **gradients** of functions.

The formula for the **average** velocity of an object is$$
\text{velocity} = \frac{\triangle s}{\triangle t} 
$$where $s$ is the displacement of the object from a point and $t$ is the time taken.

If we were to plot $s$ and $t$ on a graph, calculating the **average** velocity of the object in the interval $[t_1,t_2]$ is the exact same as finding the gradient of the linear function which contains both $(t_1, s_1)$ and $(t_2,s_2)$.

This only calculates the **average** velocity. For straight lines of a displacement, time graph this is the same as the velocity but if the velocity **changes** over time the line will not be straight and this will no longer be the case.

If we want to calculate **instantaneous velocity**, that is the velocity at any given instance, at some particular point $(t_2,s_2)$ on a curved line, we instead must use this formula:$$
velocity = \lim_{\triangle t\to0}\frac{\triangle s}{\triangle t}
$$where we calculate the velocity by looking at the values of $t$ such that they approach $t_2$. 

**Instantaneous** velocity is a vector. The magnitude of it is the same as the **instantaneous** speed, and the direction is the direction of moment at that **instance** which, in the case of a curve, is a tangent to the curve.