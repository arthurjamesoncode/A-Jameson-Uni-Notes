## Question 1
Which of the following vectors is a **unit vector** under the Standard Euclidean metric? 

**Question:** $$
\langle0,1,0,0.25,-0.25\rangle
$$
**Answer:** No, because $$\sqrt{1^2+0.25^2+(-0.25)^2}=\sqrt{1+\frac18}\neq1$$  

**Question:**$$
\langle-1,0,0,1\rangle
$$
**Answer:** No, because $$
\sqrt{(-1)^2+1^2}=\sqrt2\neq1
$$
**Question:**$$
\langle 0,0,0.5,0.5,0,\frac1{\sqrt{2}}\rangle
$$
**Answer:** Yes, because $$
\begin{split}
\sqrt{0.5^2+0.5^2+(\frac1{\sqrt2}})^2 
& =\sqrt{\frac14+\frac14+\frac12} \\
& =\sqrt1 \\
& = 1
\end{split}
$$
**Question:** $$
\langle \cos\frac\pi2, 0, \sin\frac\pi2\rangle
$$
**Answer:** Yes, because $$
\begin{split}
\sqrt{(\cos\frac\pi2)^2 + (\sin\frac\pi2)^2}
& = \sqrt{0^2+1^2} \\
& = \sqrt{1} \\
& = 1
\end{split}
$$
**Question:** $$
\langle 1, 0, -1\rangle
$$
**Answer:** No, because $$
\sqrt{1^2+(-1)^2}=\sqrt2\neq1
$$
**Question:**$$
\langle-\cos\frac\pi8,0,\sin\frac\pi8\rangle
$$
**Answer:** Yes, because $$
\sqrt{(-\cos\frac\pi8)^2+(\sin\frac\pi8)^2}=\sqrt1=1
$$
****
## Question 2
Vector magnitude (length) depends on how we define the geometry of the space it lives in. 

Different ways of measuring are given by different definitions of distances.

We call such magnitudes (or lengths) the vector norms:

in lectures we saw the Euclidean $L_2$-norm $||v||_2=\sqrt{x^2+y^2}$

$L_1$-norm: $||v||_1=|x|+|y|$

$L$-infinity norm: $||v||_\infty=\max(|x|,|y|)$

In the general case, we define an $L_p$-norm for a vector $v=(v_1,...,v_n)$ in an n-dimensional real space $\mathbb R^n$ as $$
||v||_p=(\sum^n_{i=1}|v_i|^p)^{\frac1p}
$$
**Question:** Place the following vectors in order of increasing magnitude:
- $A$: $(0,1,0,1)$ in the $L_1$ norm
- $B$: $(1,0,1,0)$ in the $L_p$ measure with $p=3$
- $C$: $(0,0,1,1)$ in the $L_p$ norm with $p=0.5$
- $D$: $(0,1,1,1)$ in $L$-infinity norm
- $E$: $(0,1,1,0)$ in the $L_2$ measure.

**Answer:** First we can find the values of the magnitude for each vector:
$$||A||_1 = 1+1=2$$ $$||B||_3 = (1^3 + 1^3)^{\frac13} = 2^{\frac13}\approx1.2599 $$ $$||C||_{0.5}=(1^{0.5}+1^{0.5})^{\frac1{0.5}}= 2^2=4 $$ $$||D||_\infty= \max(0, 1, 1, 1) = 1$$ $$||E||_2 = (1^2+1^2)^{\frac12}=2^{\frac12}\approx=1.4142 $$
Now that we know the magnitudes we can rank them like so (from smallest to largest):
- $D$
- $B$
- $E$
- $A$
- $C$

>Note that the tutorial ranks them $BEDAC$. The only difference is that it $D$ is in a different place. I do not understand where she has gotten this from, but I am going to wait until we get to the tutorial first.
>
>**Update:** after going to the tutorial, the TA Laura agreed with me that this is wrong. So I am emailing Olga.

