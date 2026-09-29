This lecture we will start going through Haskell syntax. It is worth noting that Haskell comes with it's own interpreter called `ghci`, which can be used to load programs into and run single lines of code.

```
ghci> 2 + 15 
17 

ghci> 49 * 100 
4900 

ghci> 1892 - 1471 
421 

ghci> 5 / 2
2.5 

ghci> 2^10 
1024

ghci> 2**2.5 
5.65685
```

## Basic Syntax

### Boolean Expressions
Haskell uses the same syntax as **C** for the boolean operations AND and OR, where AND is `&&` and OR is `||`. It uses a function `not` for the boolean operation NOT.

```
ghci> True && False
False 

ghci> True && True 
True 

ghci> False || True 
True 

ghci> not False 
True 

ghci> not (True && True)
False
```
### Equalities and Inequalities
Haskell uses `==` to check if two values are equal and `/=` to check if two values are not-equal. Most programming languages use `!=` for not-equal. Haskell's choice of `/=` is meant to resemble the $\neq$ used in maths.

```
ghci> 5 == 5 
True 

ghci> 1 == 0 
False 

ghci> 5 /= 5 
False 

ghci> 5 /= 4 
True 

ghci> "hello" == "hello" 
True
```

Haskell uses `<` to check if one value is less than another, `>` to check if one value is greater than another, `<=` to check if one value is less than or equal to another. and `>=` to check if one value is greater than or equal to another.

```
ghci> 1 < 2 
True 

ghci> 1 <= 1 
True 

ghci> 100 > 101 
False 

ghci> 10 >= -10 
True
```
### Order of Operations and Brackets
The order of operations in Haskell is as we expect (BIDMAS). 

The following is evaluated in order from first to last:
- Brackets
- Indices
- Division
- Multiplication
- Addition
- Subtraction

So:
```
ghci> (50 * 100) - 4999 
1 

ghci> 50 * 100 - 4999 
1 

ghci> 50 * (100 - 4999) 
-244950
```

It's worth noting that you must place brackets around negative numbers so
```
ghci> 5 * (-3)
-15

ghci> 5 * -3

<interactive>:1:1: error:
    Precedence parsing error
        cannot mix `*' [infixl 7] and prefix `-' [infixl 6] in the same infix expression
```

### Evaluating Functions
Haskell uses a special syntax for function calls where the name of the function is followed by it's arguments all separated by a space

So:
```
ghci> min 9 10 
9 

ghci> min 3.4 3.2 
3.2 

ghci> max 100 101 
101
```

Functions also bind more tightly than any other operator. This means you will often need to bracket your arguments. So:
```
ghci> max 2 1 + 3
5
ghci> (max 2 1) + 3 
5

ghci> min 28 100/4 
7.0 
ghci> min 28 (100/4) 
25.0
```
Notice how the first two are the same but the second two give different outputs.

If a function has two arguments we can make it **infix**. This means we can place it in the middle of it's two arguments, instead of before.

For example:
```
ghci> mod 10 4 
2 

ghci> 10 `mod` 4 
2
```
This can make reading some expressions more natural, especially where the order of the arguments matters.
## Defining Our Own Functions
In the examples above, we've used `ghci` to evaluate predefined functions, for the most part we will program in Haskell by defining our own functions.

We can do this by saving our functions in a file and then loading them into `ghci`. Alternatively we can compile our file and create a runnable `.exe` file. Compilation will be looked at during the IO part of the course, for now we will focus on loading files into `ghci`.

For example, lets write a function which adds 2 to its input:
```
addTwo x = x + 2
```

If we save this function inside a file called `code.hs` and then load it into `ghci`, we can run it with some arguments. We use `:l file.hs` to load our file into `ghci`. Note that to load it successfully we must have either have `ghci` loaded in the same location as our file or provide an absolute file path allowing `ghci` to find our file.

```
Prelude> :l code.hs
[1 of 1] Compiling Main 
Ok, modules loaded: Main.
*Main> addTwo 2
4
```

The syntax for defining a function is
```
function_name arg_1 arg_2 ... = body
```
Where 
- `function_name` must start with a small letter
- all arguments must start with small letters
- `body` is some expression

An **expression** is just a combination of functions. Everything that can be typed into `ghci` is an expression.

Some examples of functions we could define are:
```
addTwo x = x + 2 

addSquares x y = x**2 + y**2 

maxThree x y z = max (max x y) z
```

For a more in-depth example, consider a function which turns a 2 bit binary number, $b_1b_2$ to decimal.

This needs to perform the following operation$$
b_1\times 2^1 + b_2 \times 2^0
$$So 11 in binary becomes $$
1\times 2 + 1\times 1 = 3
$$
In Haskell we can do:
```
bin_to_dec b1 b2 = b1 * 2^1 + b2 * 2^0
```

## Comments
It is often a good idea to comment code, to add detail about why a function is written in a certain way etc.

```
-- single line comments looks like this

f x = x + x -- it can go after code written on the same line

{- Multi line comments look like this
	and can span 
	multiple lines -} 
```

