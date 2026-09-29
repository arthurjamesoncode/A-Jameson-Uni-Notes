## Binary Addition
Binary addition is the same as decimal additions, except we now only have 2 symbols.

When we add 2 numbers in decimal, we add the corresponding digits and if the sum is greater than or equal to 10 we carry the one to the sum of the next digits.

Binary addition is the same, except now, when we add the corresponding digits, we have to carry the one if the sum is greater than or equal to 2.

You see how it works below:
![[binary_addition.png]]
## Half Adder
A half adder is a type of circuit that can add 2 bits together. It takes 2 bits as input and returns 2 bits. The bits it returns are a carry and a sum.

It is called a half adder as it does not take in a carry bit, and therefore can only be used for the first step in the addition.

Below you can see the half adder circuit:
![[half adder.png]]
The formula for this circuit is this $$
Sum=(P\lor Q)\land\lnot(P\land Q),\; Carry=(P\land Q)
$$
The truth table for the half adder circuit is as follows:

| $P$ | $Q$ | $Sum$ | $Carry$ |
| --- | --- | ----- | ------- |
| 1   | 1   | 1     | 0       |
| 1   | 0   | 0     | 1       |
| 0   | 1   | 0     | 1       |
| 0   | 0   | 0     | 0       |

>You may notice that $(P\lor Q)\land\lnot(P\land Q)\equiv P\oplus Q$. You don't need to recognise this but XOR gates can be used to simplify these circuits a bit.

## Full Adder Circuit
The full adder circuit is actually made up of two half adders.

The formulas for a full adder are$$
Sum=(P\oplus Q)\oplus C_{in},\; Carry=((P\oplus Q)\land C_{in})\lor(P\land Q)
$$
Try drawing the circuit from those formulas as an exercise.

The truth table for this circuit is below

| $P$ | $Q$ | $C_{in}$ | $S$ | $C_{out}$ |
| --- | --- | -------- | --- | --------- |
| 1   | 1   | 1        | 1   | 1         |
| 1   | 1   | 0        | 0   | 1         |
| 1   | 0   | 1        | 0   | 1         |
| 1   | 0   | 0        | 1   | 0         |
| 0   | 1   | 1        | 0   | 1         |
| 0   | 1   | 0        | 1   | 0         |
| 0   | 0   | 1        | 1   | 0         |
| 0   | 0   | 0        | 0   | 0         |
Because full adders take in a carry they can be chained together to add full $n$-bit numbers together. Look below for a figure on how a 4 bit adder works.
![[4_bit_adder.png]]
## Two's Complement
Typically a fixed number of bits is used to represent integers, something like 8, 16, 32, or 64 bits.

Unsigned integers can take all the space available, however signed integers require us to use a leading bit for a sign, to indicate positive or negative.

It may be tempting to assume that if we use a sign to indicate positive and negative numbers that $00000001_2 = 1_{10}$ and $10000001_2=-1_{10}$, but if that were true then $10000000_2=-0_{10}$. We can't have negative 0, and this way makes adding things very strange so surely we can find something better.

Enter "two's complement" this is a way to efficiently represent negative numbers by computer.

Let $[0,0,0,0]$ be a 4-bit bit string representation of a unsigned integer. In this case, each bit, moving right to left, represents increasing powers of 2. So the place values are actually $[8,4,2,1]$.

So $[1,1,1,1]$ is 15, $[0,0,0,1]$ is 1, $[1,0,0,0]$ is 8, and so on.

If instead $[0,0,0,0]$ represents a signed integer we now change the place values. They are still increasing powers of 2 moving from right to left, but now most significant bit is negative. So now the place values are $[-8,4,2,1]$.

So now $[1,1,1,1]$ is -1, $[0,0,0,1]$ is still 1, $[1,0,0,0]$ is -8, and so on.

If we break it down further $[1,1,1,1]$ becomes the sums of their place values $(-8)+4+2+1$, which gives us $-1$.

Essentially to represent $-a$ in 4 bits what we actually represent is $2^4-a$. This can be generalised to $2^n-a$ for n-bit signed integers.
## Properties of Signed Numbers
All signed numbers follow the following properties
- Positive numbers start with 0
- Negative numbers start with 1
- 0 is always represented as a string of zeros
- -1 is always represented as a string of ones
- The number range is split exactly evenly between negative and non-negative numbers.
- The range of numbers we can represent in n-bits is $-2^{n-1}$ to $2^{n-1}-1$.

