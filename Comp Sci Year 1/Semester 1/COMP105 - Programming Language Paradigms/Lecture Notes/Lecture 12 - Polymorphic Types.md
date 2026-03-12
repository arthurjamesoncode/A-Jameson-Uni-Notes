## Topics

- Type Polymorphism
- Type Classes

## Type Polymorphism
Some functions work on many different types.

**For Example:**
```
length' [] = 0  
length' (_:xs) = 1 + length' xs
 
ghci> length' [1,2,3]  
3  
ghci> length' "abc"  
3  
ghci> length' [True, False, False]  
3
```

>Here we see length working on lists of type \[Int], \[Char], and \[Bool]

**We can see the type of the length function here**
```
ghci> :t length'  
length' :: [a] -> Int
```

`a` is a type variable.

- The length function can be applied to any list.
- `a` represents the type of the list elements. 

>Since, when determining the length of the list, it doesn't matter what type the elements are, the function doesn't need a specific type. In this case, `a` represents any possible type.

### Type Variables
Type variables can appear multiple times.

**For Example:**
```
ghci> :t head  
head :: [a] -> a  

ghci> :t tail  
tail :: [a] -> [a]
```

Within a single type `a` always means the same type. Like how `x` always means the same number in a given equation.

>This means that the return types of these functions are determined by the type of the input. The head of the list must be the same type as the elements of a list, for instance.

Functions can also use multiple variables.

**For Example:**
```
ghci> fst (1, 'a')  
1  
ghci> snd (1, 'a')  
a  

ghci> :t fst  
fst :: (a, b) -> a  
ghci> :t snd  
snd :: (a, b) -> b
```

These different variables can each be bound to a different type. When `fst` and `snd` are called in the example above `a` is bound to `Int` and `b` is bound to `Char`.

>It is important to recognise that while they **CAN** be different types they don't **HAVE** to be. `fst` can still work on `(1, 2)` which has the type `(Int, Int)`. In this case `a` and `b` are both `Int`.

Function types can tell you a lot about what a function does.

**For Example:**
```
ghci> zip [1,2,3] "abc"  
[(1,'a'),(2,'b'),(3,'c')]

ghci> :t zip  
zip :: [a] -> [b] -> [(a, b)]
```

It's relatively clear what zip does from its type annotation.

>This is something that can be very helpful in exams where you have access to GHCI. Compared to checking a lecture slide, it is often faster to type `:t foldr`, or similar, in GHCI to remind yourself of the order of arguments for these more complex functions.

### Type Annotations
It is good practice to give **type annotations** for your functions.

**For Example:**
```
length' :: [a] -> Integer  
length' [] = 0  
length' (_:xs) = 1 + length' xs
```

**The syntax is:**
```
function_name :: type
```

This is usually placed before the function definition.

If a type annotation isn't given, Haskell infers one for you.

**For Example:**
```
all_true [] = True  
all_true (x:xs) = x && all_true xs

ghci> :t all_true  
all_true :: [Bool] -> Bool
```

Haskell can infer the type since:
- The use of `:` means the input must be a list
- The list must contain bools because of the use of `&&`
- The function must return a bool since the base case returns `True` and `&&` also returns `True`

>Adding type annotations can help you catch bugs.

```
third_head list = head (head (head list))
 
ghci> :t third_head  
third_head :: [[[a]]] -> a  

third_head :: [a] -> a  
third_head list = head (head (head list))

Couldn't match type ‘a’ with ‘[[a]]’  
‘a’ is a rigid type variable bound by  
the type signature for third_head :: [a] -> a
```

Above you can see that this function, which is supposed to get the third item of a list, does not work as intended.

When given no type annotation the function infers `third_head :: [[[a]]] -> a`, which is clearly not intended since its meant to work on any `[a]`. 

When the function is given the explicit annotation `third_head :: [a] -> a` this is caught at compile time since Haskell cannot match the type inferred type of the function with the explicitly given one. 

This prevents you from being able to compile and run the program while the function is acting differently from how you intend it to. 

>Importantly, this can catch some errors but not all. You do still have to be careful and test functions thoroughly.

>The correct implementation of this would be `third_head list = head (tail (tail list))` or `third_head = head . tail . tail`. Important to recognise that this function is partial and will crash on any list with less than 3 elements.

