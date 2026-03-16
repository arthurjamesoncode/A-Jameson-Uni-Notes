## Example Problem
Consider the problem below:

"An arrow is launched at an angle of $60\degree$ landing 400 metres (measured horizontally) from it's starting position.

Suppose we know that the height of the arrow after it has travelled $x$ metres is given by some function $f(x)$.

**Question:** What is the highest height achieved, when (at which $x$ value), and how is the arrow flying when this height is achieved?"

We can see an illustration of roughly what this looks like below.
![[arrow_curve.png]]

We can understand the flight of the arrow as 2 lines, $$
\begin{split}
& (0,0) \to (x,H) \\
& (x,H) \to (400,0)
\end{split}
$$but as it flies in a curve we know this is a rather rough approximation. To make it closer to the curve we can increase the number of the lines we use to approximate it. So we could double this to 4 lines $$
\begin{split}
& (0,0) \to (x_1,f(x_1)) \\
& (x_1, f(x_1)) \to (x_2, H) \\
& (x_2,H) \to (x_3, f(x_3)) \\
& (x_3, f(x_3))\to (400,0)
\end{split}
$$and keep doing this process to with 8, 16, 32 lines etc.

You can see a graphical representation of this below:
![[more_line_approximations.png]]
>Note we haven't been given an $f(x)$ for this problem so you can ignore the $y$-axis of these graphs. This is just a visual aid.

In each of these approximations, the **gradient** of each line is an approximation of the **trajectory** of the arrow. If we kept adding lines to infinity (to create a perfect curve) and knew the gradient of each infinite line, we would know the exact trajectory of the arrow at each infinite point between $x=0$ and $x=400$.

When the arrow is horizontal it is at it's maximum point. This would be when there is a line with a gradient of 0.

So now we know that we need a value of $x$ such that $f(x)= H$ and we know that this will be when the gradient of the line which touches the curve is 0. So if we can come up with a function that gives us the gradient of a line which touches the curve at $x$ we can calculate the $x$ value

If we recall our our formula for the gradient of a line it uses two points. We want the gradient of the line between our point $(x,f(x))$ and the closest possible point to $(x,f(x))$.

So what is the closest possible point to $(x,f(x))$? It is $(x,f(x))$ itself. This causes a problem though since if we try to find our gradient $m$ using our formula we get $$
m=\frac{f(x)-f(x)}{x-x}=\frac00
$$which is undefined.

So how can we get the gradient of the line which touches this point on the curve.

The way to do this is to calculate $$
\frac{f(x+h)-f(x)}{x+h-x}=\frac{f(x+h)-f(x)}{h}
$$for arbitrarily small values of $h$ which approach 0. The way we write "as $h$ gets arbitrarily small" is by writing:$$
\lim_{h\to0}\frac{f(x+h)-f(x)}{h}
$$We can then use this gradient function to figure out at for which value of $x$ the gradient is 0.
## The First Derivative
The function which gives us the gradient of the line tangent to a curve given by $f(x)$ is called the **first derivative** of $f(x)$, which is denoted by $f'(x)$.

We can now say that $$
\frac{dy}{dx}=\frac{df}{dx}=f'(x)=\lim_{h\to0}\frac{f(x+h)-f(x)}{h}
$$
In older physics books the notation for this is $\dot x$.

You can compare this to our definition of instantaneous velocity from [[Lecture 7 - Intro to Calculus]].

Lets take $f(x)=x^2$ as an example, how can we compute the first derivative of $f(x)$?

Well we can do this by trying to simplify the expression given by replacing $f(x)$ with $x^2$ in our formula for the first derivative:$$
\begin{split}
\lim_{h\to0}\frac{f(x+h)-f(x)}{h}
& = \lim_{h\to0}\frac{(x+h)^2-x^2}{h} \\
& = \lim_{h\to0}\frac{x^2 + 2hx +h^2 - x^2}{h} \\
& = \lim_{h\to0}\frac{2hx + h^2}{h} \\
& = \lim_{h\to0}2x + h \\
& = 2x
\end{split}
$$
As long as we have the $$\lim_{h\to0}$$preceding our expression $h\neq0$. $h$ is just a value that is *arbitrarily* close to 0. This means that we can divide by $h$. 

Once the expression in the example above is divided by $h$ there is no longer any need to divide by $h$, which removes the restriction on $h$ not being 0, meaning that we can remove the limit, and we get our **first derivative** function in terms of $x$ alone.

Some functions are still "ill-behaved" at certain points and will not have derivatives for these values. For example:
- $f(x)=\frac1x$ at $x=0$
- $f(x)=\log x$ when $x\leq 0$

The process we just went through is called **finding the derivative via first principles**, and is something that you need to be familiar with for this module. In practice however, we typically find derivative by applying a standard set of rules.
## Rules for Finding First Derivatives
I've written all of these rules in plain English first, followed by their formal notation. I think reading the plain English versions are more confusing than looking at the maths notation, I am simply writing them as an exercise.
### The Constant Rule
The constant rule state that the first derivative of any constant value is 0.

So formally:
$$
f(x)=c\implies f'(x)=0
$$
### The Scalar Product Rule
The scalar product rule states that if $f(x)$ is the product of some function $g(x)$ and a scalar value $s$ then then $f(x)$ is the product of $s$ and the derivative of $g(x)$.

So formally:
$$
f(x)=sg(x)\implies f'(x)=sg'(x)
$$
### The Sum Rule
The sum rule states that if $f(x)$ is the sum of two functions then $f'(x)$ is the sum of their derivatives.

So formally:
$$
f(x)=g(x)+h(x)\implies f'(x)=g'(x)+h'(x)
$$
### The Product Rule
The product rule is more complicated than the sum rule. It states that if $f(x)$ is the product of two functions then $f'(x)$ is the sum of each function multiplied by the derivative of the other function.

