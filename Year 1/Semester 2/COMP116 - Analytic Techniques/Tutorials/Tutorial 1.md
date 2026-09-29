## Question 1
**Question:** Which number class is best suited to modelling the following scenarios?

**(a):** The number of students formally registered on a mandatory (for programme of study) module.

**Answer:** $\mathbb{N}$ as the value is can only be positive integers and 0

**(b):** The number of students on a module who obtain a final mark over 40%

**Answer:** $\mathbb{N}$ as the value can only be positive integers and 0

**(c):** The difference in numbers of students enrolled on a module at its start and the number still registered on the module at its conclusion.

**Answer:** $\mathbb{Z}$ as the value can only be integers, but can be negative or positive depending on if people join or leave.
## Question 2
**Question:** What is the degree of the polynomial formed by expanding $(2x^2 + 2)^4(2x^2 - 2)(x - 1)^2$?

**Answer:** We can determine the degree of this polynomial by multiplying the powers of each bracket by the term with the highest power, and then summing the resulting powers.

So we can get an answer by doing $$
\begin{split}
2\times 4 + 2 + 2 \times 1
& = 8 + 2 + 2 \\
& = 12
\end{split}
$$
## Question 3
**Question:** Which of the following expressions, when simplified, describes a degree two (quadratic) polynomial?

(I have stated the expression, and written yes if it is a polynomial of degree two and no if otherwise. An explanation of why follows)

**(a)** $$
(6x^4-3)(x^2+3)(x^2-3)
$$
**Answer:** No. We know that, as there are only multiplications performed here, that the degree of the resulting polynomial has to be $>4$, and so we know it is not a polynomial of

**(b)** $$
\frac{(x^4-1)(x^4+1)(+1)}{x^6}
$$
**Answer:** Yes. We can simplify the polynomial like so $$
\begin{split}
\frac{(x^4-1)(x^4+1)+1}{x^6} 
& = \frac{(x^8-1)+1}{x^6} \\
& = \frac{x^8}{x^6} \\
& = x^2
\end{split}
$$and $x^2$ is a polynomial of degree 2.

**(c)** $$
\frac{(x^2-1)(x+1)}{10x}
$$
**Answer:** No. We can simplify this like so$$
\begin{split}
\frac{(x^2-1)(x+1)}{10x}
& = \frac{x^3 + x^2 - x - 1}{10x} \\
& = \frac{x^2}{10} + \frac{x}{10} - \frac{1}{10} - \frac{1}{10x} \\
& = \frac{x^2}{10} + \frac{x}{10} - \frac{1}{10} - \frac{1}{10}x^-1
\end{split}
$$We know that polynomials are only valid if the powers of $x$ are from the natural numbers. As one of the terms in this identity is $x^{-1}$ we know that this identity is not a polynomial.

**(d)**$$
4(x+6)(x-6)
$$
**Answer:** Yes. We can simplify this expression like so $$
\begin{split}
4(x+6)(x-6) 
& = 4(x^2 - 36) \\
& = 4x^2 - 144
\end{split}
$$
**(e)** $$
\frac{x^2 - 5x + 10}{20}
$$
**Answer:** Yes. We know that $$
\frac{x^2 - 5x + 10}{20} = \frac{1}{20}(x^2 - 5x + 10)
$$and so we that this is a quadratic polynomial multiplied by a scalar. As scalar's do not change the degree of the a polynomial we know this expression is a polynomial of degree 2.

**(f)**$$
\frac{(x-1)(x+2)(x-3)(x-4)}{x^2}
$$
**Answer:** No. We can simplify this expression like so $$
\begin{split}
\frac{(x-1)(x+2)(x-3)(x-4)}{x^2} 
& = \frac{(x^2+x-2)(x^2-7x+12)}{x^2} \\
& = \frac{x^4 -7x^3 + 12x^2 + x^3 - 7x^2 + 12x - 2x^2+14x-24}{x^2}\\
& = \frac{x^4 -6x^3+10x^2+26x-24}{x^2} \\
& = x^2 -6x + 10 + 26x^{-1}-24x^{-2}
\end{split}
$$As this contains terms with negative powers, we know that this is not a valid polynomial. We actually know this without even expanding the brackets as we know one term of the numerator is $-1\times 2\times-3\times-4=-24$ and so $-24x^{-2}$ must be a term of the expanded expression. 
### Question 4
**Question:** What is the coefficient of $x^2$ in the polynomial formed by expanding $(2x+2)(2x-2)(x+1)^2$?

**Answer:** We can find out by simplify the expression like so $$
\begin{split}
(2x+2)(2x-2)(x+1)^2 
& = (4x^2 - 4)(x^2 + 2x + 1) \\
& = (4x^4 - 4x^2 + 8x^3 - 8x + 4x^2 - 4) \\
& = 4x^4 + 8x^3 - 8x - 4
\end{split}
$$As we can see no $x^2$ term, we know the coefficient of the $x^2$ term must be $0$.
## Question 5
**Question:** Which of the statements below is always true?

