## Question 1
State whether each of the following representations is **equivalent** to the Complex number $5+12i$?

**Question**: 
$$\begin{pmatrix} 5 & -12 \\ 12 & 5 \end{pmatrix}$$

**Answer:** Yes, this is a valid matrix representation.

**Question:**
$$13e^{i \sin^{-1}(12/13)}$$

**Answer:** Yes. We can represent any complex number as $re^{i\theta}$ so we just have to check if we have the correct values for $r$ and $\theta$.

We can get the magnitude $r$ of our complex number like so
$$
\begin{split}
r 
& = \sqrt{5^2+12^2} \\
& = \sqrt{169} \\
& = 13
\end{split}
$$
Which matches.

We can find the angle in terms of $\sin^{-1}$ by considering that we have a triangle with a hypotenuse of 13 and an opposite (to the real axis) side length of $12$. Meaning that our angle is $\sin^{-1}(12/13)$, which also matches.

**Question:**
$$\sqrt{13}e^{i \sin^{-1}(12/13)}$$

**Answer:** No. We found our magnitude (13) while answering a previous part. Since $13\neq\sqrt{13}$ this cannot represent our number.

**Question:**
$$\left( 13, \cos^{-1} \left( \frac{12}{13} \right) \right)$$

**Answer:** No. We can represent our number in the form $(r, \theta)$, so we just need to check our values of $r$ and $\theta$.

13 is the correct value for $r$ but our angle is $\cos^{-1}(\frac5{13})$ which doesn't match.

**Question:** 
$$< 5, 12 >$$

**Answer:** Yes. This is the correct vector representation.

**Question:**
$$e^{i \cos^{-1}(11/13)}$$

**Answer:** No. Both the magnitudes and angle are incorrect.
## Question 2
**Question:** What is the **Real part** of the Complex Number $\frac{\alpha + i\beta}{\gamma - i\delta}$ when $\alpha=4$; $\beta=3$; $\gamma=6$ and $\delta=3$.

**Answer:** First we must rationalise the denominator.
$$
\begin{split}
\frac{4+3i}{6-3i} 
& = \frac{4+3i}{6-3i} \cdot \frac{6 + 3i}{6 + 3i} \\
& = \frac{24 + 18i + 12i 9i^2}{36+18i-18i-9i^2} \\
& = \frac{15+30i}{45} \\
& = \frac13 + \frac{2}{3} \\
\end{split}
$$
Now we can see that the real part is $1/3 \approx 0.33$.
## Question 3
Find the **simplest** form for each of the following:

**Question:**
$$\frac{5 - 4i}{11 + 12i}$$

**Answer:** To get the simplest form we must rationalise the denominator
$$
\begin{split}
\frac{5 - 4i}{11 + 12i}
& = \frac{5 - 4i}{11 + 12i} \cdot \frac{11 - 12i}{11 - 12i} \\
& = \frac{55 - 44i - 60i + 48i^2}{121 - 132i + 132i -144i^2} \\
& = \frac{7 - 104i}{265} \\
& = \frac{7}{265} - \frac{104i}{265} \\
\end{split}
$$

**Question:**
$$\frac{2 + i}{5e^{i\pi/4}}$$

**Answer:** First we can find a non Euler form for the denominator. Since 5 is the magnitude (hypotenuse) and $\frac{\pi}4$ is the angle we see the other side lengths (our real and imaginary part) are both $\frac{5\sqrt{2}}2$. 

This gives us 
$$
\frac{2 + i}{\frac{5\sqrt{2}}2(1 + i)}
$$

Which we can then rationalise like so
$$
\begin{split}
\frac{2 + i}{\frac{5\sqrt{2}}2(1 + i)} 
& = \frac{2 + i}{\frac{5\sqrt{2}}2(1 + i)} \cdot \frac{1 - i}{1 - i} \\
& = \frac{2 + i - 2i - i^2}{\frac{5\sqrt{2}}{2}(1 + i - i - i^2)} \\
& = \frac{3-i}{5\sqrt{2}} \\
& = \frac{3\sqrt{2}-i\sqrt{2}}{10} \\
& = \frac{3\sqrt{2}}{10} - \frac{\sqrt{2}}{10}i
\end{split}
$$

**Question:**
$$\frac{\cos \frac{\pi}{8} + i \sin \frac{\pi}{8}}{3 + 4i}$$

**Answer:** First we rationalise the denominator
$$
\begin{split}
\frac{\cos \frac{\pi}{8} + i \sin \frac{\pi}{8}}{3 + 4i}
& = \frac{\cos \frac{\pi}{8} + i \sin \frac{\pi}{8}}{3 + 4i} \cdot \frac{3-4i}{3-4i} \\
& = \frac{3\cos\frac\pi8-4i\cos\frac\pi8+3i\sin\frac\pi8+4\sin\frac\pi8}{25} \\
& = \frac{3}{25}\cos\frac\pi8 + \frac4{25}\sin\frac\pi8 - i (4\cos\frac\pi8 - 3\sin\frac\pi8)
\end{split}
$$
## Question 4
Check the Cauchy-Riemann Conditions for the following functions.

**Question:** 
$$
f(z) = z^2
$$

**Answer:** First we need to find an expression for $f$ in terms of 2 multivariate real valued functions
$$
\begin{split}
f(a+ib) 
& = (a+ib)^2 \\
& = a^2 - b^2 + i (2ab) \\
\end{split}
$$
This gives us 
$$
f(a, b) = u(a, b) + i \cdot v(a, b)
$$
where $u(a,b)=a^2-b^2$, $v(a,b)=2ab$.

Now we can find our partial derivatives like so
$$
\begin{split}
\frac{\partial u}{\partial a} & = 2a \\
\frac{\partial u}{\partial b} & = -2b \\
\\
\frac{\partial v}{\partial a} & = 2b \\
\frac{\partial v}{\partial b} & = 2a
\end{split}
$$
And we can see the Cauchy-Riemann conditions hold since
$$
2a = 2a,\; -2b = -(2b)
$$

**Question:**
$$
f(z)=\bar z^2
$$

**Answer:** First we need to find an expression for $f$ in terms of 2 multivariate real valued functions
$$
\begin{split}
f(a+ib) 
& = (a+ib)^2 \\
& = a^2 - b^2 - i (2ab) \\
\end{split}
$$
This gives us 
$$
f(a, b) = u(a, b) + i \cdot v(a, b)
$$
where $u(a,b)=a^2-b^2$, $v(a,b)=-2ab$.

Now we can find our partial derivatives like so
$$
\begin{split}
\frac{\partial u}{\partial a} & = 2a \\
\frac{\partial u}{\partial b} & = -2b \\
\\
\frac{\partial v}{\partial a} & = -2b \\
\frac{\partial v}{\partial b} & = -2a
\end{split}
$$
And we can see the Cauchy-Riemann conditions don't hold since
$$
2a \neq -2a,\; -2b \neq -(-2b)
$$

The only time when $2a=-2a$ is when $a=0$, and the only time when $-2b = -(-2b)$ is when $b=0$, meaning that we can only differentiate this function at 0.
