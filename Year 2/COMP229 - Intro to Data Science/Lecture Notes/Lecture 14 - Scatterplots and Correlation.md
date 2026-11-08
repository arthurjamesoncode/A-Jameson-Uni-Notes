## Scatterplots
A scatter plot is a type of graph used to show the relationship between two quantitative variables in a set of data objects.

Say if we had $n$ objects with two variables $(x_i, y_i)$ then the scatterplot would have $n$ points in the $\mathbb R^2$ plane.

If we have $m$ quantitative variables, then the scatterplot would be in $\mathbb R^m$, although obviously we can only visualise up to $\mathbb R^3$.

If a variable is categorical instead of numeric, for example "Yes/No" or "Male/Female/Other", we can still show this on a scatterplot representing each category as a colour.

For example take the plot
![[scatterplot_example.png]]
The axis are two quantitative variables, and the colours represent categories. In this case it could Male/Female or similar.
## Normalisation and Standardisation
Real data often comes from different sources and is measured on different scales. To work with this data often we need to put it all back on the same scale.

This means we have to either normalise or standardise the data.

**Normalising** the data means to scale it so that all values are in the range $[0,1]$.

**Standardising** the data means to scale and shift it such that the mean is $0$ and the standard deviation is $1$.

>Normalisation can also refer to changing the shape of a distribution to fit a normal distribution. This should be done with great care.

For normalising a variable we can use **min-max scaling** which is essentially to apply the function
$$
f(x)=\frac{x-p}{q-p}
$$
to normalise a variable in the range $[p,q]$ to $[0,1]$.

We can also use the non-linear variations of this function
$$
f_n(x)=\left(\frac{x-p}{q-p}\right)^n
$$
For all $n\geq 1$. In all cases $f_n(p)=0$ and $f_n(q)=1$.

There is also a robust version of $z$-score normalisation that uses the median and IQR instead of the mean and standard deviation. 

>The slides don't go into much detail on this but they do provide a [link](https://www.kaggle.com/code/marcinrutecki/standardize-or-normalize-ultimate-answer).
## Variance, Covariance, and Correlation
Let variables $X$, $Y$ have $n$ samples $x_i$, $y_i$ with $i=1,...,n$ and sample means $\bar x$ and $\bar y$.

The covariance of these variables is
$$
\begin{split}
cov(X, Y)
&=E[(X-E[X])(Y-E[Y])] \\
&=E[XY] - E[X]E[Y]
\end{split}
$$
and the sample covariance is given by
$$
q_{xy}=\frac{1}{n-1}\sum^n_{i=1}(x_i-\bar x)(y_i-\bar y)
$$

If we recall that variance is
$$
\begin{split}
Var(X, Y) = \sigma^2_X
&=E[(X-E[X])^2] \\
&=E[X^2] - (E[X])^2
\end{split}
$$
and that sample variance is
$$
s^2_{x}=\frac{1}{n-1}\sum^n_{i=1}(x_i-\bar x)^2
$$

Then we can see that the **variance** of a variable is the same as the **covariance** of a variable with itself.