****
## Question 3
Which of the following statements is **true** and which is **false**?

### (a)
**Question:** For every pair of $n$-vectors, $u$ and $v$: $$
||\vec u+\vec v|| \leq ||\vec u|| + ||\vec v||
$$
**Answer:** True, the shortest distance between two points a straight line. $u+v$ is a straight line pointing to where the head of $u$ would be if it's tail lay at the head of $v$ (or vice versa). 

Therefore $||u+v||$ is always smaller that $||u|| + ||v||$ as it takes a more direct path to the same point. The one exception to this is when $u$ and $v$ are parallel. In which case $||u+v|| = ||u|| + ||v||$.

### (b)
**Question:** For very choice of $p\in\mathbb R^+$ and every $n\in\mathbb N$ there is at least one $n$-vector $u$ for which $||u||_p=1$.

**Answer:** True, take the $n$-vector $\vec v$ whose first component is 1 while the rest of it's components are 0. As $1^x=1$ and $0^x=0$ for all $x\in\mathbb R$, we know the $L_p$ norm is given by $$||\vec v||_p = 1^\frac1p = 1$$and therefore this vector is always a unit vector for all $n\in\mathbb N$ and $p\in\mathbb R$.
### (c)
**Question:** For every $n$-vector, $\vec u$ having components chosen from $\mathbb R^+\cup \{0\}$ (with $n\in\mathbb N$ and $\vec u\neq \vec 0$) there is a choice of $p\in\mathbb R^+$ for which$$
||\vec u||_p = 1
$$
**Answer:** False. The answer to **(e)** is a counter example.

### (d)
**Question:** For every $n$-vector, $\vec u$ there is an $n$-vector, $\vec v$ for which $$
||\vec u+\vec v|| > ||\vec u|| + ||\vec v||
$$
**Answer:** False, this is disproved by the proof for **(a)**.
### (e)
**Question:** For every $n$-vector, $\vec u$ (with $n\in\mathbb N$ and $u\neq 0$ ) there is a choice of $p\in\mathbb R^+$ for which $$
||\vec u||_p = 1
$$
**Answer:** False. 

Let $\vec u = (0,0.1)$

Observe that $$
\begin{split}
||\vec u||_p
& = (\sum^n_{i=1}|u_i|^p)^{\frac1p} \\
& = (|0.1|^p)^\frac1p \\
& = 0.1
\end{split}
$$
Therefore there is no value of $p\in\mathbb R^+$ for which this vector is a unit vector.
### (f)
**Question:** For every $n$-vector, $\vec u$ (with $n\in\mathbb N$) there is a choice of $p\in\mathbb R^+$ for which $$
||\vec u||_p = 1
$$
**Answer:** False, when $\vec u=\vec 0$, $||\vec u||_p=0,\;\forall p\in\mathbb R^+$.

****
## Question 4
**Question:** What matrix would be suitable for realising an effect involving scaling by a factor of 0.25, reflecting in the line $y=x$ and then moving $20$ places right (i.e. along the $x$-axis) and 10 places down (i.e. along the $y$-axis)?

**Answer:** $$
\begin{pmatrix}
0    & 0.25 & 20  \\
0.25 & 0    & -10 \\ 
0    & 0    & 1
\end{pmatrix}
$$
****
## Question 5
### (a)
**Question:** What's the algebraic form of this transformation in $\mathbb R^2$: "Scale the first coordinate by 2, the second by 3, and then translate by $\binom21$"?

**Answer:** $$
\binom xy\to \binom{2x+2}{3y+1}
$$
### (b)
**Question:** What's the transformation given by $\binom xy\to\binom{3x-3}{2y-4}$?

**Answer:** It scales the first coordinate by 3, scales the second coordinate by 2 and then translates by $\binom21$

****
## Question 6
How would you implement the following effects on a 2-dimensional graphical display?
### (a)
**Question:** A disc of radius 16 starting with its centre at $(272,272)$ bouncing in a **straight line direction** on a flat surface represented by a solid line with equation $y=0$.

