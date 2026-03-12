## Fitting Data
When we have a large number of data points, how can we **effectively** and **clearly** represent our data?

We could represent our data in a table, and we often do, but this can become long and make patterns seem unclear. It would be far better if we could define some kind of **function** which relates values.

Consider the following table of **observations** ($Y$) seen from a set of values ($X$):

| $X$ | $Y$ |
| --- | --- |
| 0   | 1   |
| 1   | 3   |
| 2   | 5   |
| 3   | 7   |
| 4   | 9   |
This table is a representation of this data, but we might be able to find a clearer one.

If we instead represent this table by plotting the points on a graph we get
![[plotted_points.png]]

Now consider the image below, which is the same graph but with the line $y=2x+1$ overlaid on it
![[perfect_fit_line.png]]

Observe that this line hits all of these points from our data perfectly! This means that the line $y=2x+1$ is a **perfect fit** for our data. What this means is that the function $f(x)=2x+1$ is a much more clear and concise way for us to represent our data. We can even use this function to predict what we might observe for values of $X$ not in our data.

In reality lines being perfect fits for data is very unlikely, but many lines can get either very close or close enough that they can be a useful approximating. **Linear regression**, which we will cover today, is the process of finding the best fitting line given a set of data points.

For some data, attempting to fit it to a linear function is misguided, and some method other than **linear regression** is required to find a well fitting function.

