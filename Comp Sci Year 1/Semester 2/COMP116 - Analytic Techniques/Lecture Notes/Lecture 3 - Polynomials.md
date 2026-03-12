## Binary and Octal
Most counting is done in a **decimal** system. That means a **base 10** system, which means a system that uses 10 symbols.

Low level computer systems use different bases for counting:
- **Binary (Base 2):** This is what low-level machine code is written in. It uses base 2 because most computers contain collections of tons of little on off switches, and binary makes the most sense in order to represent these.
- **Octal (Base 8):** This was introduced as a shorthand way to read binary. Since $2^3=8$, 3 binary digits corresponds to a single octal digit. This means we can represent binary strings using far fewer digits.

>**Hexadecimal (Base 16)** is another system for counting. It uses the 10 normal digits (0-9) plus the letters A-F to represent the numbers 10-15. It It is also used to simplify binary strings, and is probably more popular than octal as 2 hex digits can represent a whole byte.

## Modulo Arithmetic
Modulo arithmetic is a system of arithmetic for integers where numbers "wrap around" upon reaching a certain number, which we called the **modulus**.

It essentially is a type of division that focuses on the remainder instead of the quotient for any calculation $a$ (mod $n$). The result is the remainder left over after dividing $a$ by $n$.

We say $a=b(mod\; n)$, if $a$ and $b$ have the same remainder after being divided by $n$.

You may be familiar with modulus operations in various programming languages. For example in Haskell
```
ghci> 5 `mod` 2
1
```

``mod`` in Haskell is the the same as `%` in java, python or JavaScript and returns the remainder of dividing the left side by the right side. This is slightly different from the concept in maths.

In maths $b(mod\;n)$ actually has a meaning closer to the set of all numbers which have the same remainder as $b$ when divided by $n$. The main way this is different to a set is that we say $=b(mod\;n)$ instead of $\in b (mod\; n)$. So, in maths, $13=3(mod\;5)$ but in Haskell
```
ghci> 13 `mod` 5
3
```

There are a few key applications of modulo arithmetic:
- **Timekeeping:** A 12 hour clock is a modulo 12 system, since 10 + 4 = 12 and 14 = 2 (mod 12).
- **Cryptography:** It forms the backbone of RSA encryption and Diffie-Hellman key exchanges. you do not need to understand this, just know it is important for cryptography.
- **Programming:** It is used to determine is a number is even or odd, wrap indices in circular arrays and in hashing algorithms

We denote the set of integers modulo $m$, which is $\{0,1,2,\cdot\cdot\cdot,m-1\}$ by $\mathbb{Z}_m$ which is the collection of all possible remainders when an integer is divided by $m$.

You may notice that $\{0,1\}=\mathbb{Z}_2$ and $\{0,1,2,3,4,5,6,7\}=\mathbb{Z}_8$. So you can see that the symbols used for base $m$ counting systems actually correspond to $\mathbb{Z}_m$.
## Polynomials
A polynomial is a mathematical expression consisting of variables, coefficients, and exponents, combined using only addition, subtraction, and multiplication.

Using a single variable $x$, a polynomial $p(x)$ is defined as:
$$
p(x)=a_nx^n+a_{(n-1)}x^{n-1}+\cdot\cdot\cdot\; +a_1x+a_0
$$
With the key components:
- The **variable** $x$ - a placeholder value.
- The **coefficients** $a_i$ - numbers from some set, such as $\mathbb{Z, Q, R}$ or even from $\mathbb{Z}_k$
- The **degree** $n$ - the highest degree of $x$. It must be a non-negative integer.
- The **leading term** $a_nx^n$ - the term with the highest power.

It's important to know that there is another rule for what makes an identity a polynomial, related to the fact that $n$ must be a non-negative integer 

This other rule is that the powers must come from the natural numbers. In particular this means:
- There can be no **negative powers** ($x^{-1}$ which is $\frac1x$, etc.)
- There can be no **fractional powers** ($x^{\frac12}$ which is $\sqrt{x}$, etc.)

We use polynomials in Computer Science because they are simple and predictable. If you know a few points on a curve, a polynomial can help you fill in the blanks and find the rest of the data.