**Answer:** I would give the ball a velocity property (which would be a vector) which is added to the disc's position every frame. I would add $\binom{0}{-y}$ to the velocity every frame, where $y$ is an appropriate acceleration value for creating the sort of animation I want. When the ball is at the position $(272, 16)$ (or reasonably close) I would set the velocity to $\binom0{j}$ where $j>0$ and is a value that causes velocity to be $\binom00$ when the balls position is $(272,272)$. I would find an exact value for $j$ but that would require choosing an fps and doing a bunch of calculations and I cba to practice this for a MCQ test.
### (b)
**Question:** A disc of radius 16 starting with its centre at $(272, 272)$ bouncing on a flat surface represented by a solid line with equation $y=0$ but after the $i$th "bounce" the disc returns to a position $(272, 272 - 2\cdot i)$.

**Answer:** The same as the first one, except that now we choose a $j$ relative to $i$ such that the balls velocity will be $\binom00$ when the ball is at $(272, 272 - 2\cdot i)$
### (c)
**Question:** A disc of radius 16 starting with its centre at $(272, 272)$ bouncing on a flat surface represented by a solid line with equation $y=0$ but after the $i$th "bounce" the disc returns to a position $(272 + 2\cdot i, 272 - 2\cdot i)$

**Answer:** The same as the second one, except that now we choose a starting velocity of $\binom k0$ and whenever the balls position becomes $(x, 16)$ we change the velocity to $\binom kj$. We choose a value of $k$ such that in the time taken for the ball to fall it has moved 1 to the right. 
### (d)
**Question:** In the animation described in **(c)** what methods could be used to make the effect look "more realistic"?

**Answer:** If we decreased the value of $k$ slightly after each bounce. This would mean it doesn't return to the same position but the curve would more natural.

**\[Hint:** what path would be typically traced by a table tennis ball bouncing along a table when dropped from a given height?**]**

****
## Question 7
Vector manipulation does not only occur in **moving** objects on a display. Using standard **colour** **coding** conventions allows vector effects to be used to implement colour manipulations. A very widely used scheme for describing the colour of a pixel in, for example, a .jpg or .gif image is the so-called **RGB** convention. Here a 24 bit word is treated as three 8-bit sub-fields: bits 0-7 describe the "amount of _red_" (**R**) as a whole number between 0 (no red element) and 255 (maximum amount of red). Similarly bits 8-15 record the "amount of _green_" (**G**) and bits 16-23 the "amount of _blue_" (**B**).

In total a "colour" is a 3-vector whose components are chosen from $\mathbb Z_{256}$: the integers modulo 256.

In this **addition** and **scalar multiplication** are defined as (when $x$, $y$ and $k$ are whole numbers between 0 and 255) $$
\begin{split}
& x+y = (x+y)\mathbf{mod}{256} \\ \\
& k\cdot x = (k\cdot x)\mathbf{mod}{256}
\end{split}
$$
For example: $128+128 = 0$, $253 + 12 = 9$, $3\cdot 87=5$/ For values **less than** 0 we report these as $-k=256-k$. For example, $-1=256-1=255$; $-45=256-45=211$.

How might the following colour changes be realised by applying a suitable matrix to the -vector defining the  components of an image's pixel?
### (a)
**Question:** Swapping the red component and the blue component leaving the green component unchanged?

