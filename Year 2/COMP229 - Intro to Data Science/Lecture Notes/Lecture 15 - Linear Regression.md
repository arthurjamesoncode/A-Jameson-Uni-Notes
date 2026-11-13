This is somewhat a recap lecture for [[Lecture 13 - Linear Regression and Data Fitting]] from COMP116, although it does cover it in more detail.
## Linear Regression
Regression analysis is a statistical method for estimating the relationship between variables. For example, if a scatterplot seems to show a linear relationship between variables we could try to find the best straight line which approximates this scatterplot. This would be called **linear regression**.

For $n$ given data points $(x_i, y_i)$, the **ordinary least squares (OLS)** regression line has the equation
$$
y=ax+b
$$
where the constants $a$ and $b$ minimise the sum of squares $f(a, b)$
$$
f(a, b)=\sum^n_{i=1}(ax_i+b-y_i)^2
$$
In the above example, $x_i$ and $y_i$ are known numbers while $a$ and $b$ are unknown.

In this case we call $y$ the dependent variable and $x$ the independent variable and this process **Simple Linear Regression**.

To find the $a$ and $b$ which minimise $f(a,b)$ is an optimisation problem, and therefore originally done using calculus, we however do not need to do that. 

We can simply use a defined formula for $a$ and $b$ which will be shown shortly.
### Residuals and Symmetry
$$
|ax_i+b-y_i|
$$
is called the **residual**.

**Residuals** are the difference between a predictive model (such as a linear regression line) and the value for the corresponding input from a sample.

In this example the predictive model is $ax+b$, the given input is $x_i$ and the actual value from the sample is $y_i$.

We take the squares of the residuals for two reasons:
- So that residuals in different directions do not cancel out
- So that differentiation is nicer than if we used $|ax_i+b-y_i|$

An important thing to note here is that the residual as given is the **vertical distance** between the line and the point. If we swap the independent and dependent variables, our residual would now be the same as the **horizontal distance** on the original plot.

As a result of this, the regression isn't symmetric between variables.

If we say we regress on $y$ it means that $y$ is our dependent variable and we are finding the line
$$
y=ax+b
$$
similarly if we regress on $x$ it means to find the line
$$
x=cy+d
$$
### Formula
For $n$ points $(x_i, y_i)\in\mathbb R^2$, the simple linear regression line has the equation
$$
y=ax+b
$$
with
$$
a=\frac{\sum^n_{i=1}(x_i-\bar x)(y_i-\bar y)}{\sum^n_{i=1}(x_i-\bar x)^2}
$$
and
$$
b = \bar y - ax
$$
It is worth noting that $a$ has an interesting relationship with the sample correlation and sample standard deviations of $x$ and $y$

$$
a=r_{xy}\frac{s_y}{s_x}
$$

Another formula for $a$ is
$$
a=\frac{\overline{xy}-\bar x\bar y}{\overline{x^2}-(\bar x)^2}
$$
## Applications & Limitations
Linear approximation was the first approach to be used in ML algorithms.

Although lines can be deceptive. They can mask or create trends in data.

Below is a picture of "Anscombe's Quartet". This is a set of four datasets which all have the same:
- Means (x and y)
- Standard Deviations (x and y)
- Sample Correlation Coefficient
- Linear Regression Line

