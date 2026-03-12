## Topics

- `scan`
- `takeWhile`
- `dropWhile`
- `zipWith`

## Scan
A scan is like fold, but returns a list containing the values of the accumulator at each step.

**For Example:**
```
ghci> scanr (+) 0 [1,2,3,4]  
[10,9,7,4,0]  

ghci> scanr (*) 1 [1,2,3,4]  
[24,24,12,4,1]

ghci> scanr1 (\ x acc -> x ++ " " ++ acc) ["one", "two", "three"]  
["one two three","two three","three"]
```

>Observe how `scanr` starts at the right of the list, so the last item in the returned list is actually the initial value.

See below for an implementation of scan:
```
scanr' :: (a -> b -> b) -> b -> [a] -> [b]  

scanr' _ init [] = [init]  
scanr' f init (x:xs) =  
	let  
		recursed = scanr' f init xs  
		new = f x (head recursed)  
	in  
		new : recursed
```

There are also left to right versions of scan.

**See Below:**
```
ghci> scanl (+) 0 [1..10]  
[0,1,3,6,10,15,21,28,36,45,55]

ghci> scanr (+) 0 [1..10]  
[55,54,52,49,45,40,34,27,19,10,0]
 
ghci> :t scanl  
scanl :: (b -> a -> b) -> b -> [a] -> [b]
```

>There are also `scanr1` and `scanl1` functions which, similarly to `foldr1` and `foldl1` use a value from the list to initialise the accumulator. Like the folds, `scanr1` takes the last item of the list and `scanl1` takes the first. 
### Higher Order Fibonacci
Below is an implementation of the `fast_fib` function from Lecture 9, using only higher order functions:
```
fib_pairs n = scanl (\ (a, b) _ -> (b, a + b)) (0, 1) [1..n]
ghci> fib_pairs 7  
[(0,1),(1,1),(1,2),(2,3),(3,5),(5,8),(8,13),(13,21)]  

fib_to_n n = map fst (fib_pairs n)  
ghci> fib_to_n 7

[0,1,1,2,3,5,8,13]
```

The `fib_pairs` function uses a list range and a scan to generate the first n Fibonacci pairs. 

It does this by using an accumulator value of the last Fibonacci pair, and generating a new one from this. An initial value of `(0, 1)` is given.

>Observe how the list range is only used to determine the number of times this happens. The value is so unnecessary that in the folded function the `x` is replaced with a `_`.

The Fibonacci numbers are then found by mapping `fst` over the list of pairs.

## `takeWhile`  
`takeWhile` takes from a list while a condition is true. 

**For Example:**
```
ghci> takeWhile (<=5) [1..10]  
[1,2,3,4,5]  
ghci> takeWhile (/=' ') "one two three"  
"one"  
ghci> takeWhile (\ x -> length x <= 2)  
["ab", "cd", "efg"]  
["ab","cd"]
```

**Implementation:**
```  
takeWhile' :: (a -> Bool) -> [a] -> [a]  
takeWhile' _ [] = []  
takeWhile' f (x:xs)  
| f x = x : takeWhile' f xs  
| otherwise = []
```

## `dropWhile`  
`dropWhile` drops from a list while a condition is true.

**For Example:**
```
ghci> dropWhile (==1) [1,1,2,2,3,3]  
[2,2,3,3]  
ghci> dropWhile (`elem` ['a'..'z']) "smallBIG"  
"BIG"  
ghci> dropWhile (\x -> x < 10 && x > 0) [1,2,3,10,4,5]  
[10,4,5]
```

**Implementation**
```
dropWhile implementation  
dropWhile' :: (a -> Bool) -> [a] -> [a]  
dropWhile' _ [] = []  
dropWhile' f (x:xs)  
| f x = dropWhile' f xs  
| otherwise = x:xs
```

###  A Complex `takeWhile` and `dropWhile` Example

```
split_words "" = []  
split_words string =  
	let  
		first = takeWhile (/=' ') string  
		up_to_space = dropWhile (/=' ') string  
		after_space = dropWhile (==' ') up_to_space  
	in  
		first : split_words after_space
		 
ghci> split_words "one two three"  
["one","two","three"]
```

### `words` and `unwords` 

The `split_words` function exists in prelude and is called `words`

**For Example:**
```
ghci> words " foo bar baz "  
["foo","bar","baz"]

ghci> unwords ["foo","bar","baz"]  
"foo bar baz"
```

## `zipWith`
`zipWith` zips two lists together using a function.

**For Example:**
```
ghci> zipWith (+) [1,2,3] [4,5,6]  
[5,7,9]  
ghci> zipWith (++) ["big", "red"] ["dog", "car"]  
["bigdog","redcar"]  
ghci> zipWith (\ x y -> if x then y else -y)  
[True, False, False] [1,2,3]  
[1,-2,-3]
```

**Implementation:**
```  
zipWith' :: (a -> b -> c) -> [a] -> [b] -> [c]  
zipWith' _ [] _ = []  
zipWith' _ _ [] = []  
zipWith' f (x:xs) (y:ys) = f x y : zipWith' f xs ys
```

**Examples of `zipWith`:**
```
mult_by_pos list = zipWith (*) list [0..]  
ghci> mult_by_pos [2,3,4,5]  
[0,3,8,15]

ghci> zipWith (\ x y -> x : y : []) "abc" "123"  
["a1","b2","c3"]
  
interleave str1 str2 =  
	let  
		zipped = zipWith (\ x y -> x : y : []) str1 str2  
	in  
		concat zipped
  
ghci> interleave "abc" "123"  
"a1b2c3"
```

### `any`  
The `any` function takes a predicate f  and returns True if anything in the list satisfies f.

**Implementation:**
```
any' :: (a -> Bool) -> [a] -> Bool  
any' f xs = or $ map f xs
  
ghci> any (>10) [1,2,11,12]  
True
```

### `all`
The all function takes a predicate f and returns True if everything in the list satisfies f.

**Implementation:**
```
all' :: (a -> Bool) -> [a] -> Bool  
all' f xs = and $ map f xs

ghci> all (>10) [1,2,11,12]  
False
```