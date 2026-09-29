## Question 1
**Question:** An experiment reports the following outcomes for results ($y_i$) returned from data values ($x_i$).

| X   | Y    |
| --- | ---- |
| 2   | 1425 |
| 5   | 1014 |
| 8   | 900  |
| 11  | 548  |
| 14  | 381  |
| 17  | 274  |
| 19  | 248  |
| 21  | 181  |
| 23  | 26   |
| 25  | 16   |

What is the **gradient** of the best-fit line found by using least-squares minimization? Your answer should be accurate to one decimal place.

**Answer:** To answer this we use the formula
$$
a = \frac{\sum_{k=1}^n(x_i-\bar x)(y_i-\bar y)}{\sum_{k=1}^n(x_i-\bar x)^2}
$$

First we need our values for $\bar x$ and $\bar y$, which we calculate like so:
$$
\begin{split}
\bar x 
& = \frac{2+5+8+11+14+17+19+21+23+25}{10} \\
& = \frac{145}{10} \\
& = \frac{29}2 \\
& = 14.5 \\
\\
\bar y
& = \frac{1425+1014+900+548+381+274+238+181+26+16}{10} \\
& = \frac{5013}{10} \\
& = 501.3
\end{split}
$$

Now we can substitute into our equation like so:
$$
\begin{split}
a 
& = \frac{(2-14.5)(1425-501.3)+(5-14.5)(1014-501.3)+(8-14.5)(900-501.3)+(11-14.5)(548-501.3)+(14-14.5)(381-501.3)+(17-14.5)(274-501.3)+(19-14.5)(248-501.3)+(21-14.5)(181-501.3)+(23-14.5)(26-501.3)+(25-14.5)(16-501.3)}{(2-14.5)^2+(5-14.5)^2+(8-14.5)^2+(11-14.5)^2+(14-14.5)^2+(17-14.5)^2+(19-14.5)^2+(21-14.5)^2+(23-14.5)^2+(25-14.5)^2} \\
& = \frac{(-12.5)(923.7)+(-9.5)(512.7)+(-6.5)(398.7)+(-3.5)(46.7)+(-0.5)(-120.3)+(2.5)(-227.3)+(4.5)(-253.3)+(6.5)(-320.3)+(8.5)(-475.3)+(10.5)(-485.3)}{(-12.5)^2+(-9.5)^2+(-6.5)^2+(-3.5)^2+(-0.5)^2+2.5^2+4.5^2+6.5^2+8.5^2+10.5^2} \\
& = \frac{-11546.25-4870.65-2591.55-163.45+60.15-568.25-1139.85-2081.95-4037.5-5095.65}{156.25+90.25+42.25+12.25+0.25+6.25+20.25+42.25+72.25+110.25} \\
& = \frac{-31971.95}{552.5} \\
& = -57.86778281 \\
& = -57.9
\end{split}
$$

And so we found $a=57.9$ to 1 decimal place
## Question 2
Consider the same table of observations and results from **question 1**. If each $x_i$ is replaced by $\ln{x_i}$, and each $y_i$ is replaced by $\ln{y_i}$, what is the gradient of the new line of best fit.

**Answer:** To do this we need our new values for $\bar x$ and $\bar y$. We can actually use the logarithm rule of
$$
\log_n(a)+\log_n(b)=\log_n(ab)
$$
to simplify our calculations.

$$
\begin{split}
\bar x
& = \frac{\ln(3\cdot5\cdot8\cdot11\cdot14\cdot17\cdot19\cdot21\cdot23\cdot25)}{10} \\
& = \frac{25.00098915}{10} \\
& = 2.500098915 \\
\\

\bar y
& = \frac{\ln(1425\cdot1014\cdot900\cdot548\cdot381\cdot274\cdot238\cdot181\cdot26\cdot16)}{10} \\
& = \frac{55.54963577}{10} \\
& = 5.554963577
\end{split}
$$

Ok. I was extremely angry at the prospect of having to re compute the gradient, since its such a long and boring calculation. Since the dataset is exactly the same I looked into if there was a way to find the gradient of this new line, given the formula for the old line.

There is not. 

So I put it into a line of best fit calculator and moved on with my life.

The answer is -1.8

This calculator also told me that the above is wrong by less than 1. This is why calculating things like this by hand is incredibly stupid. It is incredibly easy to just get something slightly wrong somewhere and not know where.
## Question 3
Given a value for $k$ and a range for $x$, find the areas under the curve given by $f(x)=k$.

**Question:** $k=0,\;1\leq x \leq 2$

**Answer:** Since $k=0$, $f(x)=1$. 

Intuitively, we know the answer is 1, since the bounds given and line $y=1$ form a unit square, but to solve this with integration we can do. We first need to find the **antiderivative** $F(x)$ of $f(x)=1$ which is $F(x)=x+c$
$$
\begin{split}
\int_1^2 1dx 
& = F(2)-F(1) \\
& = 2 + c - (1 + c) \\
& = 1
\end{split}
$$
**Question:** $k=-1,\;1\leq x\leq2$

**Answer:** Since $k=-1$, $f(x)=\frac1x$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=\ln(x)+c$, we can then use this to find the area
$$
\begin{split}
\int_1^2 \frac1xdx 
& = F(2)-F(1) \\
& = \ln2 + c - (\ln1 + c) \\
& = \ln2-\ln1 \\
& = \ln2
\end{split}
$$