>You may recall [[Lecture 3 - Polynomials#Predicting A Sequence|Lagrange interpolation]] from lecture 3. This a method of data fitting that finds a polynomial which perfectly fits any given set of data points. This method often results in over-fitting, details of which are found in the same lecture.
## Measuring Best Fit
In order to find the best fitting function we need a way to measure how well each function fits a given data set.

The standard way to measure how well a function fits a given set of data points is **least squares**.

Given a set of data points from $\mathbb R^2$, 
$$
\{\langle x_k,y_k \rangle:k\in\mathbb{N},\; 1\leq k \leq n\}
$$
and a function $F: \mathbb{R\to R}$, the **least squares** score $S$ is given by
$$
S=\sum_{k=1}^n(y_k-F(x_k))^2
$$
Determining the best fitting function is an **optimisation problem**, the "optimal" solution for a given set of data points minimising some real function $S$.

We call the **vertical distance** between the observed point and the output of $F$, ($y_k - F(x_k)$), a **residual**. The least squares score is defined as the sum of the squares of the residuals. We square them before we sum them for a few reasons:
- To ensure that each result is positive, meaning that opposite direction residuals do not cancel each other out.
- Squaring "punishes" outliers, meaning that they add more to the score
- Squares are easy to differentiate
## Simple Linear Regression
The simplest example of data fitting is fitting a line. 

Recall that a linear function $f(x)$ is given by 
$$
f(x)=ax+c
$$
This means that a linear function $f(x)$ is defined by two characteristics:
- $a$ the gradient of the line
- $c$ the y-intercept of the line

This means that finding the **"best-fitting line"** is done by finding the best pair $(a,b)$ to maximise the function 
$$
S(a, b)=\sum_{k=1}^n(y_k-ax_k-b)^2
$$
Notice that $x_k$ and $y_k$ are actually not variables in our function $S(a,b)$ they are known numbers (or constants) which we get from our given data set.

We can now find values of $a$ and $b$ which maximise $S$ through partial differentiation. This won't be shown here but I recommend trying this as an exercise. It's useful to know where the formula comes from, but for this module you simply need to know the formulas for $a$ and $b$ which maximise $S$. 

This is given by
$$
\begin{split}
a 
& = \frac{\sum_{k=1}^n(x_i-\bar x)(y_i-\bar y)}{\sum_{k=1}^n(x_i-\bar x)^2} \\
\\
b & = \bar y -a\bar x
\end{split}
$$
Where $\bar x$ and $\bar y$ are the arithmetic means of all $x_k$ and $y_k$ values respectively.

Notice that the line of best fit will always pass through the **centroid** $(\bar x,\bar y)$ of the data.
### Example
Consider the data points given by the following table

| $x$ | $y$ |
| --- | --- |
| 1   | 1   |
| 2   | 2   |
| 3   | 3   |
| 4   | 10  |

We can see from this data that
$$
\begin{split}
\bar x 
& = \frac{1+2+3+4}{4} \\
& = \frac{10}4 \\
& = 2.5\\
\\
\bar y
& = \frac{1+2+3+10}{4} \\
& = \frac{16}{4} \\
& = 4
\end{split}
$$
This lets us compute $a$ like so
$$
\begin{split}
a 
& = \frac{\sum_{k=1}^n(x_i-\bar x)(y_i-\bar y)}{\sum_{k=1}^n(x_i-\bar x)^2} \\
& = \frac{(1-2.5)(1-4)+(2-2.5)(2-4)+(3-2.5)(3-4)+(4-2.5)(10-4)}{(1-2.5)^2+(2-2.5)^2+(3-2.5)^2-(4-2.5)^2} \\
& = \frac{4.5+1-0.5+9}{2.25+0.25+0.25+2.25} \\
& = \frac{14}{5} \\
& = 2.8
\end{split}
$$
Now that we have a value for $a$, we can substitute this in and find our value for $b$ like so
$$
\begin{split}
b 
& = 4-(2.8)(2.5) \\
& = 4-7 \\
& = -3
\end{split}
$$

Meaning that the best fitting line for these data points is given by the function
$$
f(x)=\frac{14}5x-3
$$
### Geometric Meaning of $a$
We have our formula for $a$ given by
$$
a = \frac{\sum_{k=1}^n(x_i-\bar x)(y_i-\bar y)}{\sum_{k=1}^n(x_i-\bar x)^2}
$$
We can see that the numerator actually corresponds to the difference between the **sum of the area of the green rectangles** and **the sum of the area of the red rectangles**, while the **denominator** corresponds to the **sum of the area of the blue squares**.
![[positive_numerator.png]]

To further illustrate this consider this inversion of the same data and notice how the green rectangles become red.
![[negative_numerator.png]]
## R-Squared
Now that we have a way to find our **line of best fit**, how do we know if this is actually a good way to model our data? The answer to this is to compare it against the simplest model, taking the **means**.

To do this we use the **coefficient of determination** which is denoted by $R^2$ and given by
$$
R^2 = 1 - \frac{SS_{res}}{SS_{tot}}
$$
Where
$$
\begin{split}
SS_{res} & = \sum_{k=1}^n(y_k-f(x_k))^2 \\
\\
SS_{tot} & = \sum_{k=1}^n(y_k-\bar y)^2
\end{split}
$$
Essentially, $SS_{res}$ is the sum of the squares of the residuals, and $SS_{tot}$ is the sum of the square of the difference between each $y$ value and the mean $y$ value.

Since both $SS$ values are sums of squares, we know that it is impossible for either $SS$ to be negative.

The maximum $R^2$ value is 1, which is achieved when $SS_{res}$ is 0, meaning that the function is a perfect fit.

If $R^2$ is 0, it means that $f(x)$ is no better a model than $\bar y$. It is possible for $R^2$ to be negative, which means that the function is a worse approximation compared to just taking the mean.

For example, consider the data set we used before, we can work out our $SS_{res}$ and $SS_{tot}$ values like so
$$
\begin{split}
SS_{res}
& = (1 - (\frac{14}{5}(1)-3))^2+(2 - (\frac{14}5(2)-3))+(3 - (\frac{14}{5}(3)-3))+(10 - (\frac{14}{5}(4)-3)) \\
& = (1+\frac15))+(2-\frac{13}5)+(3-\frac{27}{5})+(10-\frac{41}5) \\
& = 1.2^2 + (-0.6)^2 + (-2.4)^2+1.8^2 \\
& = 10.8 \\
\\
SS_{tot}
& = (1-4)^2+(2-4)^2+(3-4)^2+(10-4)^2 \\
& = (-3)^2+(-2)^2+(-1)^2+6^2 \\
& = 9 + 4 + 1 + 36 \\
& = 50
\end{split}
$$
Which lets us find $R^2$ like so
$$
\begin{split}
R^2 
& = 1 - \frac{10.8}{50} \\
& = 0.784
\end{split}
$$
You can see graphical representations of $SS_{res}$ and $SS_{tot}$ below
![[r-squared_graph.png]]
### Bigger is not Always Better (as I keep telling my girlfriend)
A better $R^2$ score does not mean a better set of predictions. $R^2$ always increases or stays the same as more variables are added, this is called [kitchen sink regression](https://en.wikipedia.org/wiki/Kitchen_sink_regression) which you don't need to know but can read about.

But even within two dimensions sometimes $R^2$ can mislead us.

Consider the following data set
$$
D:[10,9,11,10,10,9,11,10,100,100]
$$
and the following sets of predictions
$$
\begin{split}
&A:[10,9,11,10,10,9,11,10,70,70] \\
&B:[20,20,20,20,20,20,20,20,90,90]
\end{split}
$$
From looking at these predictions we can immediately see that $A$ is a generally better set of predictions, except that the last two much further off when compared to $B$.

I'm going to skip the computation, but if we calculate the $R^2$ values for these 2 sets of predictions we get
$$
\begin{split}
R^2_A & \approx 0.86 \\
R^2_B & \approx 0.923
\end{split}
$$
So going just off of $R^2$ scores alone, it seems that $B$ is a better set of predictions, which we can see to not be the case.
## Limits and Opportunities of LSR
Least-Squares Regression (LSR) does have some limitations:
- **Extreme values** - Since we square error, a single extreme value can skew the line away from the majority of the data
- **Can lose information about shapes:** Using the simple linear regression formula can create exactly the same line from different data sets with very different shapes.
- **Assumes homoscedasticity** - Residuals should be independent and uniformly distributed amongst variables (this is what homoscedasticity)
- **Predictions only make sense near given data** - The line of best fit for a group of marks based on study time could have a $y$-intercept of 20, but studying for 0 hours doesn't mean you will get 20 marks.

It is important to **understand your data BEFORE you fit it!**.

There are also plenty of opportunities for to use LSR:
- We can do **cross-validation** by randomly splitting the data into 5 groups. This lets us use 4 groups to find a regression line and then use the remaining group to test by computing the average error. You can then repeat this 4 more times by swapping groups.
- We can use more parameters or other functions. For example if we use $a$, $b$, and $c$ and a general quadratic polynomial function we can find the best fitting quadratic instead of the best fitting line.

We must be careful not to equate **correlation** with **causality**. You can look to [this website](https://www.tylervigen.com/spurious-correlations) for examples of correlating things which are clearly not related.