Look at the following example for 4 bits.
![[twos_complement.png]]
You can see here that if you go right starting from 0 then you are just counting up in regular binary to 7, before it swaps to negatives. 

If you start from 0 and go left you start to count down until you reach -8 before it swaps to positives. If you're struggling to understand why all 1s is to the left of all 0s, think of the number 10000. If you count back once from 10000 you get 9999. It's a bit different since both 10000 and 9999 are positive and 10000 has a leading 1, but the idea is that you go from all 0s to all the highest digit in the number system.
## Operations with Signed Integers
Two's complement is very easy for computers to understand. In fact one of it's main benefits is that it allows the same circuits we had for adding to subtract.

Imagine we are adding $2$ and $3$ in binary. That is the same as adding $0010$ and $0011$. If you do that we can see the results comes out as follows:
![[2+3_bin.png]]

Now lets add 2 negative numbers, $-1$ and $-3$. Their 4-bit strings are as follows, $1111$ and $1101$ and their binary addition looks like this:
![[-1+-3_bin.png]]
The answer achieved here $1100$ is the correct binary number. Remembering the place values $[-8,4,2,1]$, $1100$ is the same as $(-8)+4+0+0=-4$.

We can see that this is correct but you may notice that there is a carry off the end. The result of the standard addition of these 2 binary numbers would be $11100$ but we ignore the carry, for the exact reason why check the section below.

We can also process subtraction by just adding a single negative and positive number together. For example, $4$ and $-3$. You can see the result of this addition below:
![[4-3_bin.png]]
We can see that result is $0001$ in binary or $1$ in decimal, which we know to be correct. Again you can see that this generates a carry that would transfer into the 5th bit but that we ignore it.
### Why We Ignore The Carry
When we add two negative numbers together in standard decimal, $-a$ and $-b$, what we are actually calculating is $-(a+b)$. For example if we take $a=-5,\;b=-2$ when we add them to get $-7$ we are actually getting $-(5+2)$.

So when we add 2 two's complement numbers together we are adding a representation of $-a$ and $-b$ and we want to end up with a representation of $-(a+b)$. If the twos complement of $x$ is $2^n-x$ then we want to add $(2^n-a)+(2^n-b)$ and end up with $(2^n-(a+b)$.

But if we actually compute $(2^n-a)+(2^n-b)$ for some integers $a$ and $b$, we will get $(2^n-a)+(2^n-b)=2^{n}+(2^{n}-(a+b))$. So when we actually compute it we have an extra $2^n$ that we need to get rid of. The value of the carry bit is $2^n$ and so we ignore it.

We also ignore the carry when we add one positive number and one negative number.

Let $a,b\in \mathbb{Z^+}$. Imagine we add the binary representation of $a$ and the binary representation of $-b$. This is the same as $a+(2^n-b)$. Now the result of this is either going to be negative or non-negative. Negative if $a<b$ and non-negative if $a\geq b$.

Case 1, $a<b$:
	In this case $(2^n-b)+a\leq2^n$, and $a-b<0$.
	Since $(2^n-b)+a\leq2^n$ there will be never be a carry into the $(n+1)th$ position.
	Since $a-b<0$ we will represent it as $2^n-(a-b)$.
	Observe that $2^n-(a-b)=(2^n-b)+a$, and so when $a<b$ adding the positive and negative representations simply works.

Case 2, $a\geq b$:
	In this case $(2^n-b)+a\geq2^n$, and $a-b\geq 0$.
	Since $a-b\geq 0$ can just represent it as the binary for $a-b$.
	Since $(2^n-b)+a\geq2^n$ it has definitely generated a carry into the $(n+1)th$ position.
	Since $2^n+a-b-2^n=a-b$, we can see that we can safely ignore the carry bit.

So we can see that whenever we generate a carry bit into the $(n+1)th$ position we can safely ignore it.

If you want a simpler way to understand everything I have just shown, know that it works this way because two's complement addition is actually addition modulo $2^n$. You don't need to know exactly what this means, but you should understand that we can ignore the carry bits.
### Overflow
Take the 4-bit binary representations of 4 and 5, $0100$ and $0101$. You can see the result of adding these below.
![[overflow.png]]
While the result of this is $9$ is unsigned 4-bit binary, in signed binary this is $-7$. This is because overflow has occurred. 

If you have a 3-bit string to show the size of a number and 1 sign bit, you can only represent $2^3$ non-negative numbers $(0\to7)$, and $2^3$ negative numbers $(-1\to-8)$. If you have a sum that exceeds these values, you will get an overflow.

