## List Ranges
A list range is a way to write a long list in a compact way. It uses the syntax
```
[<start>..<end>]
```
where start and end have some way of iterating between them.

So for example:
```
ghci> [1..20] 
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20] 

ghci> ['a'..'z'] 
"abcdefghijklmnopqrstuvwxyz" 

ghci> ['K'..'Z'] 
"KLMNOPQRSTUVWXYZ"
```

You can a step size, by indicating the second element of the range.

For example:
```
ghci> [2,4..20] 
[2,4,6,8,10,12,14,16,18,20]
 
ghci> [3,6..20] 
[3,6,9,12,15,18] 

ghci> [20,19..15] 
[20,19,18,17,16,15]
```

## Infinite Lists
You can use this notation to define **infinite lists**. You can pass these lists to functions, this only works because Haskell is lazy, meaning it only evaluates what it needs to. If a function requires the whole list to return a value Haskell will get stuck

For example:
```
ghci> [1..] 
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21... (continues until forced to stop)

ghci> take 5 [1..]
[1,2,3,4,5]

ghci> length [1..]
(will never find a value and will only terminate if forced to)
```

>Note that `take n ls` returns a list made up of the first `n` elements of `ls`

The **repeat** function creates an infinite list made up of it's input.
```
ghci> repeat 5 
[5,5,5,5,5,5,5,5,5,5,...
```

The **cycle** function repeats a list infinitely.
```
ghci> take 10 (cycle "abc") 
"abcabcabca"
```

## List Comprehensions
List ranges only produce simple arithmetic sequences, but list comprehensions can produce more complex lists.

For example:
```
ghci> [x*x | x <- [1..10] ] 
[1,4,9,16,25,36,49,64,81,100] 

ghci> [x / 10 | x <- [2,4..10] ] 
[0.2,0.4,0.6,0.8,1.0]
```

They use the syntax 
```
[<expression using x> | x <- <list>]
```
and create a list of the results of the value of the expression when passed the values from the list.

You can also add **predicates** to the list comprehension, these are comma separated boolean expressions which determine whether the expression gets added to the new list.

For example
```
ghci> [x*x | x <- [1..10], x*x > 40] 
[49,64,81,100] 

ghci> [x*x | x <- [1..10], x*x > 40, x*x < 80] 
[49,64] 

ghci> [x*x | x <- [1..10], 2*x > 10] 
[36,49,64,81,100]
```

List comprehensions can make up the body of a function:
```
evens_less_than y = [x | x <- [0..(y-1)], x `mod` 2 == 0] 

ghci> evens_less_than 10 
[0,2,4,6,8] 

lt10 xs = [ if x < 10 then "Yes" else "No" | x <- xs] 

ghci> lt10 [8..11] 
["Yes","Yes","No","No"]
```

You can also use multiple **sub-lists** in a list comprehension
```
ghci> [ x*y | x <- [2,5,10], y <- [8,10,11]] 
[16,20,22,40,50,55,80,100,110] 

ghci> [ x*y | x <- [2,5,10], y <- [8,10,11], x*y > 50] 
[55,80,100,110]
```

Note that, for list comprehensions which use more than 1 variable, the expression is added for every possible combination of variables from the sub-lists. You can think of it as similar to a nested for-loop in imperative languages.
## Lists of Lists
We have covered lists and list comprehensions but we need to talk about lists of lists.

We have lists of lists. Haskell has no problem with that. The one caveat is that each list contained in a list of list must contain the same type.

So this is perfectly fine:
```
ghci> let x = [[1,2,3],[4],[5,6]] 
ghci> head x 
[1,2,3] 
ghci> tail x 
[[4],[5,6]] 
ghci> length x 
3
```

We can also nest list comprehensions when acting on lists of lists
```
f xxs = [ [ x | x <- xs, even x ] | xs <- xxs] 

ghci> f [[1,2,3],[4],[5,6]]
[[2],[4],[6]]
```
The above code is a function that filters out all the odd numbers from each list contained in `xxs`
## Imperative List Comprehensions
List comprehensions started in the functional programming world, but have appeared in imperative languages.

For example, Python allows list comprehensions
```Python
squares = [x**2 for x in range(10)] 

[x.lower() for x in ["A","B","C"]]
```
