## Method Of Exhaustion
Consider the problem of trying to find the shaded area on the graph below.

![[shaded_graph.png]]

We can approximate this by using rectangles. You can see this on the graph below. The blue rectangles are an area that is greater than the area we want to find, and the orange rectangles are an area that is less than the area we want to find.

![[rect_approx_1.png]]

If we decrease the size of the base of our rectangles and use this to fit more in we can find a better approximation.

![[rect_approx_2.png]]

Observe that the area up to the blue rectangles is still greater than the area we want to find, and the area of the orange rectangles is still less than the area we want to find.

This method of approximating the area under a graph is called the **"Method of Exhaustion"** and it dates back to ancient Greek mathematicians. 

This method can overestimate (blue rectangles) and sometimes underestimate (orange rectangles). Notice that as we choose smaller bases of rectangles the difference between the the overestimation and the underestimation become smaller.

Before we used smaller and smaller differences in $x$ to determine a function which gives the gradient of the line tangent to a curve at a given point. Let's see if we can do something similar to find a function which can give us the area under a graph between 2 points.
## Area as a Function
Suppose we are looking at an area between 
$$
x=a;\; x=b,\; a<b
$$
We can fit $N$ rectangles between $a$ and $b$ where
$$
N=\frac{b-a}{h}
$$
In these examples we consider $N$ a natural number which means that $h$ divides $b-a$ neatly.

If we just look at the area $A$ under the graph from $x$ to $x+h$, we can recognise some things:
- $A$ is greater than $hf(x)$, (this is the same as the **orange** rectangle)
- $A$ is less than $hf(x+h)$, (this is the same as the **blue** rectangle)

If we define a function $A(h, a, b)$ as the the area under a graph $f(x)$ between $x=a$ and $x=b$ we know that $A(h, a, b)$ is between $L(h, a, b)$ and $U(h, a, b)$ where 
$$
L(h, a, b) = \sum_{k=0}^{N-1}hf(a+kh),\; U(h, a, b) = \sum_{k=1}^{N}hf(a+kh) 
$$
$L(h,a,b)$ is essentially the sum of the areas of all the **orange** rectangles, and $U(h,a,b)$ is the sum of the areas of all the **blue rectangles**.

>If you're struggling to understand exactly why this works, refer back to the graphs above. Notice that the $i$th **blue rectangle** is the exact same as the $(i+1)$th **orange rectangle**.

As $h$ approaches 0, the difference between $L(h,a,b)$ and $U(h,a,b)$ gets closer and closer to 0, but $h$ can never **actually** reach 0, since 
$$
N=\frac{b-a}{h}
$$

This means that 
$$
A(h, a, b)=\lim_{h\to0}\sum^{N-1}_{k=0}hf(a+kh)
$$
This, initially, is not that helpful, but what if $f(x)$ is actually the derivative of some function $F(x)$.

Assuming that $f(x)=F'(x)$, we know 
$$
f(x) = \lim_{h\to0}\frac{F(x+h)-F(x)}{h}
$$
and so we know that 
$$
A(h,a,b)=\lim_{h\to 0}\sum^{N-1}_{k=0}h\cdot(\lim_{h\to0}\frac{F(a+(k+1)h)-F(a+kh)}{h})
$$
Two limits is a bit redundant so we can remove the inner limit to get
$$
\begin{split}
A(h,a,b) 
& = \lim_{h\to 0}\sum^{N-1}_{k=0}h\cdot(\frac{F(a+(k+1)h)-F(a+kh)}{h}) \\
& = \lim_{h\to 0}\sum^{N-1}_{k=0}{F(a+(k+1)h)-F(a+kh)}
\end{split}
$$
We still can't completely remove the limit as $h$ still exists in the denominator of the expression for $N$.

Now consider the process of actually summing up this area. We show this process below, with $S$ indicating the sum at that step.
$$
\begin{split}
k=1:\;\; S 
& = \lim_{h\to 0}F(a+2h) - F(a+h) \\
\\
k=2:\;\;
S 
& = \lim_{h\to 0}F(a+3h) - F(a+2h) + F(a+2h) - F(a+h) \\
& = \lim_{h\to 0}F(a+3h) + F(a+h) \\
\\
k=3:\;\; S
& = \lim_{h\to 0}F(a+4h) - F(a+3h)h + F(a+3h) + F(a+h) \\
& = \lim_{h\to 0}F(a+4h)-F(a+h) \\
&\;\;\vdots
\\
k=N-1:\;\; S
& = \lim_{h\to 0}F(a+Nh) - F(a+h)
\end{split}
$$

