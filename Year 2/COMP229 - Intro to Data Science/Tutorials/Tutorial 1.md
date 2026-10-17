**Problem 1.1**

(1) Only 25% of professors could be in the top 25% of teaching ability, yet 90% think they are.

(2) This could be possible depending on which average you take. If the mean is used there could be a bunch of very bad professors.

**Problem 1.2 and 1.3**
$$
[1,9,9,9,9,9,9,9,9,9]
$$

**Problem 1.4**
This problem is just a bunch of simple computations. So I'm just going to list the important things gone over rather than transcribing the computations:
- The range, in this module, is considered the interval $[min, max]$ rather than the difference $max-min$
- Every non-empty dataset has a mode.
- It is possible for every datapoint to be the mode
- When finding sample variance you correct for bias by dividing by $n-1$ instead of $n$ (Bessel's Correction)
- Boxplots can use either the minimum and maximum value or they can use the minimum and maximum **non-outlier** values.

**Problem 1.5**
No. The minimum mean would be the sample with the collection of smallest integers that satisfy the conditions which is
$$
[-5,1,1,1,1,1,1,1,1,1]
$$
The mean of which is $\frac{9*1-5}{10}=\frac{4}{10}=0.4>0$.

**Problem 1.6**
We already know how a sample of $n$ integers from the range $[-5,5]$ with the minimum mean would be laid out.
$$
[-5,1,...,1]
$$

So the formula for the mean is:
$$
\frac{-5+n-1}n 
$$
And we just need to solve the following inequality like so
$$
\begin{split}
\frac{-5+n-1}n & \leq 0 \\
-5+n-1 & \leq 0 \\
n & \leq 6
\end{split}
$$
Since $6$ is the maximum value of $n$ which satisfies that inequality, we know the answer is 6.