**Answer:** The basis vectors for this vector space are $$
\vec e_r = (1,0,0),\;\vec e_g = (0,1,0),\;\vec e_b = (0,0,1)
$$meaning that the identity matrix for this vector space is $$
A=
\begin{pmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 
\end{pmatrix}
$$
We know that a map $f$ that would swap the red and blue component but leave the green component unchanged would give the following images:$$
f(\vec e_r) = \pmatrix{0 \\ 0 \\ 1},\;
f(\vec e_g) = \pmatrix{0 \\ 1 \\ 0},\;
f(\vec e_b) = \pmatrix{1 \\ 0 \\ 0}
$$Using these images we can construct our linear map matrix like so $$
A_f=
\begin{pmatrix}
0 & 0 & 1 \\
0 & 1 & 0 \\
1 & 0 & 0 
\end{pmatrix}
$$
### (b)
**Question:** Replacing the green component with its "negative"? (**Note:** this differs from the "arithmetic sense": "negative" is the result of swopping the bit 1 for 0 and vice versa, so that "$-0=255$" rather than 0)

**Answer:** First lets try to do this as a linear map constructed with our basis vectors, just like the last example.

We know the images of our basis vectors in this map:$$
f(\vec e_r) = \pmatrix{1 \\ 0   \\ 0},\;
f(\vec e_g) = \pmatrix{0 \\ 254 \\ 0},\;
f(\vec e_b) = \pmatrix{0 \\ 0   \\ 1}
$$giving us the matrix$$
A_f=
\begin{pmatrix}
1 & 0   & 0 \\
0 & 254 & 0 \\
0 & 0   & 1 
\end{pmatrix}
$$
Let's quickly test this matrix on some values:$$
\begin{split}
A_f\pmatrix{25\\50\\100} 
& = 
\begin{pmatrix}
1 & 0   & 0 \\
0 & 254 & 0 \\
0 & 0   & 1 
\end{pmatrix}
\pmatrix{25\\50\\100} \\
& = 
\pmatrix{25\\12700\mathbf{\;mod\;}256\\100} \\
& =
\pmatrix{25\\156\\100}
\end{split}
$$
Something is wrong here, since we know that $-50$ should be $255-50=205$ but the green component of our result is $156$. We constructed our matrix using the images of our vectors, which will always work for a **linear** map, so now we know that this map is **not** linear.

Let's consider how modulo arithmetic works and how we can get to $255 - k$ using addition and multiplication $\mathbf{mod}\;256$.  

$256k\;\mathbf{mod}\;256=0$ for all $k\in\mathbb Z$. However what is $255k\;\mathbf{mod}\;256$? Well we can see this on the table below:

| $k$ | $255k\;\mathbf{mod}\;256$ |
| --- | ------------------------- |
| 0   | 0                         |
| 1   | 255                       |
| 2   | 254                       |
| 3   | 253                       |
| 4   | 252                       |
We can see that the value of $255k\;\mathbf{mod}\;256$ is always $(256-k)\;\mathbf{mod}\;256$.

Realising this property gets us some of the way there. In fact if we use the matrix $$
A_f=
\begin{pmatrix}
1 & 0   & 0 \\
0 & 255 & 0 \\
0 & 0   & 1 
\end{pmatrix}
$$The green component of the resulting matrix is exactly 1 greater than it needs to be. So now we need to **add** another vector in order to **subtract** 1 from our green component. We cant use the vector $$\vec s=\pmatrix{0\\-1\\0}$$as all our components are $\mathbf{mod}\;256$, so we instead use the vector $$
\vec s=\pmatrix{0\\255\\0}
$$
To do this transformation in a single matrix, we need to use **homogenous** coordinates. So our final matrix is $$
A_f=
\begin{pmatrix}
1 & 0   & 0 & 0   \\
0 & 255 & 0 & 255 \\
0 & 0   & 1 & 0   \\
0 & 0   & 0 & 1
\end{pmatrix}
$$
>In the tutorial this is explained as multiplying by -1 and then adding the constant 255. This makes sense. This is rather obvious now, and I probably didn't need that table to figure out what 
### (c)
**Question:** Replacing **all** components by their "negative"?

**Answer:** To do this we can just generalise from our last answer. So the matrix we can use is $$
A_f=
\begin{pmatrix}
255 & 0   & 0   & 255 \\
0   & 255 & 0   & 255 \\
0   & 0   & 255 & 255 \\
0   & 0   & 0   & 1
\end{pmatrix}
$$