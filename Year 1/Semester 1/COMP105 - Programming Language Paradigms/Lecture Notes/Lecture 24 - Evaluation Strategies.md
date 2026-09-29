## Topics

- Evaluation Strategies
- Laziness and Lists
- The `$` and `$!` operators.
## Evaluation Strategies
There are a few different ways that expressions can be evaluated.
### Strict Evaluation
In strict evaluation, we always apply the innermost functions first.

**For Example:**
```
inc x = x + 1  
square x = x * x

-- So square (inc 2) = (2 + 1) * (2 + 1) = 9
```

The above code evaluated strictly would look something like this:
```
square (inc 2)  
> square (3)  
> 3 * 3  
> 9
```

This is probably the kind of evaluation you are most familiar with if you come from imperative languages.
### Lazy Evaluation
In lazy evaluation, we always apply the outermost function first.

So the above code evaluated lazily would look something like this:
```
square (inc 2)  
> inc 2 * inc 2  
> 3 * 3  
> 9
```

>Haskell evaluates things lazily so this will be our main focus for these lecture notes.

Haskell doesn't compute anything until it needs it for some reason. For example to output it to the console, or to use that result in another computation. 

**For Example:**
```
ghci> let x = 1 + 1  
ghci> let y = x + x  
ghci> let z = y / 2  
ghci> z  
2.0

ghci> let x = 1 + undefined  
ghci> let y = x + x  
ghci> let z = y / 2  
ghci> z  
*** Exception: Prelude.undefined
```

>`undefined` is a constant value that will throw an error whenever it is computed.

We can see this explicitly using the `:sprint` command.

**For Example:**
```
ghci> let x = 2
ghci> :sprint x
x = _

ghci> let y = x + x
ghci> :sprint y
y = _

ghci> let z = y / 2
ghci> :sprint z
z = _

ghci> z  
2.0
ghci> :sprint x
x = 2
ghci> :sprint x
y = 4
ghci> :sprint z
z = 2.0
```

>Notice how GHCI evaluates `x`, `y` and `z` only after they have been used.

If a value has never been used, it is never computed.

**For Example:**
```
ghci> let f x = 1  
ghci> f 2  
1  
ghci> f 3  
1  
ghci> f undefined  
1
```

>Notice how `f undefined` doesn't give the `*** Exception: Prelude.undefined` error.

### Imperative Languages
Imperative languages are always strict because programmers **need** to know the order of side effects.

**For Example in Python:**
```
def inc(x):  
	print "hi from inc"  
	return x + 1
	  
def square(x):  
	print "hi from square"  
	return x * x
	  
>>> print square(inc(2))  
hi from inc  
hi from square  
9
```

>Observe how the `"hi from inc"` message is printed first.
### Functional Languages
For pure functions the order of evaluation is not important, as you will always get the same answer and there are no side effects to worry about.

There are functional programming languages that are strict by default, such as ML and Ocaml, but there are also languages that are lazy by default, like Haskell.

### Lazy vs Strict
If strict evaluation finds an answer, lazy evaluation will find the same answer, but sometimes lazy evaluation can find an answer that strict evaluation can not.

**For Example:**
```
ghci> fst (1, 1 `div` 0)  
1
```

Strict evaluation would crash on this example as you cannot divide by 0.

Sometimes lazy evaluation can be more efficient than strict evaluation, particularly is some values are computed and never used as lazy evaluation only computes a value when it is needed.

**For Example:**
```
ghci> head (map (*2) [1..100])
2

ghci> head (map (*2) [1])
2
```

Both of those examples are exactly as efficient as each other since all Haskell computes is `2*1`.
## Lists
Lists are never evaluated until they are needed.

**For example:** 
```
take 2 [1..100]  
> 1 : take 1 [2..100]  
> 1 : 2 : take 0 [3..100]
> 1 : 2 : [] -- this is because take include `take 0 _ = []` as a base case
> [1,2]
```

So `take 2 [1..10]` and `take 2 [1..10000]` are the same efficiency.

To show this we can use `:sprint`.

```
ghci> let x = [1..10]
ghci> let y = [1..1000]

ghci> :sprint x
x = _
ghci> :sprint y
y = _

ghci> take 2 x
[1,2]
ghci> take 2 y
[1,2]

ghci> :sprint x
x = 1:2:_
ghci> :sprint y
y = 1:2:_
```

### Infinite Lists
Laziness allows for infinite lists

**For Example:**
```
all_1s = 1 : all_1s
 
ghci> take 4 all_1s  
[1,1,1,1]
```

>`all_1s` is the same as `[1,1..]`

We can perform computations on infinite lists **because** of laziness.

**For Example:**
```
all_1s = 1 : all_1s  
all_2s = zipWith (+) all_1s all_1s

ghci> take 4 all_2s  
[2,2,2,2]

numbers n = n : numbers (n+1)  
ghci> take 10 (numbers 0)  
[0,1,2,3,4,5,6,7,8,9] 

even_numbers = filter even (numbers 0)
ghci> take 10 even_numbers  
[0,2,4,6,8,10,12,14,16,18]
  
sieve (x:xs) = x : filter (\y -> y `mod` x /= 0) (sieve xs)  
primes = sieve [2..]
  
ghci> take 10 primes  
[2,3,5,7,11,13,17,19,23,29]  
ghci> primes !! 1000  
7927
```

## `$!` and `$`
Recall that `$` is used to evaluate functions. Well `$!` evaluates functions strictly.

This is something you won't notice for most code but it can change inputs and have efficiency boosts.

**For Example:**
```
func a b = if a then b else 0  
ghci> func False $ (error "error")  
0  
ghci> func False $! (error "error")  
*** Exception: error
```

>For an example of how it can be used to boost efficiency look ahead to the next lecture: [[Lecture 25 - Tail Recursion]].