As we saw $5+4=9$, $9$ is too large to fit in the $0\to 7$ range we have available and so we got an overflow, resulting in an incorrect sum.

Similarly if we added $-5$, $1011$, and $-4$, $1100$, you would get $10111$ (23 in unsigned binary), however since ignore the carry bits we would just get $0111$ in signed binary which is $7$. Again because an overflow has occurred.
#### Testing for Overflow
Overflow is a problem when it goes undetected so we need to be able to recognise it.

If the two numbers being added have different signs, there will never be an overflow as the number will be getting closer to 0.

If the two numbers being added have the same sign, an overflow will have occurred if the of the result is different.
### An Algorithm to get the Two's Complement of a Number
So twos complement represents $-a$ as $2^n-a$. In order to get to the twos complement of a number there is a simple algorithm you can follow.

For the following example, let $n=4,\; a=5$:
- Start with the binary representation of $a$, $0101$.
- Flip all of the bits of $a$ (also called performing a **bitwise not** operation), $1010$.
- Add 1 to the flipped version of $a$, $1011$.

So this computes the two's complement of a number, but why does it work?
- This relies on the fact that $2^n-a=2^n-1-a+1=((2^n-1)-a)+1$
- $2^n-1$ in binary is always an n-bit string consisting of all 1s.
- Subtracting any number $a$ from an n-bit string consisting of all 1s is the same as performing a **bitwise not** on $a$. 
- So to calculate $((2^n-1)-a)$ in binary you just can just flip all the bits in $a$.
- Then to find $2^n-a$ you simply need to add 1.

Observe as well that $2^n-(2^n-a)=a$. So in order to find the binary value of a number given it's two's complement, you can simply perform this same two's complement algorithm on that two's complement. 

## Integer Types in High Level Languages
There are many integer data types in high level languages, a lot of modern languages may simplify it to just "Number" or similar (often implemented with linked lists or similar so that they can be of arbitrary size) but the older high level languages had a bunch of specific data types for integers with specific bit sizes.

For example, Java has the following integer data types, all implemented with 2's complement:
- **byte, 8-bit -** $-128\to+127$
- **short, 16-bit -** $-32768\to+32767$
- **int, 32-bit -** $-2147483648\to+2147483647$
- **long, 64-bit -** $-2^{63}\to+2^{63}-1$
## Floating Point Numbers
It is not always possible to express numbers in integer form. 

Real, or floating point, numbers are used in a computer when:
- The number is outside of the integer range of the computer. For example $3.6\times 10^{40}$ or $1.6\times 10^{-19}$
- Or when the number contains a decimal fraction, like $123.456$

In decimal, scientific notation, or standard form, refers to when we indicate numbers by $their\; digits \times 10^x$. We place a decimal point after the first digit, and then the power of 10 we select moves the decimal point back to where it should be.

Take $123.456$ for example. In scientific notation, we would write this number as $1.23456\times 10^2$.

This is similar to how we represent floating point numbers in binary.

Take the binary number $10.01_2$ this is the same as:
- $=1\cdot2^1 + 0\cdot2^0 + 0\cdot2^{-1} + 1\cdot2^{-2}$
- $=1\cdot 2 + 1\cdot 0.25$
- $=2.25_10$

So in a binary scientific representation $10.01_2=1.001\times 2^1$.

>In binary, for any non-zero number, the leading digit is always 1.

Floating point numbers in binary are made up of the following:
- The sign bit of the number
- The sign bit of the exponent
- The magnitude of the exponent, which power of 2 we will be multiplying by.
- The magnitude of the number, which we call the mantissa or significand.

For example, if we had 8 bits we could have S EE MMMMM where:
- S is the sign bit
- The first E is the sign of the exponent
- The second E is the magnitude of the exponent
- The Ms are the bits reserved for the mantissa.

### IEEE 754
IEEE 754 is a standard for floating-point arithmetic. It is implemented in many hardware units and stipulates levels of precision for computer representation of numbers.

It specifies the following datatypes:
- 16 bit **half precision** numbers: 5 for exponent, 11 for mantissa 
- 32 bit **single precision** numbers: 8 for exponent, 24 for mantissa 
- 64 bit **double precision** numbers: 11 for exponent 53 for mantissa
- 128 bit **quadruple precision** numbers: 15 for exponent 113 for mantissa 
- 256 bit **octuple precision** numbers: 19 for exponent 237 for mantissa