**(a)** For every fixed degree $k\geq 2$ there is **some** degree $k$ polynomial with coefficients chosen from the Real numbers, which has no Real roots.

**Answer:** False. Every polynomial with an **odd** degree has at least 1 real root. So $k=3$ is a counter example.

**(b)** Every polynomial of degree 3 or higher has at least one root belonging to the Real numbers.

**Answer:** False. Even degree polynomials, are not guaranteed to have any real roots. You can derive a degree 4 polynomial which has no real roots by multiplying 2 degree 2 polynomials with no real roots. So $(x^2+1)(x^2+2)$ is a counter example.

**(b)** Every **even** degree polynomial has an **even number** of Real roots.

**Answer:** False. $x^2$ is an even degree polynomial which only has 1 root, 0. This is labelled wrong on canvas as a true statement. 

**(c)** If $p(x)$ is a degree $k$ polynomial all of whose coefficients are **non-zero** and $q(x)$ is a degree $t$ polynomial all of whose coefficients are non-zero then the degree $k+t$ polynomial also has every one of its coefficients as non-zero values.

**Answer:** False. Choose $k=1$ and $t=1$, $p(x)=x+1$, and $q(x)=x-1$. $p(x)\cdot q(x)= x^2-1$. The coefficient of the $x$ term of this polynomial is 0, and so this is a counter example. 

**(d)** If 0 is a root of a polynomial $p(x)$ then the coefficient of $x^0$ in this polynomial is 0.

**Answer:** True. We know that if $r$ is a root of a polynomial that $(x-r)$ is a factor of that polynomial. This means that $(x-0)=x$ is a factor of $p(x)$. This means that $p(x)=x\cdot q(x)$ where $q(x)$ is some other polynomial.

As $p(x)$ is the result of multiplying every term of $q(x)$ by $x$, the $x^0$ term of $q(x)$ will become an $x^1$ term meaning that there will be no $x^0$ term.

**(e)** Any degree $k$ polynomial, all of whose coefficients are identical integers has a root belonging to the Reals.

**Answer:** False. $x^2 + x + 1$ has no real roots.
## Question 6
Consider the following identities:$$
\begin{split}
1567 = 1\cdot10^3 + 5\cdot10^2 + 6\cdot10^1 + 7\cdot10^0 \\
3791 = 3\cdot10^3 + 7\cdot10^2 + 9\cdot10^1 + 1\cdot10^0
\end{split}
$$Now consider the two degree 3 polynomials$$
\begin{split}
p(x) = x^3 + 5x^2 + 6x^1 + 7 \\
q(x) = 3x^3 + 7x^2 + 9x^1 + 1
\end{split}
$$
**Question:** What is the relationship between the digits of the integers (in the left hand sides of the identities) and the coefficients of $p(x)$ and $q(x)$?

**Answer:** The coefficients of $p(x)$ correspond to the digits of 1567 and the coefficients of $q(x)$ correspond to the digits of 3791.

**Question:** Calculate the product $p(x)\cdot q(x)$. How do coefficients of this product relate to the process of multi-digit multiplication (e.g., $1567 \cdot 3791$)?

**Answer:** 1. When expanding $$(x^3 + 5x^2 + 6x+7)(3x^3+7x^2+9x+1)$$we go through the normal process of multiplying $x^3 \times (3x^3+7x^2+9x+1)$, repeating for the other terms of the left bracket, and then summing them. 

If we complete the full multiplication we get $$5x^6 + 9x^5 + 4x^4 + 0x^3 + 4x^2 + 9x^1 + 7x^0$$
The coefficients of this polynomial correspond to the the digits of $$1,567\times3,791=5,940,497$$
If you reflect on any individual step, such as $x^3 * (3x^3+7x^2+9x+1)$, you can see the coefficients of the result $$3x^6+7x^5+9x^4+x^3+0x^2+0x^1+0x^0$$correspond to the result of multiplying $1\cdot10^3$ by $3791$, and so on for all other place values.

**Question:** What does this suggest about the the connection between "school" addition method (place-value arithmetic) and the process of multiplying two polynomials?

**Answer:** This suggests that the process of multiplying polynomials, is almost identical to place-value multiplication. The only real difference is that instead of the place values we use the various degrees of $x$.
## Question 7
The previous example used polynomials with coefficients in the set $\{0,1,2,...,9\}$. Now, consider the set of polynomials $\mathbb{Z}_m[x]$, where coefficients are drawn from $\{0,1,2,...,m-1\}$ for a natural number $m\geq 2$.

**Question:** How would you represent the binary value **1001010** as a degree-6 polynomial $p(x)$ in $\mathbb{Z}_2[x]$?

**Answer:** $$p(x) = 2^6 + 2^3 + 2^1$$
**Question:** How would you represent the octal value **6723** as a degree-3 polynomial $q(x)$ in $\mathbb{Z}_8[x]$?

**Answer:**$$
q(x)=6\times8^3 + 7\times8^2 + 2\times8^1 + 3\times8^0
$$

