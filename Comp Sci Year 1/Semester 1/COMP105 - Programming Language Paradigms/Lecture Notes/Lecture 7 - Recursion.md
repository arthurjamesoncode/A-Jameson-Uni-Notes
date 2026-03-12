A **recursive** function is one that calls itself.

For example:
```
factorial n = if n > 1
			  then n * factorial (n - 1)
			  else 1
```

A recursive function has:
- A **base case**;
- One or more **recursive rules** that move us closer to the base case.

Take the factorial example, this has a base case of `n` being 1 or lower, in which case it returns 1. Otherwise it has the recursive rule of returning `n` times the factorial of `(n-1)`.

The execution of the **factorial** function looks like this:
```
factorial 4 
→ 4 * factorial 3 
→ 4 * 3 * factorial 2 
→ 4 * 3 * 2 * factorial 1 
→ 4 * 3 * 2 * 1
→ 24
```

## Pattern Matching
When writing recursive functions in Haskell, we can use **pattern matching** to remove the if statement, giving us a nicer syntax.

```
factorial 1 = 1
factorial n = n * factorial (n-1)
```

Haskell matches patterns from **top to bottom**, so in the above example it checks if `n` is 1 before it moves on to the general step. This means that your **catch-all** case must come last.

```
sayMe 1 = "One!" 
sayMe 2 = "Two!" 
sayMe 3 = "Three!" 
sayMe 4 = "Four!" 
sayMe 5 = "Five!" 
sayMe x = "Not between 1 and 5"
```
## Building Recursive Functions
Every recursive function must have a base case:
- This gives a **stopping condition** for the recursion;
- Is usually the simplest case;
- Can be more than 1 discrete cases.

If you do not have a base case, your function will never terminate.

Consider if this was our entire definition for the **factorial function**:
```
factorial n = n * factorial (n-1)
```

This function would never terminate:
```
factorial 2 
→ 2 * factorial 1 
→ 2 * 1 * factorial 0 
→ 2 * 1 * 0 * factorial (-1) . . .
```

Our recursive functions also have **recursive rules** which make progress towards a base case.

This usually means making a numeric argument smaller or bigger, looking at a smaller section of a list or data structure, etc. It simply is a way that moves us towards the base case, whatever that may be.

In the factorial example, our base case is 1 and our input is assumed to be bigger than 1. So our recursive rule passes `(n-1)` to the function, which makes it so we are closer to terminating.

If we make no progress, then we will never terminate

For example:
```
factorial 1 = 1 
factorial n = n * factorial n
```
will result in
```
factorial 2 
→ 2 * factorial 2 
→ 2 * 2 * factorial 2 
→ ...
```
which never terminates.
## Looping
In a functional language like Haskell, recursion is the only way to handle looping.

You can think of a **base case** like the **stopping condition** of a loop, and you can think of the recursive rules as doing the computation.

Everything that can be done with a loop can be done with recursion, but there is not necessarily an easy way to translate code from a loop to recursion.
## Complex Recursive Functions
Recursive functions are allowed to have **multiple base cases**. Each different case represents a different stopping condition.

For example:
```
is_even 0 = True 
is_even 1 = False 
is_even n = is_even (n-2)
```

The above example takes a non-negative integer `n`. If `n` is not 0 or 1 then it recursively calls itself using `(n-2)`. If `n` is 1 it knows the number passed to it was not even and returns `False`, if `n` is 0 it know the number passed to it was even and returns `True`.

There are two base cases here depending on whether the number passed to it was odd or even at the start.

Some recursive functions may have more than one recursive rule.

For example:
```
even_sum 0 = 0 
even_sum x = if x `mod` 2 == 0 
			 then x + even_sum (x-1) 
			 else even_sum (x-1)
```

The above example returns `even_sum (x-1)` when the number passed to it is odd, and returns `x + even_sum (x-1)` when the number passed to it is even.

Exactly what it returns and what needs to be called depends on the input, so this function has multiple recursive rules.

It is very important to make sure that the rules are comprehensive, as there must always be some recursive rule that can be applied (unless we are at one of the base cases).
## Guards
When we have multiple recursive rules we can use **guards** to make our code nicer.

For example:
```
even_sum x 
	| (x == 0) = 0 
	| (x `mod` 2 == 0) = x + even_sum (x-1) 
	| otherwise = even_sum (x-1)
```

The syntax for **guards** is this:
- Each guard has the format `| <test> = <expression>`
- `<test>` is an expression which evaluates to a boolean
- `<expression>` can be anything and will be returned when `<test>` evaluates to true.
- the special case `otherwise` is a catch all

Guards are nice to avoid having many nested ifs.
### Guards Vs Pattern Matching
We have now seen both guards and pattern matching as ways to write recursive functions.

There is no right or wrong answer about which ones to use in a given situation but generally:
- Guards work well when you have conditionals to test
- Pattern matching works well when checking for specific values, or when working with lists/tuples or other types that can be broadly pattern matched.

You can also combine both pattern matching and guards if you so choose, for example:
```
even_sum 0             = 0
even_sum x  
	| (x `mod` 2 == 0) = x + even_sum (x-1) 
	| otherwise        = even_sum (x-1)
```

For readability, I recommend matching your outputs to a function to the same level of white space.
## Tips For Writing Recursive Functions
Understanding how to write a function in a recursive way is something that can be pretty hard at first. Formulating problems in a recursive way is a skill which will be developed on this course. 

Seeing a lot of examples will help, and trying a lot of exercises will also help.

When designing a recursive function think about:
- When do you want to stop? - These times will be your base cases
- How do you make progress towards a base case? - Here you need to consider ways to make your problem smaller. There could be more than 1, and they could depend on certain conditions. These are the recursive rules.

It can helpful to assume that the function already works for a smaller problem.

Consider a function that counts how many `e`s are in a string. If we have the first letter of a string and the rest of the string, we can define a function which either:
- Returns 1 plus the number of `e`s in the rest of the string if the first letter is an `e`
- Or returns just the number of `e`s in the rest of the string if the first letter isn't an `e`.
Which always works assuming our original function works.

If we add in the base case that when the string is empty, there are 0 `e`s in the string, we now have a function which works for the smallest possible case. Since we then designed a function assuming it works for a smaller case, we can combine these to get a function which works for every case.

Consider Euclid's algorithm.

Euclid’s algorithm is an algorithm for finding the greatest common denominator of two numbers `a` and `b`, so `gcd 400 60` is 20
1. if `a > b` then set `a := a - b` 
2. if `b > a` then set `b := b - a` 
3. if `a` is equal to `b` then return `a` 
4. Otherwise go back to step 1 and repeat

In Haskell we can define this as:
```
gcd' a b 
	| a == b = a 
	| a > b = gcd' (a - b) b 
	| b > a = gcd' a (b - a)
```