So formally:
$$
f(x)=g(x)\cdot h(x) \implies f'(x) = g'(x)\cdot h(x) + g(x)\cdot h'(x)
$$
### The Quotient Rule
The quotient rule is slightly more complicated than the product rule. It states that if $f(x)$ is the result of dividing one function by another function then $f'(x)$ is the difference of the derivative of the numerator multiplied by the denominator and the derivative of the denominator multiplied by the numerator, all divided by the product of the denominator with itself.

So formally:
$$
f(x)=\frac{g(x)}{h(x)} \implies 
f'(x) = \frac{g'(x)\cdot h(x) - g(x)\cdot h'(x)}{h(x)\cdot h(x)}
$$
### The Chain/Composition Rule
The chain rule (or composition rule) states that if $f(x)$ is the composition of 2 functions that $f'(x)$ is the the derivative of the outer function composed with the inner function, multiplied by the derivative of the outer function.

So formally:
$$
f(x)=g(h(x))\implies f'(x)=g'(h(x))\cdot h'(x)
$$
### The Power Rule
The power rule states that if $f(x)$ is of the form $x^t$ where $t\in\mathbb R$ then $f'(x)$ is the product of $t$ and $x^{t-1}$.

So formally:
$$
f(x)=x^t\implies f'(x)=tx^{t-1}
$$
### Logarithm Rule
The logarithm rule states that if $f(x)$ is of the form $\log_n x$ then $f'(x)$ is the reciprocal of the product of $\ln(n)$ and $x$. 

So formally:
$$
f(x)=\log_n (x) \implies f'(x) = \frac{1}{\ln(n) \cdot x}
$$
The above is the general form for differentiating $\log_n(x)$, however often you will see functions of the form $\log(x)$ with no base. In calculus, when working with logs, it is standard to assume that $\log(x)=\ln(x)$. 

>In case you don't know, $\ln (x)$ is the same as $\log_e(x)$ where $e$ is Euler's number. You can read more about $e$ [here](https://en.wikipedia.org/wiki/E_(mathematical_constant). 
>
>I recommend also reading up on [logarithms](https://en.wikipedia.org/wiki/Logarithm), in particular the lists of logarithmic identities, the main ones (like $\log_n(ab)=\log_n(a)+\log_n(b)$) don't take very long to memorise and are pretty useful.

You may see a version of the rule above stated as 
$$
f(x)=\log(x)\implies f'(x)=\frac1x
$$
Or as
$$
f(x)=\ln(x)\implies f'(x)=\frac1x
$$

I personally don't like overloading $\log(x)$ like this, as $\log(x)$ with no base can actually mean $\log_{10}(x)$, $\log_2(x)$ or $\ln(x)$ depending on context which leaves room for confusion. You do need to be aware that this is the way it is used though.
### The Exponential Rule
The exponential rule states that if $f(x)$ is of the form $n^x$ then $f'(x)$ is the product of $\ln(n)$ and $n^x$.

So formally:
$$
f(x)=n^x\implies f'(x)=\ln(n)\cdot n^x
$$
Most commonly you will see this rule when $n=e$. 

$e^x$ is the same as $\exp(x)$. As a result you may see this rule expressed as
$$
f(x)=\exp(x)\implies f'(x)=\exp(x)
$$
### The Trigonometric Rules
The trigonometric rules state that if $f(x)$ is of the form $\sin(x)$ then $f'(x)$ is $\cos(x)$. They also state that if $f(x)$ is $\cos(x)$ then $f'(x)$ is $-\sin (x)$.

So formally:
$$
\begin{split}
& f(x) = \sin(x)\implies f'(x)=\cos(x) \\
& f(x) = \cos(x)\implies f'(x)=-\sin(x)
\end{split}
$$

If you remember that $$
\tan(x) = \frac{\sin(x)}{\cos(x)}
$$You can use a combination of these rules and the quotient rule to find the derivative of $\tan (x)$.
## Examples of Finding Derivatives Using Standard Rules
### Example 1
Consider the function given by 
$$
f(x)=x^2+2x+5
$$
We know, because of the sum rule, that we can find $f'(x)$ by finding the derivative of each individual term and summing them.

So by the power and constant rules we know that $$
f'(x)=2x + 2
$$
### Example 2
Consider the function given by 
$$
f(x)=\tan(x)=\frac{\sin(x)}{\cos(x)}
$$
As stated above, we can use the trigonometric rules and the quotient rule in tandem to find this derivative.
$$
f(x)=\frac{g(x)}{h(x)}
$$
Where $g(x)=\sin (x)$, $h(x)=\cos (x)$ and therefore $g'(x)=\cos(x)$, $h'(x)=-\sin (x)$.

So we know that 
$$
\begin{split}
f'(x)
& = \frac{(\cos(x)\cdot \cos(x))-(-\sin(x)\cdot \sin(x))}{\cos(x)\cdot\cos(x)} \\
& = \frac{(\cos(x)^2)+ (\sin(x))^2}{(\cos (x))^2} \\
& = \frac{1}{(\cos(x))^2}
\end{split}
$$
### Example 3
Consider the function given by
$$
f(x)=(1+5x^2)^3
$$
If we define 
$$
g(x)=x^3,\; h(x)=1+5x^2
$$we can understand $f(x)$ as 
$$
f(x) = g(h(x))
$$letting us use the chain rule (composition rule).

We know by the sum and product rules that
$$
g'(x)=3x^2,\;h'(x)=10x
$$
and so by the chain rule we know that 
$$
\begin{split}
f'(x)
& = 3(1+5x^2)^2(10x) \\
& = 30x(1+5x^2)^2
\end{split}
$$

