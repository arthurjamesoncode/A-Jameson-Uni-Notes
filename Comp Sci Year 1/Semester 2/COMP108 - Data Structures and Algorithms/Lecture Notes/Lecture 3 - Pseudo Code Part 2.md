Today we will look at more examples of algorithms that can be implemented in code, and write pseudo code for them.
## Unique Factors
Suppose $x$ and $y$ are both positive integers.

How could we write a while loop that outputs all factors of $x$ which are not factors of $y$.

Below we can see some example results we would want for various values of $x$ and $y$.
![[results_1.png]]

We know that, as we are looking numbers which are factors of $x$ and not factors of $y$ that we will need to check if 
```
x % i == 0 AND y % i /= 0
```
is true, as, if $i$ is a factor of $x$, $x/i$ will give a remainder of 0 and, if $i$ is not a factor of $y$, then $y/i$ will give a remainder that isn't 0. We then output any numbers for which this is true. 

This gives us our output condition, but how do we determine which numbers to check? 

Well as we know they have to be factors of $x$ we know that all the numbers we need to check will be $\leq x$.  We also know that we will never output 1, as 1 is a factor of all positive integers and that all the numbers we output will be positive integers. We can use this to get our **bounds** for which numbers we need to check. Which are 2 and $x$.

We also know that we want to look for ALL factors of $x$ which are not factors of $y$, which means we will want to increment our iterator regardless of whether the condition we check is true or not. We also want to check every number within these bounds as there is not a simple way to move from factor of $x$ to factor of $x$.

There are some ways to optimise this a bit, but this is a good start and all that is necessary for right now.

So now we can write our while loop:
```
i = 2
while i <= x do
	if x % i == 0 AND y % i /= 0 then
		output i
	endif
	
	i++
endwhile
```

We can also do the same logic using a for loop:
```
for i = 2 to x do
	if x % i == 0 AND y % i /= 0 then
		output i
	endif
endfor
```
## Finding Lowest Common Multiple
Suppose $x$ and $y$ are both positive integers and $x<y$

How could we write a while loop that outputs the lowest common multiple, LCM, of $x$ and $y$.

We know that a lowest common multiple has to be divisible by both $x$ and $y$ so we immediately know we will be checking 
```
lcm % x == 0 AND lcm % y == 0
```

Now we need to determine the range of numbers we must check. We know that the LCM of $x$ and $y$ has to be at least the size of $y$ which is the greatest of our two integers, and it will never be more than $x\times y$ as $x\times y$ is always divisible by both $x$ and $y$. 

So now we know the **bounds** of this search space to be $y$ and $x\times y$. If we search this space linearly, starting from the smaller value $y$, and output the first number that satisfies our condition, we know we will output the LCM of $x$ and $y$.

Since we only want to output 1 number, we can use a flag to exit our while loop after we find a single number that satisfies our condition. We also know we only need to move onto the next number if we don't find a number that satisfies our condition. This means we should put the increment in the else clause of our if statement.

We also don't need to check every number in the search space as, unlike when looking for factors, we have a simple way to move from one multiple of $y$ to another. All we need to do is increment in steps of $y$. We can also simplify our condition to
```
lcm % x == 0
```
as we now know for sure that all of the numbers we will check are multiples of y.

So now, we can write the full while loop:
```
lcm = y
found = false

while lcm < x*y AND found /= true do
	if lcm % x == 0 then
		found = true
	else 
		lcm = lcm + y
	endif
endwhile

output lcm
```

## Multiplication Table
Suppose $x$ is a positive integer, how could we write an algorithm to output the multiplication table up to $x$.

For example for $x=4$ we would want to output the items in:
![[4x4_mult_table.png]]

To output this table we want to output $1\times1,1\times2,1\times3,1\times4$ then $2\times1,2\times2,2\times3,2\times4$ and so on. To do this we can **nest** two loops. To do this we need to use 2 variables instead of one.

You can see how to do this below:
```
for i = 1 to x do
	for j = 1 to x
		output i * j
	endfor
endfor
```