This allows computers to draw smooth curves in video games or to predict trends in data.
## Hidden Polynomials
Every number can be written as a polynomial for some value of $x$. 

Consider the number 1567 in decimal. This number can be written as 
$$
1567 = 1\times1000 + 5\times 100 + 6\times10 + 7\times1 
$$
We can also write this as 
$$
1567 = 1\times10^3 + 5\times10^2 + 6\times10^1 + 7\times10^0
$$
Now consider the polynomial 
$$
p(x)=x^3 + 5x^2 + 6x^1 + 7
$$
The coefficients of this polynomial are the same as the digits of 1567. We can also see that $$
p(10)=1567
$$
What this tells us is that we can construct a polynomial from a number that, when passed the base of the counting system the number uses, can return the original number.

Consider the binary number 1011, which is 11 in decimal. How could you translate this to a polynomial in a similar way to how we did it for 1567.

In order to do this we simply break down the number into each place value and the digit. 
$$
1011 = 1\times2^3 + 0\times2^2 + 1\times2^1 + 1\times2^0 
$$
If we simply change the 2s to a variable, $x$ we have a polynomial that, when passed 2, will return our given binary number. 
$$
p(x) = x^3 + x + 1,\; p(2) = 11
$$
Now consider the octal number 63, which is 51 in decimal. We can use this same process to find a polynomial that when passed 8 will return our given octal number.
$$
p(x)= 6x + 3,\; p(8) = 51 
$$
>Notice that the possible coefficients for a polynomial meant to represent a base $n$ number will be drawn from $\mathbb{Z}_n$.
## Operation on Polynomials
We can perform various operations on polynomials to generate new polynomials. 
### Addition and Subtraction
To add or subtract two polynomials, we simply combine the like terms. The like terms are any terms with the same power of $x$.

In terms of programming, this is the same as adding two arrays element by element.

For example:
$$
\begin{split}
(3x^2+2x+5)-(4x-1) 
& = 3x^2 + 2x + 5 -4x +4 \\
& = 3x^2 -2x + 9
\end{split}
$$
### Multiplication by a Scalar
A scalar is just a fixed number. To multiply a polynomial by a scalar, we multiply every coefficient by that number. 

In programming, an example could be scaling the intensity of a colour or the size of an object.

For example:
$$
3\cdot (2x^2-5x+1) = 6x^2-15x+3
$$ 
### Multiplication
Multiplication of two polynomials is done by multiplying every term in the first polynomial by every term in the second. This is known as the distributive law.

For Example: 
$$
\begin{split}
(x+2)(3x-1) 
& = 3x^2 + 6x - x - 2 \\
& = 3x^2 + 5x - 2
\end{split}
$$
In CS, operations on polynomials are the backbone of Cryptography. $mod(k)$ applied to these operations is the basis of modern encryption.

You can chain together multiplications of multiple polynomials, for example:
$$
\begin{split}
(x+1)(x+2)(x+3)(x+4) 
& = (x^2+3x+2)(x+3)(x+4) \\
& = (x^3+6x^2+11x+6)(x+4) \\
& = x^4+10x^3+35x^2+50x+24
\end{split}
$$
## Roots of Polynomials
A root, or a zero, of a polynomial is a value for $x$ which is a solution to the equation $p(x) = 0$. We consider roots solutions of polynomial identities.

On a graph of a polynomial, the roots are the exact points where the curve crosses or touches the horizontal $x$-axis.

There are some key properties of polynomial roots which we should know:
- **The Degree Rule** - A polynomial of degree $k$ will have at most $k$ real roots.
- **The Sign Change Rule** - This is also called the **Intermediate Value Theorem**, and states that if a polynomial is negative at one point $a$ and positive at another point $b$ it must have crossed the $x$-axis at least once somewhere in between.

