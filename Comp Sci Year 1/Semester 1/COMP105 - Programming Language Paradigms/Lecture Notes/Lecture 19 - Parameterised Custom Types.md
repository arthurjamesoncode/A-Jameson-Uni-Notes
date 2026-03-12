## Topics

- Parameterised Custom Types
- The `Maybe` Type
- The `Either` Type
- `case` Expressions

## Type Variables in Custom Types
We can use type variables in custom types.

**For Example:**
```
data Point a = Point a a

ghci> :t Point (1::Int) (2::Int)  
Point Int

ghci> :t Point "hello" "there"  
Point [Char]
```

>Obviously using any non number types with `Point` kind of goes against the purpose of `Point` to represent a point in 2d space, but this still illustrates the possibility of using any type within a custom type.

You can also use multiple variables in the same type:

**For Example:**
```
data Things a b c = Things a b c deriving(Show)  

ghci> Things [] 1.5 'a'  
Things [] 1.5 'a'

ghci> :t Things [] 1.5 'a'
Things [] 1.5 'a' :: Fractional b => Things [a] b Char

ghci> Things "string" "other string" True  
Things "string" "other_string" True

ghci> :t Things "string" "other_string" True
Things "string" "other_string" True :: Things [Char] [Char] Bool
```

>Here we can see Things can contain multiple different types. It's important to recognise that `a`, `b`, and `c` can be different but they don't have to be, as can be seen in the last example.

We can write functions using these types.

**For Example:**
```
first_thing (Things x _ _) = x  
ghci> first_thing (Things 1 2 3)  
1

ghci> :t first_thing  
first_thing :: Things a b c -> a
```

>Notice the use of pattern matching to access the data stored in one of these custom types.

## The `Maybe` Type
The Maybe type is used in pure functional code that might fail, or not return a value.

**Definition and Examples:**
```
data Maybe a = Just a | Nothing

ghci> :t Just "hello"  
Maybe [Char] 
 
ghci> :t Just False  
Maybe Bool  

ghci> :t Nothing  
Maybe a
```

See above how it has 2 constructors. One is just `Nothing` and has no parameter, so therefore contains no data. The other is the `Just` constructor and contains a value of type `a`. 

>This means that we can check if the code returns a `Nothing` and act accordingly. This is essentially error handling within pure functional code.

Maybe can be used to create whole versions of partial functions.

**For Example:**
```
safe_head [] = Nothing  
safe_head (x:_) = Just x
 
ghci> safe_head [1,2,3]  
Just 1
  
ghci> safe_head []  
Nothing
```

>Where `head` would crash when given an empty list, `safe_head` instead returns `Nothing`.

## Case Expressions
Case expressions can do pattern matching within functions.

**For Example:**
```
head_or_zero list =  
	let  
		h = safe_head list  
	in  
		case h of Just x -> x  
				  Nothing -> 0

ghci> head_or_zero [1,2,3]  
1
```

The syntax for a case expression is:
```
case expression of pattern1 -> expression  
				   pattern2 -> expression  
				   ...  
				   patternk -> expression
				   _        -> expression
```

>The wildcard (`_`) acts as a catch all for case expressions. It does not need to be there, and usually won't since you can just add exhaustive cases, but can be useful if you only need to do something specific for the a few of many possible cases.

Case is just an expression like most things in Haskell and can be written on one line using slightly different syntax.

**For example:**
```
ghci> let h = Just 5
ghci> case h of {Just x -> x; Nothing -> 0}
5

ghci> (case 1 of 1 -> 1) + (case 2 of 2 -> 1)  
2
```

Below is a more complex example of how to write a safe function using `Maybe`:
```
safe_get_heads list =  
	let  
		mapped = map safe_head list  
		filtered = filter (/=Nothing) mapped  
		unjust = (\ x -> case x of Just a -> a)  
	in  
		map unjust filtered

ghci> safe_get_heads [[], [1], [2,3]]  
[1,2]
```

### Exceptions in Haskell
Haskell does include support for exceptions.

**For Example:**
```
ghci> head []  
*** Exception: Prelude.head: empty list
```

Exceptions are **not** pure functional, since every function can only return 1 type. 

>You cannot catch exceptions in pure functional code and catching exceptions in IO code will not be covered in this course, but can be done. 
>
>Maybe, and some other parameterised types, can be used to add exception like behaviour to pure code.

## The `Either` Type
The `Either` type lets you store multiple different types as the same type.

**Definition and Examples:**
```
data Either a b = Left a | Right b
 
ghci> :t Left 'a'  
Either Char b

ghci> :t Right (2 :: Int)  
Either a Int
```

>As the `a` and `b` variables can be any type both the `Left 'a'` expression and `Right (2 :: Int)` expression can evaluate to the same type. In this case: `Either Char Int`.

The `Either` type can be used to store multiple values of 2 different types in the same list.

**For Example:**
```
ghci> let list = [Left "one", Right 2, Left "three", Right 4]
ghci> :t list
list :: Num a => Either [Char] a

is_left (Left _) = True  
is_left _ = False
  
ghci> map is_left list  
[True,False,True,False]
```

The `Either` type can also be used to make one function return values with 2 possible types.

**For Example:**
```
is_digit = (`elem` "0123456789")

int_or_char c = if is_digit c 
					then Left (read [c] :: Int)
					else Right c

ghci> int_or_char '1' =
Left 1 

ghci> int_or_char 'b' =
Right 'b'

ghci> :t int_or_char
int_or_char :: Char -> Either Int Char

ghci> map int_or_char "ab1c2"
[Right 'a', Right 'b', Left 1, Right 'c', Left 2] 
```

>It's important to recognise that this is not returning 2 types of `Int` or `Char`. It is returning 1 type, which is `Either Int Char`.

**Some more Examples:**
```
-- uses the is_left function and list value from earlier
get_lefts list =  
	let  
		filtered = filter is_left list  
		unleft = (\ (Left x) -> x)  
	in  
		map unleft filtered
		 
ghci> get_lefts list  
["one","three"]

ghci> let nums = [Left pi, Right (4::Int), Left 2.7182]

square (Left x) = Left (x ** 2)  
square (Right x) = Right (x ^ 2)
  
ghci> map square nums  
[Left 9.86,Right 16,Left 7.38]
```

### Meaningful Error Messages
Either can be used to give detailed errors.

**For Example:**
```
safe_head_either [] = Right "empty list"  
safe_head_either (x:_) = Left x
  
ghci> safe_head_either []  
Right "empty list"

ghci> safe_head_either [1,2,3]  
Left 1
```