>Remember that when we find sample variance or covariance we divide by $n-1$ to correct for bias (Bessel's correction).

The **Pearson Product-moment** correlation is 
$$
\rho_{X,Y} = \frac{cov(X,Y)}{\sigma_X\sigma_Y}
$$
This is a number we can use to represent how **correlated** two variables are.

The **sample Pearson correlation** is given by
$$
\begin{split}
r_{xy}
&= \frac{q_{xy}}{s_xs_y} \\
&= \frac1{n-1}\cdot\frac{\sum^n_{i=1}(x_i-\bar x)(y_i - \bar y)}{s_xs_y} \\
&= \frac{\sum^n_{i=1}(x_i-\bar x)(y_i - \bar y)}{\sqrt{\sum^n_{i=1}(x_i-\bar x)^2\sum^n_{i=1}(y_i - \bar y)^2}}
\end{split}
$$
The last step of that is the easiest formula to apply.
## Correlations
Correlation between two variables represents how connected the variables are **linearly**. Lack of correlation doesn't mean no relationship, correlation just indicates a linear relationship:
- If two variables generally increase/decrease together they will have a **positive correlation**
- If one variable generally increases while another generally decreases, they will have a **negative correlation**

Below you can see a number of different scatterplots all with different correlation coefficients
![[correlated_scatterplots.png]]
The top row shows a gradual change in $r_{x,y}$ from 1 to -1. However in the middle line the change is sudden.

Notice that the middle line are all datasets that can be represented as a straight line. Therefore
$$
|r_{x,y}| = 1
$$
in all cases, with the exception of the very middle.

Directly horizontal or vertical lines do not have corelation coefficients since the variance, and therefore standard deviation, of one of the variables is 0. Since we divide by the standard deviation of both variables, this causes a divide by 0 error.

The bottom row of scatterplots all show datasets in which there is clearly some relation between the variables. The problem is that this relation is not linear and, as a result, the correlation coefficient is 0.

Sample correlation by itself does not imply causation. There is a list of [spurious correlations](https://www.tylervigen.com/spurious-correlations)
that you can view to illustrate this, and so you must be careful to assume a true correlation (which does imply causation) between variables off of a small sample.
## Linear Transformations
A function $f:\mathbb R^n\to\mathbb R^m$ is called a **linear transformation** if:
- It is closed under addition $f(\vec u + \vec v)=f(\vec u) + f(\vec v)$
- It is closed under scalar multiplication $f(s\vec v)=sf(\vec v)$

>You can look back to [[Lecture 6 - Linear Transformations]] from COMP116 and it's successive lectures for more detailed information.

When working with vectors, any linear transformation preserves the origin. In other words they stretch and rotate vectors but they don't translate them.

This means while we consider $f(x)=ax+b$ to be a linear function (in calculus) since it represents a straight line in $\mathbb R^2$ the function
$$
f(\vec u) = A\vec u + \vec b
$$
is not considered linear with vectors since $+\vec b$ is a translation. We refer to these types of functions as **affine**.
### Transformations and Correlation
Under any linear or affine transformation $x\to ax+b$ where $a\neq 0$ the correlation $r_{x,y}$ is multiplied by $sign(a)$.

This is because
$$
\begin{split}
r_{ax+b,y} 
&= \frac
{\sum^n_{i=1}((ax_i + b)-(a\bar x+b))(y_i - \bar y)}
{\sqrt{\sum^n_{i=1}((ax_i+b)-(a\bar x+b))^2\sum^n_{i=1}(y_i - \bar y)^2}} \\
&= \frac
{\sum^n_{i=1}(ax_i -a\bar x)(y_i - \bar y)}
{\sqrt{\sum^n_{i=1}(ax_i-a\bar x)^2\sum^n_{i=1}(y_i - \bar y)^2}} \\
&= \frac{a}{\sqrt{a^2}} \cdot \frac{\sum^n_{i=1}(x_i-\bar x)(y_i - \bar y)}{\sqrt{\sum^n_{i=1}(x_i-\bar x)^2\sum^n_{i=1}(y_i - \bar y)^2}} \\
&= \frac{a}{\sqrt{a^2}}\cdot r_{x,y}
\end{split}
$$
And you can notice that $\frac{a}{\sqrt{a^2}}$ is the same as $sign(a)$.

What this means is that corelation doesn't care about the shift or the scale of any specific variable.
### Linear Dependence
If two samples $x_i$ and $y_i$ are **linearly dependent** meaning that
$$
y_i=ax_i + b
$$
with $a\neq 0$ then $r_{x,y}=sign(a)$.

This follows from our definition, and from the theorem we just proved.
## Closing Problem
Problem "Find the sample correlation for

| $x$ | $y$ |
| --- | --- |
| 1   | 1   |
| 2   | 3   |
| 3   | 5   |
| 4   | 7   |
| 5   | 9   |
"

We can do this by plugging it into our formula. First we need the means
$$
\begin{split}
\bar x 
&= \frac{1+2+3+4+5}5 = 3 \\
\bar y
&= \frac{1+3+5+7+9}5 = 5
\end{split}
$$

Then we need to find our numerator
$$
\begin{split}
\sum^n_{i=1}(x_i-\bar x)(y_i - \bar y) 
&= (1-3)(1-5)+(2-3)(3-5)+(3-3)(5-5)+(4-3)(7-5)+(5-3)(9-5) \\
&= 8 + 2 + 0 + 2 + 8 \\
&= 20
\end{split}
$$

Then we need to find our denominator. Which we can do by finding the two parts of it first and multiplying them
$$
\begin{split}
\sum^n_{i=1}(x_i-\bar x)^2
&= (1-3)^2+(2-3)^2+(3-3)^2+(4-3)^2+(5-3)^2 \\
&= (-2)^2 + (-1)^2 + 0^2 + 1^2 + 2^2 \\
&= 4 + 1 + 0 + 1 + 4 \\
&= 10 \\
\\
\sum^n_{i=1}(y_i-\bar y)^2
&= (1-5)^2+(3-5)^2+(5-5)^2+(7-5)^2+(9-5)^2 \\
&= (-4)^2 + (-2)^2 + 0^2 + 2^2 + 4^2 \\
&= 16 + 4 + 0 + 4 + 16 \\
&= 40
\end{split}
$$
And now putting it altogether we get
$$
\begin{split}
r_{x,y} &= \frac{20}{\sqrt{10\cdot40}} \\
&= \frac{20}{20} = 1
\end{split}
$$

We could skip most of this by just recognising that these are the values for
$$
y=2x-1
$$
and therefore $x$ and $y$ are linearly dependent and $r_{x,y}$ must be 1.