>Polynomials of degree $n$ always have $n$ roots. This is true but only if you allow [[Lecture 14 - Complex Numbers|complex roots]] and count with **multiplicity** in mind. 
>
>Multiplicity is essentially the idea that if $r$ is a root of $p(x)$ then $r$ is not only also a root of $p(x)^n$, but is exactly $n$ coinciding roots of $p(x)^n$.
>
>For example, $x$ has 1 root of 0. $x^2$ also has 1 root of 0 but, if counted with multiplicity in mind, we would say $x^2$ has 2 coinciding roots at 0.
### Irrationals
It is worth revisiting irrational numbers. Irrational numbers can be solutions to certain identities.

Take the quantities $\sqrt{2}=2^{\frac12}$ and $\sqrt[3]{20}=20^{\frac13}$. We can see these as the solutions to the following polynomials:
- $2^{\frac12}:\; p(x)=x^2-2$
- $20^{\frac13}:\; p(x)=x^3-20$

There are some real numbers which are not definable as the root of a polynomial in $\mathbb{Q}[X]$ (The set of polynomials with rational coefficients). We call these numbers **transcendental**.

One example of a **transcendental number** is $\pi$. This was proven in 1882 by Ferdinand von Lindemann. While $\pi$ is the solution to polynomials like $p(x)= x-\pi$, there is no polynomial with rational coefficients that $\pi$ is a solution to.

This implies that $\pi$ and other transcendental numbers cannot be expressed through finite algebraic operations.
### Quadratic Polynomials
A quadratic polynomial is any polynomial of degree 2, they are of the form 
$$
ax^2 + bx + c
$$
and it's roots can be given by the quadratic formula 
$$
x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$

You can see a graphical representation of some quadratic polynomials below.
![[quadratic.png]]

A quadratic polynomial can have 0, 1, or 2 real roots. 

If $$b^2-4ac=0$$then it will have 1 real root $r$ given by $$\frac{-b}{2a}$$
If $$b^2-4ac>0$$then it will have 2 real roots given by the quadratic formula.

If $$b^2-4ac<0$$then it will have no real roots.
### Cubic Polynomials
Cubic polynomials are any polynomial of degree 3, they are of the form $$
ax^3 + bx^2 + cx + d
$$
Cubic polynomials must have at least 1 real root, and can have 1, 2, or 3 real roots.

There is a general formula for finding a cubic root, but it is really complicated and rarely used. Other methods are usually used which you can see later on.

![[cubic.png]]
### Roots as Factors
If a number $r$ is a root of a polynomial then $(x-r)$ is a factor of that polynomial.

So if we know that a quadratic curve crosses the $x$-axis at $x=2$ and $x=-3$ then we can write it as $$
(x-2)(x+3)=x^2+x-6
$$
When finding roots, we often will factorise equations if possible as finding the roots from $x^2+x-6$ is hard but finding the roots from $(x-2)(x+3)$ is trivial.

Since roots, can give us factors we can use the roots of a polynomial to write it as a product of its factors. So$$
p(x)=a(x-r_1)(x-r_2)\cdot\cdot\cdot(x-r_n)
$$
>In Digital filters for images and audio, for example an equalizer on Spotify or a filter in Photoshop, the software is often manipulating the roots of a polynomial.
### The Bisection Method
The **bisection method** is an application of the **Intermediate Value Theorem** and it similar to binary search. It finds the root of the polynomial by repeatedly halving the search area.

The bisection method is as follows:
- **Pick an Interval:** Find two points $a$ and $b$ where $p(a)<0$ and $p(b)>0$. By IVT, there must be a root between them.
- **Find the Midpoint:** Calculate $c=\frac{a+b}{2}$
- **Evaluate:** If $p(c)=0$ you have found the root and can finish. If $p(c)<0$ you know the root must be between $c$ and $b$. If $p(c)>0$ you know the root must be between $a$ and $c$.
- **Repeat:** Repeat the process with the new, smaller interval.

It's worth noting that occasionally roots will not be rational, and so you won't be able to find an exact value. Because of this instead of checking if $p(c)=0$ you check if $|p(c)|<l$ where $l$ is an acceptably small value.
## Predicting a Sequence
If I gave you the start of a sequence $$1,2,3,...$$what would you think would come next?

The obvious answer is 4 but a polynomial can justify many other answers:
- $1,2,3,4$ is described by $p(x)=x$
- $1,2,3,7$ is described by $p(x)=\frac12x^2-\frac12x+1$
- $1,2,3,10$ is described by $p(x)=x^3-6x^2+12x-6$