But are very different when plotted on a graph.
![[anscombe's_quartet.png]]

For the bottom two, single outliers skew the model further away from the rest.

For the top right, the curve seems to suggest some kind of polynomial regression to make more sense.

This is why visualisation and understanding of data is very important. It does not make sense to try and force everything into a line.

There are two main limitations of linear regression:
- Predictions only make sense near the given line
- Relations can be misleading if another variable is affecting both variables.
## Evaluators
Evaluators are ways to measure how good a certain predictive model is. There are many different ones which all have different downsides.

>Note that predicted values are represented by $\hat y$ 

**Mean bias error** is the mean of the residuals.
$$
MBE=\frac1n\sum(y_i-\hat y)
$$
The main downside of this is that residuals in different directions cancel each other out.

**Mean absolute error** is the mean of absolute values of the residuals.
$$
MAE = \frac1n|y-\hat y|
$$
**Mean square error** is the mean of the squared residuals.
$$
MSE=\frac1n\sum(y_i-\hat y)^2
$$
The main downside of this is that it is measured in squared units, which makes it harder to interpret. This is what we minimise when we look for $a$ and $b$ when doing linear regression.

**Root mean squared error** is the root of the mean squared error.
$$
RMSE=\sqrt{\frac1n\sum(y_i-\hat y_i)^2}
$$
**Mean absolute percentage error** is the mean of the absolute value of the residual divided by the absolute data value.
$$
MAPE=\frac1n \sum\frac{|y_i-\hat y_i|}{|y_i|}
$$
The main downside of this one is that you cannot differentiate it.

>Daniel notes that the first and last evaluators listed here are the least useful, although they all have downsides listed with their definitions.
### $R^2$
$R^2$, or the coefficient of determination, is an evaluator which compares how good a predictor is to the mean of the data set.

$$
\begin{split}
R^2
&=1-\frac{SS_{res}}{SS_{tot}} \\
&=1-\frac{\sum(y_i-\hat y)^2}{\sum(y_i-\bar y)^2}
\end{split}
$$

In the best case the $SS_{res}$ is 0 and $R^2=1$ and it's a perfect predictor over the sample.

If $SS_{res}=SS_{tot}$ then $R^2=0$ and the model is exactly as good at predicting as the mean is.

If $SS_{res}>SS_{tot}$ then $R^2<0$ the model is worse at predicting than the mean. 

This isn't always a great indicator of the accuracy of the dataset.

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
Case $B$ has a better $R^2$ value than $A$ despite the fact that $A$ is a better predictor in the majority of cases.

There is also the added problem that $R^2$ increases with the addition of dimensions. Adding irrelevant variables improves the results artificially.

### Other Notes
Cross validation means to randomly split the data into a number of groups (e.g. 5), and then compute a regression line from all but one, using the remaining group as a test.

Then you repeat the process so that all groups are used as the test group once.

Graphical analysis of residuals is an important part of validation. The residuals should be independent and have a constant variance.

Regression lines are highly sensitive to outliers. You should attempt to remove significant outliers which can lead to reversed conclusions.
## Closing Problem
"Find the regression line $y = ax + b$, and compare it to the regression line $x = cy + d$

| $x$ | $y$ |
| --- | --- |
| 1   | 3   |
| 2   | 1   |
| 3   | 2   |
| 4   | 1   |
| 5   | 3   |
"

First we need to find $\bar x$ and $\bar y$
$$
\begin{split}
\bar x 
&=\frac{1 + 2 + 3 + 4 + 5}{5} \\
&=\frac{15}5 \\
&=3 \\
\\
\bar y 
&=\frac{3+1+2+1+3}{5} \\
&=\frac{10}5 \\
&=2
\end{split}
$$

In both cases we need the numerator so we find
$$
\begin{split}
\sum^n_{i=1}(x_i-\bar x)(y_i-\bar y)
&=(1-3)(3-2)+(2-3)(1-2)+(3-3)(2-2)+(4-3)(1-2)+(5-3)(3-2) \\
&= (-2)(1)+(-1)(-1)+(0)(0)+(1)(-1)+(2)(1) \\
&= -2 + 1 + 0 -1 + 2 \\
&= 0
\end{split}
$$

Since our numerator is 0, we know that $a$ and $c$ are both 0 so we can find $b$ and $d$ like so.
$$
\begin{split}
b = 2 - 0(3) = 2 \\
c = 3 - 0(2) = 3
\end{split}
$$
And so our regression line for $y$ is
$$
y=2
$$
and our regression line for $x$ is
$$
x=3
$$