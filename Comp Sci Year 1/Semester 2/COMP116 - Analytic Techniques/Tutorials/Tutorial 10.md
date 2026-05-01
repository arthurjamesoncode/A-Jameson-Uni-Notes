## Question 1
**Answer:** First we need to check that the probabilities add to 1.
$$
4 \times 0.125 + 8 \times 0.0625 = \frac12+\frac12=1
$$
Since they do, we can now add up the probabilities like so
$$
\begin{split}
H(S) 
&= -\sum_i^nP_i\cdot \log_2(P_i) \\
&= -4\cdot\frac18\log_2(\frac18) - 8\cdot\frac1{16}\log_2(\frac1{16}) \\
&= -4 \cdot \frac18\cdot - 3 - \\
&= 1.5 + 2 \\
&= 3.50
\end{split}
$$
## Question 2
**Answer:** This suggests $L(S)\geq3.50$, meaning that, at minimum, it requires 3.50 bits on average to encode a symbol from this set. Since we want to encode all 12, we do $12\times3.5$ to get 42.
## Question 3
**Answer:** The probability distribution given doesn't add to one, so I don't think this works.
## Question 4
**Answer:**
$$
\begin{split}
H(S) 
&= -3(\frac14\log_2\frac14) - 2(\frac18\log_2\frac18) \\
&= -\frac34\cdot-2 -\frac14\cdot -3 \\
&= \frac64+\frac34 \\
&= \frac94 \\
&= 2.25
\end{split}
$$
## Question 5
**Answer:**
- A - No
- B - No
- C - Yes
- D - No
- E - No
- F - No
## Question 6
**Answer:**
$$
\begin{split}
P(\text{last}\;|\;\text{the}) &=  \frac17 \\
\\
P(\text{last}\;|\;\text{when, the}) &= 1
\end{split}
$$
Bias variance trade off