**Question:** The octal value **6723** corresponds to the binary value **110111010011**. What does this indicate about expressing an octal value as a polynomial in $\mathbb{Z}_2[x]$ versus $\mathbb{Z}_8[x]$? What would the degree of this binary polynomial be?

**Answer:** The degree of the binary polynomial for 110111010011 would be 11. This indicates that, if we call label the degree of any given octal d, that the corresponding binary polynomial will have a degree of $3d+2$. This is because 3 digits in binary correspond to 1 digit in octal, and as a one digit octal value has a polynomial with a degree of 0, we must add $3-1=2$ to get the right value for the degree. 

There are 2 exceptions to this, which are when the most significant digit of the octal value is $<4$ and $\leq 2$ as this would only require 2 digits to represent in binary, and if it is <2 it would only require 1. 

If we label the number of digits required to represent the most significant octal digit as $m$ the actual formula for the degree of the corresponding binary polynomial is $3d+m-1$.

**Question:** Many applications (cryptography, scientific simulations) involve quantities with thousands of bits. Because machine word sizes are limited (rarely exceeding 128 bits), standard hardware-level arithmetic cannot process these numbers in a single step.  
- What is the only option for performing arithmetic on such large numbers?  
- Why might "standard school methods" (long multiplication) be problematic or inefficient for numbers with many thousands of bits?

**Answer:** To handle large scale arithmetic we can represent the binary number as a polynomial representing the same number in higher base counting system, and then perform the arithmetic on the coefficients of this polynomial. As the degree of this polynomial will be much lower than the degree of the binary polynomial this allows us to perform arithmetic on these numbers. 

Standard school methods, would have to sum together thousands of results of multiplications, where as using a number system with a higher base allows us to sum far fewer results.

**Question:** Given the connection between base-$m$ representation and polynomials in $\mathbb{Z}_m[x]$, what does this suggest as an alternative approach for multiplying very large numerical quantities?

It suggests that we can use multiplication of polynomials in order to represent multiplications between numbers from a higher base counting system, in order to reduce the number of operations we must perform.
## Question 8
**Question:** Root finding methods are one specialized subarea of algorithmics and are important tools within optimization approaches. Briefly comment on why the following polynomial attributes may be important to the performance of general root finding methods.

**(1)** The polynomial degree.

**Answer:** Different polynomial degrees have different maximum and minimum number of roots. Specifically simple polynomials have formulas, while more complicated polynomials have to use some kind of trial and error method.

**(2)** The number type of coefficients, $\mathbb{H}$ (can be $\mathbb{Z}$, $\mathbb{Q}$, or $\mathbb{R}$).

**Answer:** Depending on the number type of coefficients, it affects the possible number types of the roots.
## Question 9
**Question:** Suppose that $p(x)$ is a polynomial whose degree is $k$ with $k\geq 3$. Suppose, further, that we can find two distinct Real values, $a$ and $b$, for which $p(a)$ < 0 and $p(b)>0$.

**(a)** What does this allow us to deduce about one root of $p(x)$

**Answer:** We know that one root of $p(x)$ must be a real number in the interval $(a, b)$.

**(b)** Describe (ideally using pseudo-code or Python code) how the fact that $p(a)$ < 0 and $p(b)>0$ can be used in an algorithm to find either an exact root of $p(x)$ (that is a value $c$ for which $p(c)=0$ or, at worst an arbitrarily good approximation to an exact root (that is, a value $c$ for which, although we may have $p(c)\neq 0$ we can make $|p(c)|$ as “small as desired”, e.g. $<10^{-5}$ or $<10^{-30}$ etc.)

**Answer:** 
```
set min = a

set max = b

While p(mid) /= 0 OR |p(mid)| is not as small as desired then
    set mid = (max+min)/2
    if p(mid) > 0 then
         set max = mid
    else if p(mid) < 0 then
         set min = mid
    endif
endwhile

output mid
```

**(c)**  Having found (or found a “good enough approximation to”) one root, $c$, of a degree $k$ polynomial, $p(x)$, how could we use this information to find other (Real) roots of $p(x)$? 

Hint: Look at pages 33-37 of the recommended course textbook.

**Answer:** You can divide the polynomial by $(x-c)$, as $(x-r)$ is a factor of $p(x)$ if $r$ is a root of $x$.

**(d)** There are (at least) three difficulties that might arise when trying to find other roots of $p(x)$. Describe (in informal terms) two such difficulties.

**Answer:** If the root is an approximation, it may be difficult to find others by dividing. The found root may not easily factor out of the given polynomial.

**(e)** In principle, the thinking underlying part (a) could be applied to find zeros (as they are called) of arbitrary Real valued functions, e.g. $f(x)=sin^2(x)$. Why might it be the case that such an approach would fail despite having found $a$ and $b$ with $f(a) < 0$ and $f(b) > 0$? 

Hint: Consider the function $f(x)=\frac{x-1}{x}$ with choices $a=0.5$ and $b=-0.5$ as well as the choice $a=0.5$ and $b=1.5$.

**Answer:** The graphs of these **non-polynomial** functions may not be connected in a continuous way.