Notice that, since we subtract $F(a+kh)$ and add $F(a+(k+1)h)$ each step, the positive term of each step is cancelled out by the negative term of the next step. So our final expression only keeps the positive term of the last step and the negative term of the first step.

We also know that $a+Nh = b$ which means that 
$$
A(h,a,b)=\lim_{h\to 0}F(b)-F(a+h)
$$
Since we no longer use $N$, we can now remove the limit and safely set $h=0$ to get
$$
A(a, b) = F(b) - F(a)
$$

In conclusion, the area under a the graph of $f(x)$ between $x=a$ and $x=b$ is given by
$$
F(b)-F(a)
$$
where $f(x)=F'(x)$.

We call the area under the graph of $f(x)$ between $x=a$ and $x=b$ the **definite integral** of $f(x)$ from $a$ to $b$ and we denote it by
$$
\int_a^bf(x)dx = F(b)-F(a)
$$
The $\int$ sign is chosen as a replacement for the sum sign.

We call the general formula for the area under the graph the **indefinite integral** and we denote it the same, just without the limits
$$
\int f(x)dx = F(x)
$$
## Anti-Derivatives
The function $F(x)$ for which $f(x)=F'(x)$ is called the **anti-derivative** of $f(x)$.

We compute **anti-derivative** by applying the inverse of the rules we have for finding the derivative. We will go over the rules in a bit, but first lets look at a specific example.

Consider the function given by
$$
f(x)=5x-x^3
$$

We can find the anti-derivative of this function by inverting the power rule, so incrementing the power by 1 and dividing by the new power. So
$$
\begin{split}
5x \to \frac{5x^2}{2}\\
\\
x^3 \to \frac{x^4}{4}
\end{split}
$$
This tells us 2 of the terms for our **anti-derivative**, but there is 1 other term which may exist.

We know from the constant rule that when we differentiate a constant it becomes 0, because of this we can't be sure that $F(x)$ does not have a constant term. To indicate this we have to add the term $C$ to our anti-derivative to indicate some arbitrary constant.

So putting it all together, our antiderivative for $f(x)$ is
$$
F(x) = \frac{5x^2}{2}-\frac{x^4}{4} + C
$$

Because we must include the term $C$, it means that any function which has **one** anti-derivative actually has **infinitely many**, as there are infinite possibilities for the value of $C$.

Now lets see how we can use this anti-derivative to calculate the area under the graph of $f(x)$ from $x=0$ to $x=2$. We can do this by simply substituting these values into the formula we have for a definite integral.
$$
\begin{split}
\int_0^2f(x)dx 
& = F(2) - F(0) \\
& = (\frac{5(2)^2}{2}-\frac{(2)^4}{4}+C)-(\frac{5(0)^2}{2}-\frac{(0)^4}{4}+C) \\
& = 10-4+C-C \\
& = 6
\end{split}
$$
Notice that the $C$ terms always cancel out when finding definite integrals.

To get an idea of what we are computing when we do this, you can look at the image below. 6, as found above, is the area of the blue region on the graph.
![[definite_integral_example.png]]
### Signed Area
How about if, instead of $x=0$ to $x=2$ we now look at the area from $x=0$ to $x=4$. Now this is over a larger range, so immediately we know that this area should be larger, so lets calculate it like we did above.
$$
\begin{split}
\int_0^4f(x)dx 
& = F(4) - F(0) \\
& = (\frac{5(4)^2}{2}-\frac{(4)^4}{4}+C)-(\frac{5(0)^2}{2}-\frac{(0)^4}{4}+C) \\
& = 40-64+C-C \\
& = -24
\end{split}
$$
You will notice not only that this result is less than our previous result, but that it is negative. This is because what you are computing with a definite integral is the **signed area** with respect to the $x$-axis. Any area above the $x$-axis is considered positive and any area below the $x$-axis is negative.

Below you can see a zoomed out version of this graph. What this integral is actually computing is the **blue area** minus the **green area**, since the green area is larger than the blue area, this means that the total area is negative.

![[signed_area.png]]

If you want to calculate the **absolute area** you would need to find all the **roots** of $f(x)$ and then sum the absolute values of the definite integrals between each pair of roots.
## Rules For Integration
Integration and differentiation are **inverse** operations. If a continuous function is **integrated** and then **differentiated**, the original function is obtained.

