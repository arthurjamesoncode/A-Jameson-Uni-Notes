## What is an Algorithm?
An algorithm is a sequence of precise and concise instructions that guide a person or computer to solve a specific problem in a finite amount of time.

Algorithms have an input, which is acted upon, and before some output is generated.

Examples from daily life include:
- Cooking recipe - Input: Ingredients and cooking tools/appliances - Output a cooked meal 
- Furniture assembly guide - Input parts - Output furniture

Algorithms are free from grammatical rules, meaning the content of an algorithm is more important than its form. As long as it explains how to perform the task it's acceptable.

Programs must follow some syntax rules, meaning the form is important. Even if the idea is correct, it is not acceptable for there to be syntax errors.
## Pseudo Code
Pseudo code is a way to write algorithms that borrows from the kind of structures and syntax we see in programming languages, without being bound to them.

Essentially, it is a bit more structured than just saying an algorithm in plain English, but doesn't need to conform to any specific syntax as long as it is readable by a human.

Consider the following algorithm to find the $n$-th power of a number $x$, written in plain English.

Input: a number number $x$ and a non-negative integer $n$
Output: the $n$-th power of $x$
Algorithm:
1. Set a temporary variable $p$ to 1 
2. Complete the multiplication $p\times x$ and store the result in $p$
3. Repeat step 2 $n$ times.
4. Output the result $p$.

This is a simple program that can be implemented in many different programming languages. We can also write a version in pseudocode.

It could look something like this:
```
p = 1 
for i = 1 to n 
	p = p * x
output p
```

The exact specifics of what you use don't matter. All that matters is that a human can read it. For example instead of the assigning equals, you can use `←` or instead of `p * x` you can write `p times x`.

While we do use a for loop, which is a structure we know from programming languages, there is no syntax, only logic.

If you were to write this program in a programming language the syntax would be very important. The code would not run unless it follows the specific rules set out by the language.

If typing a pseudo code algorithm, I recommend using some kind of monospace font. This is obviously optional but makes it easier to read pseudocode in general, as all letters take up the same amount of space.
### Control Flow
We need to control the flow of our algorithms in various ways. We know many of these constructs from programming languages already.

Before we get into the exact types of control flow we use when writing pseudocode (or when writing in an imperative programming language), we need some way indicate when our blocks of code start an end.

There are a many ways to do this, and you can use whichever one feels the best to you. The one thing I recommend is choosing one that is very explicit about when blocks start and end. All of the examples I am showing are good.

```
begin
	<statement1>
	<statement2>
	.
	.
	.
end
```

OR

```
{
	<statement1>
	<statement2>
	.
	.
	.
}
```

I recommend using the first one or similar, and also specifying which type of block you are beginning or ending. Whatever one you use, you should indent code in the same block to the same degree, to make your code easy to read.

The style I use does not use begin, as that is implied by the start of the block but does say `end` followed by the type of block it is ending, such as `endif` or `endfor`. You can see examples of this below.
### `if-then-else`
`if` statements, or `if-then-else` statements, check a Boolean condition and then, if the condition is true, execute some statements in the `if-then` block. If the condition is false, it will instead execute statements in the `else` block.

```
if <condition> then
	<statement>
else
	<statement
endif
```

### `for-loop`
For loops execute some code for every item in some set. This can be every item in a list, or every value in a certain range. You can see examples of this below.

```
for <variable> ← <value1> to <value2> do
	<statement>
endfor
```

OR

```
for <variable> in <set or list> do
	<statement>
endfor
```
### `while-loop`
While loops execute some code while a certain condition is true. When writing while loops, it is important to make sure that the statement the while loop executes moves the condition closer towards truth. If this doesn't happen, the while loop will become an infinite loop.

```
while <condition> do
	<statement>
endwhile
```
### Loop Example
Now let's look at an example of how we could write a pseudo code algorithm to find the sum of the $n$ positive numbers. We can do this with both a for loop and a while loop

`for-loop`
```
sum = 0

for i = 1 to n
	sum = sum + i
endfor

output sum
```

`while-loop`
```
sum = 0
i = 1

while i <= n do
	sum = sum + i
	i = i + 1
endwhile

output sum
```

To check that our algorithm does what we want it too, we can can use a **trace table** to see what the values are at each time. 

Below is the trace table for when $n=6$.
![[sum_trace_table_n6.png]]
## Determining What Algorithms Do
We will now look at some example algorithms and determine what they are doing.

Note that the `%` operator is called modulo, and determines the remainder of a division. So `a % b` gives the remainder when `a`is divided by `b`. This is needed for the first 2 examples.

We also use `==` to denote equality and `!=` or `/=` to denote that things aren't equal. AND, NOT and OR, function like normal Boolean operators.
### Example 1
Consider the following pseudo code algorithm. What is it computing? 

Suppose `0 < x < y` and both `x` and `y` are integers.
```
i = 1

while i <= x do
	if x % i == 0 AND y % i == 0 then
		output i
	endif
	
	i = i + 1
endwhile 
```

To do this we can either just look at the code and attempt to determine what it is doing or use a trace table to determine the outputs and then try and understand what the outputs are.

If we read the code we can see that the code checks whether
```
if x % i == 0 AND y % i == 0
```
for all values of `i` between 1 and `x`, which the smaller of our two integers, and then outputs `i` if our condition is true.

This condition checks whether the remainder of dividing `x` by `i` and the remainder of dividing `y` by `i` are both 0. This is the same as saying whether `i` is a factor of both `x` and `y`. Since the program runs for all values `i` from 1 to `x`, and `x` is the smaller of our two integers, we know that this program outputs all of the common factors of `x` and `y`.

If you don't understand what a program does just be reading it you can fill out a trace table, look at what it outputs and then try to see any patterns. You can then verify this by checking the program.

For example, when `x=4, y=12`:
![[cf_trace_table_4-12.png]]
Or when `x=6, y=15`:
![[cf_trace_table_6-15.png]]
### Example 2
Consider the algorithm below. What is it computing

Suppose `0 < x < y` and both `x` and `y` are integers.
```
i = x
found = false

while i > 1 AND NOT found do
	if x % i == 0 AND y % i == 0 then
		found = true
	else
		i = i - 1
	endif
endwhile

output i
```

Here our loop checks whether 2 conditions are both true. `i > 1` and `NOT found`. `NOT found` is true when `found == false`. This means that our loop run as long as found, which we call a flag variable, is false and `i` has a value greater than `1`.

Inside the loop we check `x % i == 0 AND y % i == 0` and if it is true we set our `found` flag to `true`. Otherwise, we decrement `i` by 1. Since when `x % i == 0 AND y % i == 0` is true we set our `found` flag to `true`, this means that when `i` is a common factor of both `x` and `y` we exit the while loop. 

This means that, since we then output `i`, our output is the first number we encounter that is a common factor of `x` and `y`.

Since we start at `i=x` and end after `i=1` and `0<x<y`, we check every number which could be factor of both `x` and `y`. As 1 is a common factor of all integers, it always outputs 1 if it finds no other common factors.

So this program find the **highest common factor** of two integers.

