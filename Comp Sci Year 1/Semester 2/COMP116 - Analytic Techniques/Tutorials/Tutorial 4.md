## Question 1
Sort the following statements into the following 3 categories:
- **A:** Can be differentiated only a finite number of times before becoming 0
- **B:** Can be differentiated infinitely often with a different function resulting each time
- **C:** In neither A nor B

**Question:**
$$
f(x) = x^k \quad \forall k \in \mathbb{N}
$$
**Answer:** A

**Question:**
$$
f(x) = x^k \quad \forall k \in \mathbb{W}
$$
**Answer:** A 

**Question:**
$$
f(x) = x^k \quad \forall k \in \mathbb{Q} \setminus \mathbb{W}
$$
**Answer:** B

**Question:**
$$
f(x) = x^k \quad \forall k < 0
$$
**Answer:** B

**Question:**
$$
f(x) = x^k \quad \forall k \in \mathbb{R}
$$
**Answer:** C

**Question:**
$$
f(x) = x^k \quad \forall k \in \mathbb{Z}
$$
**Answer:** C
## Question 2
**Question:** The function $f(x)$ is defined as $f(x) = \alpha x^3 + \beta x^2 + \gamma x$. Find the **smallest** critical point of this function (i.e. a value of $x$ for which $f'(x) = 0$) when $\alpha=12$, $\beta=20$ and $\gamma=6$.

Give your answer rounded to **2 (TWO)** decimal places.

**Answer:** So we know that 
$$
f(x) = 12x^3+20x^2+6x
$$
and by using the sum and power rules we know that 
$$
f'(x)=36x^2+40x+6
$$

To find the critical points we solve $f'(x)=0$ like so:
$$
\begin{split}
0 &= 36x^2+40x+6 \\
\\
x 
&= \frac{-40\pm\sqrt{40^2-4(36)(6)}}{2(36)} \\
&= \frac{-40\pm\sqrt{736}}{72} \\
&= \frac{-10\pm\sqrt{46}}{18} \\
\\
x_1 &= -0.1787593354 \\
x_2 &= -0.9323516657
\end{split}
$$

If we substitute these values of $x$ back into out original function then we get 
$$
\begin{split}
f(x_1)&\approx-0.501997 \\
f(x_2)&\approx2.065789
\end{split}
$$
Since $f(x_2)>f(x_1)$ our answer is to 2 decimal places is $-0.93$.
## Question 3
The function $f(x)$ is defined as $f(x) = \alpha \ln(x)^{\gamma} - \beta \ln(x)^{\gamma+1}$. This function has a critical point when $x = 1$. Find the other critical point of this function when $\alpha=10$, $\beta = 3$, and $\gamma=3$.

Give your answer to **two** decimal places.

**Answer:** To find the critical points of this function, first we must find $f'(x)$.

Since we know 
$$
f(x) = 10\ln(x)^3-3\ln(x)^4
$$
by the composition, power, and logarithm rules we know
$$
\begin{split}
f'(x)
& = 30\ln(x)^2(\frac1x) -12\ln(x)^3(\frac1x) \\
& = \frac1x(30\ln(x)^2-12\ln(x)^3) \\
& = \frac1x(6\ln(x)^2)(2\ln(x)-5)
\end{split}
$$
To find critical points, we need to solve $f'(x)=0$ which we can do by looking at the **factors** of $f'(x)$. Since $\frac1x$ can never be 0, we can find our critical points by solving
$$
\begin{split}
6\ln(x)^2 &= 0 \\ 
AND \\ 
2\ln(x)-5 &= 0
\end{split}
$$
$x=1$ is the given solution, and this is the solution for 
$$
6\ln(x)^2=0
$$
So to find our other solution we need to solve the other equation
$$
\begin{split}
2\ln(x)-5 & = 0 \\
2\ln(x) & = 5 \\
\ln(x) & = \frac52 \\
x & = e^{\frac52} \\
x & \approx  12.18249396
\end{split}
$$
Which gives us our answer of $x=12.18$.
## Question 4
Place the following functions into one of the following categories:
- **A:** The function has no critical points
- **B:** The function has a finite (at least one) number of critical points
- **C:** The function has infinitely many critical points

**Question:** 
$$
f(x)=\sin(x)^2 + \cos(x)^2 + 2x
$$

**Answer:** To answer this we first need to find $f'(x)$ which we can do with the sum, composition, and power rules like so
$$
\begin{split}
f'(x) 
& = 2\sin(x)\cos(x)-2\sin(x)\cos(x)+2 \\
& = 2
\end{split}
$$
We know that critical points satisfy the equation $f'(x)=0$, as it is never true that $2=0$, we know that this function has no critical points.

(Note that we can skip this logic if we remember that $\cos^2\theta+\sin^2\theta=1$ because then $f(x)$ becomes $2x+1$, which is a linear function and has no critical points)

**Question:** $$
f(x) = x^3 / 3 + x^2 / 2 + x
$$

**Answer:** To answer this first we need to find $f'(x)$ which we can do with the sum and power rules like so
$$
\begin{split}
f'(x) 
& = 3(\frac{x^2}3)+2(\frac{x}2)+1 \\
& = x^2 + x + 1
\end{split}
$$
We can then find the critical points by using the quadratic formula
$$
\begin{split}
x 
& = \frac{-1\pm\sqrt{1^2-4(1)(1)}}{2(1)} \\
& = \frac{-1\pm\sqrt{-3}}{2}
\end{split}
$$
Since $\sqrt{-3}$ is not a real value, we know that this function has no critical points.

**Question:** 
$$
f(x)=\exp(x^2) - 20x
$$

**Answer:** To answer this first we need to find $f'(x)$ which we can do with the exponential rule, the sum rule and the power rule like so
$$
f'(x)=2x\exp(x^2)-20
$$
Now we need to find the number of solutions to $f'(x)=0$ 
$$
\begin{split}
2x\exp(x^2)-20 & = 0 \\
2x\exp(x^2) & = 20 \\
\exp(x^2) & = \frac{10}x \\
x^2 &= \ln(\frac{10}x) \\
x^2 &= \ln(10) - \ln(x)
\end{split}
$$
We know that the graph of $\ln(10)$ is a constant so won't affect the shape of the graph much, the graph of $y=-\ln(x)$ approaches to $\infty$ as $x$ approaches 0, and that as $x$ approaches $\infty$ $y=-\ln(x)$ approaches $-\infty$. We also know that the graph of $y=x^2$ starts at 0, and approaches $\infty$ as $x$ approaches $\infty$.

Since the graphs of these equations go in opposite directions, we know that there must be exactly 1 intersection (solution) meaning that there is exactly 1 critical point in $f(x)$.

**Question:** 
$$
f(x)=\exp(1/x) - \log(1/x)
$$

**Answer:** To answer this, we first need to find $f'(x)$. We can do this with the exponential, logarithm, composition and sum rules like so
$$
\begin{split}
f'(x)
& = (x^{-2})\exp({x^{-1}}) - (x^{-1})^{-1}(x^{-2})\\
& = (x^{-2})(\exp(x^{-1})-x)
\end{split}
$$
Now that we have an expression for $f'(x)$ we need to solve $f'(x)=0$. We can do this by looking at the factors of our equation. We know $f'(x) = 0$ when:
- $x^{-2}=0$ (which is never true)
- $\exp(x^{-1})-x=0$

Since $x^{-2}=0$ is never true, we just need to know the number of solutions to $\exp(x^{-1})-x=0$, which we can solve like so:
$$
\begin{split}
\exp(x^{-1})-x & = 0 \\
\exp(x^{-1}) & = x \\
x^{-1} & = \ln(x) \\
\frac1x & = \ln(x) 
\end{split}
$$
So any solutions to that equation give us critical points. That equation is incredibly hard to solve, but we don't need to find a specific solution as we are only concerned with the number of solutions. 

If you recall the shape of the $y=\ln(x)$ graph, you know that as $x$ approaches 0, $y$ approaches $-\infty$ and, as $x$ approaches $\infty$, $y$ also approaches $\infty$. In contrast, if we recall the graph for $y=\frac1x$, we know that as $x$ approaches 0, $y$ approaches $\infty$ and as $x$ approaches $\infty$, $y$ approaches 0.

Since these graphs move in opposite directions, we know that they must only cross paths once, and therefore there is exactly 1 solution to our equation giving us a finite number of critical points.

**Question:** 
$$
f(x)=\sin(x)^2 + \cos(x)^2 + 2x^2 + 2x
$$

**Answer:** This is similar to one of the questions above, and so I will do it in a slightly different order. First we can simplify $f(x)$ like so 
$$
f(x)=2x^2 + 2x + 1
$$
Then, we need to find $f'(x)$, which we can do by using the sum and power rules like so
$$
f'(x)=4x+2
$$
Now we just need to find the number of solutions to $f'(x)=0$ like so
$$
\begin{split}
4x+2 & = 0 \\
4x & = -2 \\
x & = -\frac24
\end{split}
$$
and so we know that $f(x)$ has 1 critical point when $x=-\frac24$.

**Question:** 
$$
f(x)=x^3 / 3 + x^2 + x
$$

**Answer:** First we need to find $f'(x)$ which we can using the power and sum rules like so
$$
\begin{split}
f'(x) & = 3(\frac{x^2}{3})+2x+1 \\
f'(x) & = x^2+2x + 1 \\
f'(x) & = (x+1)(x+1) \\
f'(x) & = (x+1)^2
\end{split}
$$
Now we simply need to find the number of solutions to $f'(x)=0$ which we can do by looking at the factors of $f'(x)$. In this case $f'(x)$ is a perfect square and it has exactly 1 solution $x=-1$. So we know that $f(x)$ has a finite number of critical points.

**Question:** $$
f(x)=\sin(x)^2 - \exp(\cos(x))
$$

**Answer:** To answer this, first we need to find $f'(x)$ which we can do by using the trig, exponential, and composition rules like so
$$
\begin{split}
f'(x) 
& = 2\sin(x)\cos(x) - \exp(\cos(x))\cos(x)\\
& = \cos(x)(2\sin(x)-\exp(\cos(x)))
\end{split}
$$
Now we just need to determine the number of solutions to $f'(x)=0$. $f'(x)=0$ is always true whenever the factors of $f'(x)$ are 0. Since $\cos(x)$ is a factor of $f'(x)$, this means that whenever $\cos(x)=0$, $f'(x)$ is also 0.

Since we know $\cos(x)=0$ has infinitely many solutions, it must be the case that $f'(x)=0$ has infinitely many solutions and therefore $f(x)$ must have infinitely many critical points.

**Question:** $$
f(x)=\sin(x) \log(x)
$$

**Answer:** To answer this first we need to differentiate it, which we can do with the product, trig, and logarithm rules like so
$$
\begin{split}
f'(x) = \cos(x)\log(x) + \frac1x\sin(x)
\end{split}
$$
Now we need to determine how many solutions there are for the equation $f'(x)=0$
$$
\begin{split}
\cos(x)\log(x) + \frac1x\sin(x) & = 0 \\
\cos(x)\log(x) & = -\frac1x\sin(x) \\
\log(x) & = -\frac1x\tan(x) \\
x\log(x) & = -\tan(x)
\end{split}
$$
We know the shape of the graph of $-\tan(x)$ is an infinitely repeating pattern that approaches $\infty$ and $-\infty$ repeatedly, so almost any function will intersect with it an infinite amount of times (the exceptions are vertical line functions and the same function with a horizontal offset). We know that $y=x\log(x)$ looks like a less steep $x^2$ for $x>0$, which means that it will intersect $y=-\tan(x)$ infinite times giving infinitely many solutions to $f'(x)=0$.

This means that we know that $f(x)$ has infinitely many critical points.
## Question 5
**Question:** From the provided document $$
LFM(x, z)=\frac{x\cdot z}{x^5+z^3+\beta}
$$where $\beta\in\mathbb N$.

Let $$MFL(x, z) = \frac{1}{LFM(x,z)}$$

**Question:** Find the **expressions** for $\frac{\partial MFL}{\partial x}$ and $\frac{\partial MFL}{\partial z}$, the two first-order partial derivatives.

**Answer:** To do this we first need our expression for $MFL$.
$$
MFL(x, z)=\frac{x^5+z^3+\beta}{xz}
$$
Next, we need to differentiate this with respect to $x$ and $z$. We could do this using the **quotient** rule, but if instead we rearrange $MFL$ so that it is just the sums of different expressions we can differentiate it only using the power and sum rules which is much easier. So
$$
\begin{split}
MFL(x,z) 
& =\frac{x^5}{xz}+\frac{z^3}{xz}+\frac{\beta}{xz} \\
& =x^4z^{-1}+x^{-1}z^2+\beta x^{-1}z^{-1}
\end{split}
$$
Now we can find the two partial derivatives using only the sum and power rules like so
$$
\begin{split}
\frac{\partial MFL}{\partial x} 
& = 4x^3z^{-1}-x^{-2}z^2-\beta x^{-2}z^{-1} \\
\\
\frac{\partial MFL}{\partial z}
& = 2x^{-1}z-x^4z^{-2}-\beta x^{-1}z^{-2}
\end{split}
$$

**Question:** Find the expressions for the second-order partial derivatives: $\frac{\partial^2 MFL}{\partial x^2}$; $\frac{\partial^2 MFL}{\partial z^2}$; and $\frac{\partial^2 MFL}{\partial x \partial z}$.

**Answer:** Just like above, we can use the power and sum rules to find the second-order partial derivatives.
$$
\begin{split}
\frac{\partial^2MFL}{\partial x^2}
& = 12x^2z^{-1} + 2x^{-3}z^2 + 2\beta x^{-3}z^{-1} \\
\\
\frac{\partial^2MFL}{\partial z^2}
& = 2x^{-1} + 2x^4z^{-3} + 2\beta x^{-1}z^{-3} \\
\\
\frac{\partial^2MFL}{\partial x\partial z}
&= -2x^{-2}z -4x^3z^{-2}+\beta x^{-2}z^{-2}\\
\end{split}
$$

**Question:** Now find the values of $x$ and $z$ (as functions of the constant $\beta$) that will **maximize** $LFM(x, z)$.

**Answer:** $LFM(x,z)$ is the reciprocal of $MFL(x,z)$, so to find the maximum of $LFM(x,z)$ we look for the minimum of $MFL(x,z)$.

We can find this by solving the simultaneous equations given by 
$$
\begin{split}
\frac{\partial MFL}{\partial x} = 0 \\
\frac{\partial MFL}{\partial z} = 0 
\end{split}
$$
which we can write as
$$
\begin{split}
(i)\;
& 4x^3z^{-1} - x^{-2}z^2 - \beta x^{-2}z^{-1} & = 0 \\
& \frac{4x^3}z - \frac{z^2}{x^2}- \frac{\beta}{x^2z} & = 0 \\
& \frac{4x^5}{x^2z}-\frac{z^3}{x^2z} -\frac{\beta}{x^2z} & = 0 \\
& 4x^5 - z^3-\beta & = 0 \\
\\
(ii)\;
& 2x^{-1}z - x^4z^{-2} - \beta x^{-1}z^{-2} & = 0 \\
& \frac{2z}{x} - \frac{x^4}{z^2} - \frac{\beta}{xz^{2}} & = 0 \\
& \frac{2z^3}{xz^2} - \frac{x^5}{xz^2} - \frac{\beta}{xz^2} & = 0 \\
& 2z^3 - x^5 - \beta & = 0
\end{split}
$$
Now to solve these equations we can add together twice the most simplified form of $(i)$ to the most simplified form of $(ii)$. Since $2(i)$ contains the term $-2z^3$ and $(ii)$ contains $z^3$ the $z$ terms cancel out and we are left with just $x$ and $\beta$, allowing us to find $x$ in terms of $\beta$.
$$
\begin{split}
2(i) + (ii) \\
\\
8x^5 - 2z^3 -2\beta + 2z^3-x^5-\beta & = 0 + 0 \\
7x^5 - 3\beta & = 0 \\
7x^5 & = 3\beta \\
x^5 & = \frac37\beta \\
x & = (\frac37\beta)^\frac15
\end{split}
$$
Now that we have a value for $x$ in terms of $\beta$ we can substitute this into $(ii)$ to find a value for $z$
$$
\begin{split}
2z^3 - ((\frac37\beta)^\frac15)^5-\beta & = 0 \\
2z^3 - \frac37\beta - \beta & = 0 \\
2z^3 & = \frac{10}7\beta \\
z^3 & = \frac57\beta \\
z & = (\frac52\beta)^\frac13
\end{split}
$$
There is only 1 solution to this set of simultaneous equations so we know that we must have found the $x$ and $z$ values for the only critical point of $MFL(x, z)$. So we can probably assume this to be the maximum of $FML(x,z)$ which the question wants us to find.

However to show that this critical point is a minimum of $MFL(x,z)$ (and therefore a maximum of $FML(x,z)$) we need to use our second order derivatives and the Hessian.

The Hessian in this case is
$$
H = 
\begin{bmatrix}
\frac{\partial^2MFL}{\partial x^2} & \frac{\partial^2MFL}{\partial xz} \\
\frac{\partial^2MFL}{\partial xz} & \frac{\partial^2MFL}{\partial z^2}  
\end{bmatrix}
$$

We need to calculate $D((\frac37\beta)^\frac15, (\frac52\beta)^\frac13)$ and so we must find substitute these values into each of our second order derivatives. In this case it becomes incredibly unruly because of how horrible these values are so I am not going to substitute them in because I respect my time.