## Type Classes
Some functions are polymorphic but can only be applied to some types

**For Example**
```
ghci> 1 + 1  
2

ghci> 1.5 + 2.5  
4.0

ghci> "hello" + "there"  
No instance for (Num [Char]) arising from a use of ‘+’  
In the expression: "hello" + "there"
```

>Above you can see that the `+` function only works on numbers, but can work on both `Float` and `Int` variables.

`Num` is a type class  
- It restricts the type variable a to only be number types  
- Int, Integer, Float, Double are all contained in `Num`  
- Char, Bool, tuples and lists are not in `Num`

```
ghci> :t (+)  
(+) :: Num a => a -> a -> a

ghci> :t (*)  
(*) :: Num a => a -> a -> a  
```

The `Eq` type class only allows types that can be compared with `==`

```
ghci> 1 == 1  
True

ghci> [1,2,3] == [4,5,6]  
False

ghci> ('c', False) == ('c', False)  
True 

ghci> :t (==)  
(==) :: Eq a => a -> a -> Bool
```

### Type Class Syntax
When writing type annotations for function that can take any type from some given type classes the syntax is slightly different.

```
equals_two a b = a + b == 2  
ghci> :t equals_two

equals_two :: (Eq a, Num a) => a -> a -> Bool  
```

**The syntax is:**
```
(Type_class1, Type_class2, ...) => Type
```

>In the example above we would say that `a` is constrained to types within the `Eq` and `Num` type classes.

### The Most General Type Annotation
The most general type annotation is the one that is least restrictive.

```
equals_two a b = a + b == 2
 
-- Works but too restrictive  
equals_two :: Int -> Int -> Bool 
 
-- Most general  
equals_two :: (Eq a, Num a) => a -> a -> Bool
  
-- Too general (will give error)  
equals_two :: a -> a -> Bool
```

>Haskell will always try to infer the most general type annotation if given none. This means that using `:t function` is a great way to practice writing the most general type annotations.
>
>One thing to be careful of is the "Monomorphism Restriction". Why this happens is outside the scope of the course, but it essentially causes Haskell to give overly specific annotations to partially applied functions. When partially applying functions you must write the most general annotation yourself to be safe.

### Number type classes  
`Num` has two sub-classes

**`Integral`** represents whole numbers (contains `Int` and `Integer`) 
```
ghci> :t div  
div :: Integral a => a -> a -> a  
```

**`Fractional`** represents rational numbers (contains `Float`, `Double`, and `Rational`) 
```
ghci> :t (/)  
(/) :: Fractional a => a -> a -> a
```

**Why does this work?**
```
ghci> 10 `div` 2  
5  
ghci> 10/2  
5.0
```

>Numbers in Haskell code have a polymorphic type

```
ghci> :t 1  
1 :: Num a => a  
```

>When they are used, Haskell will convert them to the correct member of `Num`

You can use the `::` operator to force a number be a particular type 

**For Example:**
```
ghci> 1 :: Integer  
1  
ghci> 1 :: Float  
1.0

ghci> (1 :: Integer) / 2
No instance for (Fractional Integer) arising from a use of ‘/’
```  

Once the type has been fixed, it is fixed .

>But you can convert back to a more generic type using `fromIntegral`.

```
ghci> fromIntegral (1 :: Int) / 2  
0.5

ghci> :t fromIntegral (1 :: Int)  
fromIntegral (1 :: Int) :: Num b => b

ghci> :t fromIntegral  
fromIntegral :: (Integral a, Num b) => a -> b
```

### Converting floats to integers  
Converting floats to integers is a lossy operation. Meaning that information is lost and cannot be retrieved.

```
ghci> ceiling 1.6  
2
  
ghci> floor 1.6  
1
  
ghci> truncate 1.6  
1

ghci> round 1.6  
2
```

### Other Type Classes 
Haskell includes many typeclasses that we won’t see on this course
```
ghci> :t length  
length :: Foldable t => t a -> Int  
```

`length` works on any data structure that is Foldable. This isn't necessary to know for the course. 

For COMP105, if you see  
- Functor  
- Foldable  
- Traversable  
then think list