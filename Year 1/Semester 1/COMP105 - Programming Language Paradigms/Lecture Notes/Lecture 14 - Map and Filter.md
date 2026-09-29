## Topics

- `map`
- `filter`
- Higher Order Programming

## `map`
`map` applies a function to every element in a list and returns a new list with the results.

**For Example:**
```
map' :: (a -> b) -> [a] -> [b]  
map' _ [] = []  
map' f (x:xs) = f x : map' f xs
  
ghci> map even [1..5]  
[False,True,False,True,False]

square x = x * x  
ghci> map square [1..5]  
[1,4,9,16,25]

ghci> map reverse ["the", "quick", "brown", "fox"]  
["eht","kciuq","nworb","xof"]

ghci> map fst [(1,2),(3,5),(6,3),(2,6),(2,5)]  
[1,3,6,2,2]
```

It's common to use curried functions with map.

**For Example:**
```
ghci> map (*2) [1..5]  
[2,4,6,8,10]

ghci> map (2^) [1..5]  
[2,4,8,16,32]

ghci> map (drop 2) ["the", "quick", "brown"]  
["e","ick","own"]
```

It's also common to use anonymous functions with map.

**For Example:**
```
ghci> map (\x -> x*x) [1..5]  
[1,4,9,16,25]

ghci> map (\(x, y) -> x + y) [(1,1), (2,2), (3,3)]  
[2,4,6]

ghci> map (\(_:y:_) -> y) ["the", "quick", "brown"]  
"hur"
```

When working with nested lists, using nested maps can be powerful.

**For Example:**
```
ghci> map (map (*2)) [[1,2,3], [4,5,6], [7,8]]  
[[2,4,6],[8,10,12],[14,16]]
 
import Data.Char
  
ghci> map (map toUpper) ["the", "quick", "brown"]  
["THE","QUICK","BROWN"]
```

>Notice the second maps (`map (*2)` and `map toUpper`) are actually partially applied.

## `filter`
`filter` takes a predicate and a list and returns a list only containing the element for which the predicate is true.

>A predicate is a function which takes an item, performs some computation and then returns a bool.

**For Example:**
```
filter' :: (a -> Bool) -> [a] -> [a]  
filter' _ [] = []  
filter' f (x:xs)  
| f x = x : rest  
| otherwise = rest
where rest = filter' f xs
 
ghci> filter' even [1..10]  
[2,4,6,8,10]

ghci> filter (>=10) [1..12]  
[10,11,12]
 
ghci> filter (\x -> length x <= 2) ["aaa", "bb", "c"]  
["bb","c"]

ghci> filter (\x -> x `elem` "aeiou") "the quick brown"  
"euio"
```

>Like `map`, filter is often used with partial application and anonymous functions. Note this in the examples above.

Combining `map` and `filter` can be very powerful.

**For Example:**
```
square_even :: [Int] -> [Int]  
square_even list = map (^2) (filter even list)

ghci> square_even [1..10]  
[4,16,36,64,100]

squares_gt100 :: [Int] -> [Int]  
squares_gt100 = filter (>100) . map (^2)

ghci> squares_gt100 [1..15]  
[121,144,169,196,225]
```

>There is actually a more efficient implementation of `squares_gt100`. 
>
>If you do `squares_gt100 = map (^2) . filter (>10)` the `(^2)` function is applied to less arguments making the function faster.
>
>Note that the only meaningful change is the order in which the functions are composed.

## Higher Order Programming
What we've seen here are examples of higher order programming

This is a style which:  
- de-emphasises recursion  
- focuses on applying functions to lists  
- is available in imperative languages (python, C++) 

There is a whole family of higher order programming functions available in Haskell, many of which we will see in future lectures. 

>This is the main way people write programs in Haskell, by chaining together these types of functions.