In fact there exists a polynomial which can justify any given sequence.
### Lagrange Interpolation
For any sequence $(x_0,y_0),(x_1,y_1),...,(x_n,y_n)$ of $n+1$ points there exists a **Lagrange polynomial** that goes through all of the points in the sequence.

Lagrange Interpolation is the process of building this type of polynomial from an initial sequence of points.

The process starts with us constructing what we call "indicator" polynomials. These are called **Lagrange Basis** polynomials and are denoted by $l_i$.

We then combine these polynomials using a formula, and this gives us a new polynomial which will hit every single one of these points.
### Finding Lagrange Basis Polynomials
Lagrange basis polynomials are defined so that $l_i(x)$ is equal to 1 when passed exactly 1 of the $x$ values from the $n+1$ point sequence and equal to 0 when passed every other $x$ value.

The polynomial $l_i(x)$ is given by $$l_i(x)=\prod_{0\leq j\leq n,\;j\neq i}{\frac{(x-x_j)}{(x_i-x_j)}}$$
To see how this works, consider the sequence of points with $x$ values $x_0,x_1,x_2$ and the **Lagrange basis** polynomial $l_0(x)$. We can see that $$
\begin{split}
l_o(x_0) 
& = \frac{x_0-x_1}{x_0-x_1} \times \frac{x_0-x_2}{x_0-x_2} \\
& = 1 \times 1 \\
& = 1
\end{split}
$$and that $$
\begin{split}
l_o(x_1) 
& = \frac{x_1-x_1}{x_0-x_1} \times \frac{x_1-x_2}{x_0-x_2} \\
& = \frac0{x_0-x_1} \times \frac{x_1-x_2}{x_0-x_2} \\
& = 0 \times \frac{x_1-x_2}{x_0-x_2} \\
& = 0
\end{split}
$$
As $x_0$ through to $x_n$ are constant values, the polynomial still only has one variable $x$. 

If we give it some real values, lets say $x_0=1,x_1=2,x_3=3$ we can see that $$
\begin{split}
l_0(x)
& = \frac{x-2}{1-2}\times\frac{x-3}{1-3} \\
& = \frac{(x-2)(x-3)}{(-1)(-2)} \\
& = \frac{1}{2}x^2 - \frac{5}{2}x + 3
\end{split}
$$which is a perfectly valid polynomial.
### Combining Lagrange Basis Polynomials
To determine our Lagrange polynomial $L(x)$, we need to combine our Lagrange basis polynomials.

To combine them, we use the formula $$
L(x)=\sum^n_{i=0}y_il_i(x)
$$where $l_i(x)$ represents our Lagrange basis polynomial and $y_i$ represents the $y$ value of our given points.

Consider the sequence of points $(x_0,y_0)=(1,2),(x_1,y_1)=(2,3),(x_2,y_2)=(3,1)$. Our Lagrange Basis polynomials are given by $$
\begin{split}
l_0(x)
& = \frac{1}{2}x^2 - \frac{5}{2}x + 3 \\
l_1(x) 
& = -x^2+4x-3 \\
l_2(x) & = \frac12x^2-\frac32x+1
\end{split}
$$and so our Lagrange polynomial is $$
\begin{split}
L(x) 
& = 2(\frac{1}{2}x^2 - \frac{5}{2}x + 3) + 3(-x^2+4x-3) + 1(\frac12x^2-\frac32x+1) \\
& = (x^2-5x+6)+(-3x^2+12x-9)+(\frac12x^2-\frac32x+1) \\
& = -\frac32x^2+\frac{11}2x-2
\end{split}
$$
### Overfitting
A higher degree polynomial, can be forced to pass through any set of points from a polynomial with a lower degree. The Lagrange polynomial is not necessarily the lowest degree polynomial that will pass through all of these points.

What this means for us is that an algorithm may not be able to make reliable predictions just because an it matches our historical data perfectly. 

In machine learning we call this **Overfitting**, where AI models are too complex and so can hit all the training data points perfectly but fail dramatically when predicting real world results.