## `where` Syntax
Sometimes its useful to bind names across a **whole function**. For this we can use the `where` keyword.

`where` is an alternate to `let` which makes its definition available across the whole function not just the `in` block. `where` can bind any number of names and you can do pattern matching in `where` clauses.

For some examples of how you can use `where` look below:
```
remove_twos [] = [] 
remove_twos (x:xs) 
	| x == 2 = rest 
	| otherwise = x : rest 
	where rest = remove_twos xs

initials first last = 
	[f] ++ ". " ++ [l] ++ "." 
	where 
		(f:_) = first 
		(l:_) = last
```

The main difference between `let` and `where` is that `let` is an expression by itself (the `let` expression ends at the end of the `in` block). `where` on the other hand is attached to a function.

`where` can be particularly useful when paired with guards.
## Recursion Across Multiple Lists
Sometimes we will write recursive functions which work on more than just one list.

For example, consider a function which takes two lists of numbers and returns a new list which contains the sums of the corresponding numbers from the lists.

```
add_lists _ [] = [] 
add_lists [] _ = [] 
add_lists (x:xs) (y:ys) = x+y : add_lists xs ys

ghci> add_lists [1..5] [2..7]
[3,5,7,9,11]
```

Note that the base case stops when either of the lists are empty. This means that the resulting list will be the same length as the shorter list and the rest of the elements from the longer list will be discarded.

For another example, consider a function which is meant to test if two lists are equal. 

```
list_equal [] [] = True 
list_equal _  [] = False 
list_equal []  _ = False 
list_equal (x:xs) (y:ys) 
	| x == y    = list_equal xs ys 
	| otherwise = False
```

Notice that we have 4 base cases, 1 for both lists being empty, 2 for either list being empty but not both, and 1 for the first item of each list not being the same.

The function `zip` exists in prelude and combines two lists into a single list of tuples of corresponding elements. You can see an example implementation of this below.

```
zip' [] _ = [] 
zip' _ [] = [] 
zip' (x:xs) (y:ys) = (x, y) : zip' xs ys 

ghci> zip' [1,2,3] ['a', 'b', 'c'] 
[(1,'a'),(2,'b'),(3,'c')]
```

We can also build up multiple lists in the same function, we can use a tuple to return multiple lists. For example, consider a function which splits a list of numbers into the numbers which are greater than 10 and less than or equal to 10.

```
gt_10 [] = ([], []) 
gt_10 (x:xs) 
	| x > 10 = (x:gt, lt) 
	| otherwise = (gt, x:lt) 
	where (gt, lt) = gt_10 xs 
	
ghci> gt_10 [8..12] 
([11,12],[8,9,10])
```
## Mutual Recursion
Mutual recursion is when two functions call each other.

For example we could define 2 functions which together can determine if a number is even.

```
even1 0 = True
even1 n = even2 (n-1)

even2 0 = False
even2 n = even1 (n-2)
```

Just like with normal recursion you must have base cases, and the recursive calls must move us closer to these base cases.

You need to know what **mutual recursion** is, and may need to understand what a mutually recursive function does for one of the class tests.

However mutual recursion is a **stylistic choice** meaning that you can usually avoid it if you want to. You won't be required to write any mutually recursive functions.

The given example is a very bad function, as you can use ``n `mod` 2 == 0`` to get the same effect and it is faster and more readable. So you may be wondering why anyone would ever use mutual recursion if it makes our code worse?

The answer is that it doesn't always make our code worse, but that examples where it makes it more efficient or easier to read are fairly complicated, and this course requires simple examples that which allow you to understand the basics of how mutual recursion works.

One main use I think works very well for mutual recursion is implementations of a **state machine**, and there are many others that you may come across. This section is simply a **disclaimer** that mutual recursion is a useful tool that you should know, but that the examples you see on this course are not its best advocates.

>My solution to the challenge question of the practice final exam actually used mutual recursion to make the solution cleaner and more readable. So it is definitely a useful tool for you to know on this module.
## Multiple Recursion
Multiple recursion is when a function makes more than one recursive call in the same recursive rule.

For example:
```
fib 0 = 0 
fib 1 = 1 
fib n = fib (n-1) + fib (n-2)
```

**Multiple recursion** can make your code very slow as each recursive call can end up doing a lot of the same or similar work.

To calculate `fib 4` this program calculates:
- `fib 3`
	- `fib 2`
		- `fib 1`
		- `fib 0`
	- `fib 1`
- `fib 2`
	- `fib 1`
	- `fib 0`

As you can see it computes `fib 2` twice. This leads to unnecessary computation as we could instead reuse this value after computing it once.

This problem gets especially bad at scale, try running the above code up to `fib 40`. You can see that already, even for a number as small as 40, this code takes a huge amount of time.

To get around this we can create a helper function that computes the whole list up `n` and then return the first value. As the list stores the computed values, they only need to be computed once saving on a LOT of computation time.

```
fast_fib_help 1 = [1, 0] 
fast_fib_help n = 
	x + y : (x:y:xs) 
	where (x:y:xs) = fast_fib_help (n-1) 

ghci> fast_fib_help 10 
[55,34,21,13,8,5,3,2,1,1,0] 

fast_fib n = head (fast_fib_help n)
```