**Question:** $k=2,\;1\leq x\leq2$

**Answer:** Since $k=2$, $f(x)=x^2$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=\frac{x^3}3+c$, we can then use this to find the area
$$
\begin{split}
\int_1^2 x^2dx 
& = F(2)-F(1) \\
& = \frac{2^3}3 + c - (\frac{1^3}{3} + c) \\
& = \frac83-\frac13 \\
& = \frac73
\end{split}
$$

**Question:** $k=1,\;1\leq x\leq2$

**Answer:** Since $k=1$, $f(x)=x$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=\frac{x^2}{2}+c$, we can then use this to find the area
$$
\begin{split}
\int_1^2 xdx 
& = F(2)-F(1) \\
& = \frac{2^2}{2} + c - (\frac{1^2}{2} + c) \\
& = 2-\frac12 \\
& = \frac32
\end{split}
$$

**Question:** $k=2,\;0.5\leq x\leq1.5$

**Answer:** Since $k=2$, $f(x)=x^2$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=\frac{x^2}{2}+c$, we can then use this to find the area
$$
\begin{split}
\int_{0.5}^{1.5} x^2dx 
& = F(1.5)-F(0.5) \\
& = \frac{1.5^3}3 + c - \frac{0.5^3}{3} + c \\
& = \frac98-\frac1{24} \\
& = \frac{13}{12}
\end{split}
$$

**Question:** $k=-2,\;0.5\leq x\leq1.5$

**Answer:** Since $k=-2$, $f(x)=x^{-2}$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=-\frac{1}{x}+c$, we can then use this to find the area
$$
\begin{split}
\int_{0.5}^{1.5} x^{-2}dx 
& = F(1.5)-F(0.5) \\
& = -\frac{1}{1.5} + c - (-\frac{1}{0.5} + c) \\
& = -\frac23+2 \\
& = \frac{4}{3}
\end{split}
$$

**Question:** $k=-2,\;1\leq x\leq2$

**Answer:** Since $k=-2$, $f(x)=x^{-2}$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=-\frac{1}{x}+c$, we can then use this to find the area
$$
\begin{split}
\int_1^2 x^{-2}dx 
& = F(2)-F(1) \\
& = -\frac{1}{2} + c - (-\frac{1}{1} + c) \\
& = -\frac12+1 \\
& = \frac{1}{2}
\end{split}
$$
**Question:** $k=0,\;0.5\leq x\leq1.5$

**Answer:** Since $k=0$, $f(x)=x^{1}$.

Intuitively this means the area in the given range is $1\cdot(1.5-0.5)=1$

**Question:** $k=1,\;0.5\leq x\leq1.5$

**Answer:** Since $k=1$, $f(x)=x$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=-\frac{x^2}{2}+c$, we can then use this to find the area
$$
\begin{split}
\int_{0.5}^{1.5} xdx 
& = F(1.5)-F(0.5) \\
& = \frac{1.5^2}{2} + c - (\frac{0.5^2}{2} + c) \\
& = \frac98-\frac18 \\
& = 1
\end{split}
$$
**Question:** $k=-1,\;0.5\leq x\leq1.5$

**Answer:** Since $k=-1$, $f(x)=\frac1x$.

To find the area in the given range, we first find the **antiderivative**, which is $F(x)=\ln(x)+c$, we can then use this to find the area
$$
\begin{split}
\int_{0.5}^{1.5} \frac1xdx 
& = F(1.5)-F(0.5) \\
& = \ln(1.5) + c - (\ln(0.5) + c) \\
& = \ln(1.5) - \ln(0.5)\\
& = \ln(\frac{1.5}{0.5}) \\
& = \ln(3)
\end{split}
$$
## Question 4
Calculating Simple Linear Regression in $\mathbb{R^2}$ on different sets of pairs $(xi​,yi​)$. In each case, you should

(a) Find the least-squares regression line with the $x$-coordinate as the independent variable, and use it to “predict” the value for $x=0,x=1.5,x=10$.

(b) Find the least-squares regression line with the $y$-coordinate as the independent variable.

(c) Plot the data and the lines. Are your predictions reasonable? Why or why not?

**Question:** **Dataset I:** (1,1), (2,4), (3,5), (4,6), (5,9)

**Answer:** First we find values for $\bar x$ and $\bar y$
$$
\begin{split}
\bar x 
& = \frac{1+2+3+4+5}{5} \\
& = 3 \\
\\
\bar y
& = \frac{1+4+5+6+9}{5} \\
& = 5
\end{split}
$$

**(a)** Now we use our formula for $a$, making sure we put $(x-\bar x)^2$ in the denominator
$$
\begin{split}
a 
& = \frac{(1-3)(1-5)+(2-3)(4-5)+(3-3)(5-5)+(4-3)(6-5)+(5-3)(9-5)}{(1-3)^2+(2-3)^2+(3-3)^2+(4-3)^2+(5-3)^2} \\
& = \frac{(-2)(-4)+(-1)(-1)+(0)(0)+(1)(1)+(2)(4)}{4+1+0+1+4} \\
& = \frac{8 + 1 + 0 + 1 + 8}{10} \\
& = \frac{18}{10} \\
& = 1.8 \\
\end{split}
$$

**Question:** **Dataset II:** (-2,4), (-1,1), (0,0), (1,1), (2,4)


**Question:** **Dataset III:** (1,1), (2,4), (3,9), (4,16), (5,25)



