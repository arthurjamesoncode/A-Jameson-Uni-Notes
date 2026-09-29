## Topics
- Types
- Function types
- Partial application
## Types

Everything in Haskell has a type. 

In GHCI, :type or :t will display the type of an expression, as shown below.
```
ghci> :t 'a'
'a' :: Char
```
### Basic Number Types

- **Int** holds 64-bit integers. They can be between -2$^6$$^3$ and 2$^6$$^3$ -1.
- **Integer** holds arbitrary size integers. This means it can hold an integer as large as available memory will allow.
- **Float** holds 32-bit floating point numbers. Exactly how these work is outside the scope of this course.
- **Double** holds 64-bit floating point numbers. These are the same as float but more bits allows for more precision and a larger range.

### Other Basic Types

- **Bool** holds binary truth values. Can be either True or False
- **Char** holds a single character. Can store any Unicode character.
### Tuple Types
The type of a tuple is made up of the type of its elements 

**For example**:
```
ghci> :t (True, 'a')
(True, 'a') :: (Bool, Char)
```

This encodes the size of a tuple in its type, and means that the elements can be of different types. 

>You can think of the type of a tuple being another tuple containing the type of all of its elements
### List Types
The type of a list is determined by the type of its elements.

**For Example**:
```
ghci> :t [True, False, False]
[True, False, False] :: [Bool]
```

>**Reminder**: Strings are just lists of characters.

**So therefore**:
```
ghci> :t "abcdef"  
"abcdef" :: [Char]`
```

Although you can use String when writing type annotations instead of \[Char]

- Lists are of type x are denoted by \[x].
- Unlike tuples, lists can only contain elements of one type.
- The length of a list is not encoded in its type.
## Function Types
Functions have types as well. 

**For example:**
```
is_lower c = c `elem` ['a'..'z']

ghci> is_lower 'a' 
True

ghci> :t is_lower
is_lower :: Char -> Bool
```

For a one argument function the type is written as:
```
input_type -> output_type
```

For a multiple argument function the type uses more `->`.

**For example:**
```
boolean_and a b = a && b

ghci> :t boolean_and  
boolean_and :: Bool -> Bool -> Bool  

ghci> :t (||)  
(||) :: Bool -> Bool -> Bool
```

For a function with multiple arguments the type is written as:
```
[arg1 type] -> [arg2 type] -> ... -> [return type
```

>The reason for this is because functions in Haskell are curried, this is the same thing as partial application which will be discussed in detail in the next section.
>
>This essentially means that each function in Haskell with multiple arguments is actually a sequence of functions that take a single argument. While this seems confusing it might start to make more sense after reading through the next section.
>
>Knowing this, the syntax for writing multiple argument functions makes a lot more sense.
>A `Bool -> Bool -> Bool` function is actually a function that takes a `Bool` as it's argument and then returns a function with the type `Bool -> Bool`.
## Partial Application
In most functional languages, functions can be partially applied.

Partial application fixes some arguments and then returns a new function that only takes the remaining arguments. 
When you call this new function and provide values for the remaining arguments it will return the result as if you called the original function with the value you fixed by partial application and the new values you are providing.

**For Example**:
```
plus a b = a + b  

plus2 = plus 2 

ghci> plus2 2  
4 
 
ghci> plus2 10  
12
```

>The above example uses partial application to create a function that increments any number given to it by 2.

**Partial Application must follow the argument order**
>This is because of what is discussed above. 
>When you call a function that takes `x` arguments and only apply `y` arguments, it returns a new function that takes `x-y` arguments. 
>Haskell will always assume you are giving it the first y arguments as otherwise there would be no way for it to determine which arguments you are giving it.

### Consequences of Partial Application
#### Eta reduction
Eta reduction allows you to simplify code. 
If you are writing a function that takes n arguments and all it does is apply n arguments to the end of another function call you can simplify it by removing those arguments altogether.

**For Example:**
```
take_first_four xs = take 4 xs  
⇓  
take_first_four = take 4
```

>The above example only uses one argument, which is the most common case for eta reduction, but it still holds for n arguments as long as they are applied at the end of the function you are calling.

#### Partial application of infix operators
Infix operators can be partially applied on both sides. 

**For Example:**
```
ghci> let f = (/2)  
ghci> f 4  
2.0

ghci> let g = (2/)  
ghci> g 4  
0.5
```

Observe that when 2 is applied before and after the `/` operator the result of calling the function with 4 is different.

>This also works with functions that aren't infix by default such as `div` and `mod` when called using backticks.

**For Example:**
```
ghci> let f = (5 `div`)
ghci> f 2
2

ghci> let g = (`div` 5)
ghci> g 2
0
```

#### Preferring Multiple Arguments Over Tuples
You can define and call functions in Haskell using both multiple arguments separated by spaces; and tuples containing multiple values.

**For Example:**
```
multThree x y z = x * y * z 

AND

multThree' (x, y, z) = x * y * z
```

>Its important to recognise that the first function takes 3 arguments, which are all numbers, but the 2nd only takes one, which is a tuple containing 3 numbers.

Both of these functions do the same thing. The second one also appears similar to the syntax of a lot of other imperative languages. However the second one cannot be partially applied.

>It's better to avoid using tuples, unless they are necessary, as using partial application is one of the benefits of functional programming and using tuples in this way deprive you of that opportunity.