Just like for **differentiation** we generally compute **anti-derivatives** by using standard rules which are generally inversions of the rules we had for differentiating functions. However, these rules are not sufficient for integrating all functions, and so **lists** or tables of **known integrals** are often used.

These more complicated integrals are not something you will necessarily need to understand for this module, but you should be aware that they exist.

For example $\int_0^1 \frac1xdx$ diverges (is infinite) as $x$ can approach but never reach 0, and $\int\sqrt{\sin(x)}$ is non-elementary. You can read about $\int\sqrt{\sin(x)}$ [here](https://www.johndcook.com/blog/2020/05/13/integrate-sqrt-sin/), but this is far outsides the bounds of this course.

Just like the [[Lecture 8 - First Derivative#Rules for Finding First Derivatives|rules for differentiation]], I will be explaining the rules in plain English as an exercise, but I think they are simpler to understand if you just look at their formal notation.
### The Scalar Product Rule
The scalar product rule states that if $f(x)$ is the product of a function $g(x)$ and a scalar value $s$, then the integral of $f(x)$ is the product of the integral of $g(x)$ and $s$.

So formally:
$$
f(x)=sg(x)\implies \int f(x)dx = s\cdot\int g(x)dx
$$
### The Sum Rule
The sum rule states that if $f(x)$ is the sum of two other functions $g(x)$ and $h(x)$ then the integral of $f(x)$ is the same as the sums of the integrals of $g(x)$ and $h(x)$.

So formally:
$$
f(x)=g(x)+h(x)\implies \int f(x)dx = \int g(x)dx + \int h(x)dx
$$
### The Power Rule
The polynomial rule states that if $f(x)$ is of the form $x^k$ then the integral of $f(x)$ is the same as $\frac{x^{k+1}}{k+1}$. This is an inverse of the power rule for differentiation, and does not work for $k=-1$.

So formally:
$$
\forall k\in\mathbb{R}\setminus \{-1\},\; f(x)=x^k\implies \int f(x)dx = \frac{x^{k+1}}{k+1}
$$
### The Reciprocal Rule
The reciprocal rule states that if $f(x)$ is of the form $\frac 1x$ then the integral of $f(x)$ is $\ln(x)$. This is an inverse of the logarithm rule for differentiation. The combination of this and the power rule allows us to integrate functions of the form $x^k$ $\forall k\in\mathbb{R}$.

So formally:
$$
f(x)=x^{-1}=\frac1x\implies \int f(x)dx = \ln (x)
$$
### Trigonometric Rules
The trigonometric rules for integration are the inverse of the trigonometric rules for differentiation. These rules state that the integral of $\sin(x)$ is $-\cos(x)$ and the integral of $\cos(x)$ is $\sin(x)$. The integral for $\tan(x)$ is a bit more complicated, and outside the scope of this course, but if curious you can read about it [here](https://math.stackexchange.com/questions/2696282/integral-of-tanx).

So formally:
$$
\begin{split}
& f(x)=\sin(x)\implies \int f(x)dx = -\cos(x)\\
\\
& f(x)=\cos(x)\implies \int f(x)dx = \sin(x)
\end{split}
$$
### The Exponential Rule
The exponential rule is the inverse of  the exponential rule for differentiation. It states that if $f(x)$ is of the form $n^x$ then the integral of $f(x)$ is $\frac{n^x}{\ln(n)}$.

So formally:
$$
f(x)=n^x\implies \int f(x)dx=\frac{n^x}{\ln(n)}
$$
Again this is most common when $n=e$ and therefore $\ln(n)=1$. Because of this, you may see this rule expressed as
$$
f(x)=\exp(x)\implies \int f(x)dx=\exp(x)
$$
## The Logarithm Rule
The logarithm rule is actually **not** the inverse of the logarithm rule from differentiation. It states that if $f(x)$ is of the form $\ln(x)$ then the integral of $f(x)$ is $x\ln(x)-x$.

So formally:
$$
f(x)=\ln(x)\implies \int f(x)dx = x\ln(x)-x
$$

The proof for this uses [integration by parts](https://en.wikipedia.org/wiki/Integration_by_parts), which I recommend you read about but is not needed for this course. If you want to see the full proof you can view it [here](https://www.cuemath.com/calculus/antiderivative-of-lnx/).