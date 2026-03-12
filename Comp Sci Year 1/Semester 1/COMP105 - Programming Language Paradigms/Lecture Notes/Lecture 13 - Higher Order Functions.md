## Topics

- More Type Classes
- Higher Order Functions
- Function Composition
- Anonymous Functions

## More Type Classes
### Converting to Strings
The `show` function converts other types to strings.

**For Example:**
```
ghci> show 123  
"123"

ghci> show [1,2,3]  
"[1,2,3]"

ghci> show (True, 2.5)  
"(True,2.5)"
```

The `Show` type class contains types that can be shown.
```
ghci> :t show  
show :: Show a => a -> String  
```

Show contains:  
-  all basic types  
-  all tuples containing showable types  
-  all lists that contain showable types

### Converting from Strings
The `read` function converts strings to other types.

**For Example**:
```
ghci> read "123" :: Int  
123

ghci> read "False" :: Bool  
False

ghci> read "[1,2,3,4]" :: [Int]  
[1,2,3,4]
```


The use of `::` is necessary to tell Haskell what type it is parsing.

>Its not necessary to use `::` when Haskell can deduce the type from the context.

```
ghci> not (read "False")  
True
  
ghci> :t not  
not :: Bool -> Bool
 
ghci> read "4" * read "6"  
24

ghci> :t (*)
(*) :: Num a => a -> a -> a
```

>Haskell can deduce the type that `read` must read to from the types that these functions take.

The `Read` type class contains all types that can be read 
```
ghci> :t read  
read :: Read a => String -> a 
```

As with show, it contains: 
- all basic types  
- all tuples containing readable types  
- all lists that contain readable types

### Ordered Types  
The type class `Ord` contains all types that can be compared.
```
ghci> :t (>)  
(>) :: Ord a => a -> a -> Bool

ghci> :t (<=)  
(<=) :: Ord a => a -> a -> Bool
 
ghci> :t max  
max :: Ord a => a -> a -> a
```

It contains numbers, but also all basic types, tuples, and lists
```
ghci> 'a' < 'b'  
True
  
ghci> True > False  
True

ghci> (1, 10) <= (1, 11)  
True

ghci> [1..10] < [2..11]  
True

ghci> [5,4,5] < [5,3,6]
False
```

>Tuples and lists are compared lexicographically (element by element).
>
>We can see from the last example that when compared using `>`, `>=`, `<`, or `<=` the first element with a different value is the one that determines `True` or `False`.

## Higher Order Functions
A **higher order function** is a function that takes another function as an argument, or returns a function.

**For Example:**
```
apply_twice :: (a -> a) -> a -> a  
apply_twice f input = f (f input) 
 
ghci> apply_twice tail [1,2,3,4]  
[3,4]
```

The above function takes a function, which takes a single argument and returns a new value of the same type, and an input, and then applies the given function to the input twice. 

**For Example:**
```
ghci> apply_twice ((+) 2) 2  
6

ghci> apply_twice (drop 2) [1,2,3,4,5]  
[5]

ghci> apply_twice reverse [1,2,3,4]  
[1,2,3,4]
```

>Because the type annotation specifies that the input and output have to be the same, the following will return a type error:
>`ghci> apply_twice head [[1,2], [3,4]]`
>
>This is because head has a type of  `[a] -> a` and not `a -> a`.

## Function Composition
Function composition applies one function to the output of another.

 >Composing f with g input gives f (g input) 

```
compose :: (b -> c) -> (a -> b) -> a -> c 
compose f g input = f (g input)

ghci> compose (+1) (*2) 4  
9  
ghci> compose head head [[1,2], [3,4]]  
1
```

Haskell implements function composition using the `.` operator

```
ghci> compose head head [[1,2], [3,4]]  
1

ghci> (head . head) [[1,2], [3,4]]  
1

ghci> :t (.)  
(.) :: (b -> c) -> (a -> b) -> a -> c
```

>`.` is particularly useful when composing a long list of functions 

```
f list = length (double (drop_evens (tail list)))

f' list = (length . double . drop_evens . tail) list
```

>Both of these do the same but the second is much prettier, as the `.` avoids the need for nested brackets.
>
>However, this is just stylistic and you never **need** to use it. You should though if you want your code to be readable.

### The `$` Operator
The below function just evaluates its input.
```
evaluate :: (a -> b) -> a -> b  
evaluate f input = f input

ghci> evaluate length [1,2,3]  
3
```

The `$` operator is exactly the same as evaluate 
```
ghci> ($) length [1,2,3]  
3

ghci> length $ [1,2,3]  
3

ghci> :t ($)  
($) :: (a -> b) -> a -> b
```

>This operator may seem pointless but is very useful for avoiding brackets.
>
>This is because the $ operator has the lowest precedence of all operators, meaning it will essentially take whatever is to its right and apply it to whatever is to its left.

**For Example:**
```
ghci> length ([1,2,3] ++ [4,5,6])  
6  
ghci> length $ [1,2,3] ++ [4,5,6]  
6

ghci> (length . tail) [1,2,3,4]  
3  
ghci> length . tail $ [1,2,3,4]  
3

ghci> (length . tail) ([1,2,3] ++ [4,5,6])
5
ghci> length . tail $ [1,2,3] ++ [4,5,6]
5
```

## Anonymous Functions
Sometimes it is convenient to define a function inline.

**For example**:
```
ghci> (\x -> x + 1) 2  
3

ghci> :t (\x -> x+1)  
(\x -> x+1) :: Num a => a -> a

ghci> apply_twice (\x -> 2 * x) 2  
8
```

These are called anonymous functions since they have no name.

>You never **need** to use an anonymous function it is again stylistic. 
>
>However, sometimes you need a function to do something within a specific context such as a `map` or `filter` function (covered in the next section), and using an anonymous function is nicer to do than to name a function on a different line.

The syntax for an anonymous function is: 
```
\ arg1 arg2 ... -> expression
```

>The \ is supposed to resemble a lambda (λ). Anonymous functions are sometimes called λ-functions

## More Complex Higher Order Functions
Higher order functions can return other functions.

**For Example:**
```
f_that_adds_n :: Int -> (Int -> Int)  
f_that_adds_n n = (\ x -> x + n)

ghci> let f = (f_that_adds_n 10) in (f 1)  
11
  
ghci> (f_that_adds_n 20) 1  
21
  
ghci> f_that_adds_n 2 . f_that_adds_n 3 $ 0  
5
```

>The above example is a function returns a function that will add n to whatever is then given to it. You may remember the plus2 function from the last lecture. This is pretty much the same thing.
>
>This is because currying, or partial application, is just a nicer syntax for this type of higher order function. 
>
>As was said in the last lecture notes, multi-argument functions in Haskell are just a series of single argument functions that return a function that take 1 less argument.

They can also take and return functions

**For Example:**
```
swap :: (a -> b -> c) -> (b -> a -> c)  
swap f = \ x y -> f y x

ghci> take 4 [1..10]  
[1,2,3,4]

ghci> (swap take) [1..10] 4  
[1,2,3,4]
```

>The above is a function that takes a function that takes 2 arguments and returns a function that takes the same 2 arguments, but in reverse order.