## Topics
- Fold
## Fold
Folds take lists and turn them into a single value.

We have seen a lot of examples of this, and know how to do it recursively.

**For Example:**
```
sum' [] = 0  
sum' (x:xs) = x + sum' xs
ghci> sum' [1..10]  
55
  
product' [] = 1  
product' (x:xs) = x * product' xs  
ghci> product' [1..10]  
3628800
```

The only things that change are  
- The initial value: `0`,`1`, etc.
- The operation used in each recursive step: `+`,`*`, etc.

### `foldr`

>Haskell has various fold functions that allow you to implement this without using recursion.

**For Example:**
```
foldr' :: (a -> b -> b) -> b -> [a] -> b  
foldr' _ init [] = init  
foldr' f init (x:xs) = f x (foldr' f init xs)

ghci> foldr' (+) 0 [1..10]  
55  

ghci> foldr' (*) 1 [1..10]  
3628800
```

Above we see a recursive implementation of `foldr` called `foldr'`. 

We can see that it takes a folded function (`f`), an initial value (`init`,) and a list. We can also see when applied to an empty list it returns the initial value. 

The folded function takes 2 arguments, the current value of the list (`x`) and an accumulator (`acc`). For any list of length 1, the accumulator is the `init` and for any list with a length greater than 1 the accumulator takes the value of folding the rest of the list. 

The return value at any step of the fold is the result of `f x acc`.

Below is an implementation of `sum` using `foldr` instead of recursion.
```
sum'' list = foldr (\ x acc -> acc + x) 0 list
```

You can see the folded function here is an anonymous function. The first argument is `x` and the second is `acc`. 

>You can see from the type annotation of `foldr'` that the folded function must have type `a -> b -> b`. This is because it takes an accumulator of type `b` and has to return a new accumulator. Remember `a` and `b` can be the same type but they don't have to be. This means that the output type of a fold does not have to be the same as the input type.

Consider the expression `foldr (\ x acc -> acc + x) 0 [1,2,3,4]`. It has the following values for its accumulator at each step.
```
init = 0  
0 + 4 = 4  
4 + 3 = 7  
7 + 2 = 9  
9 + 1 = 10
```

>The final step is 10 so the expression evaluates to 10.

In python `foldr f init input_list` would be implemented like this:
```
def foldr (f, init, input_list):
	acc = init  
	input_list.reverse()  
	
	for i in range(len(input_list)):  
		acc = f(input_list[i], acc)  
	
	return acc
```

>The `input_list.reverse()` is necessary because `foldr` starts from the right.

Below are some examples of uses for `foldr`:
```
concat' list = foldr (++) [] list  
ghci> concat' ["a", "big", "bad"]  
"abigbad"
 
all' list = foldr (&&) True list  
ghci> all' [True, True, True]  
True
 
length' list = foldr (\_ acc -> acc + 1) 0 list  
ghci> length' [1,2,3,4]  
4

count_ones list = foldr (\ x acc -> if x == 1 then acc + 1 else acc) 0 list  
ghci> count_ones [1,1,2,3,1,4]  
3
```

Below are some more examples of uses for `foldr` in which the output is different to that of the input:
```
sum_of_lengths list = foldr (\x acc -> acc + length x) 0 list  
ghci> sum_of_lengths ["one", "two", "three"]  
11

to_csv list = foldr (\x acc -> show x ++ "," ++ acc) "" list  
ghci> to_csv [1,2,3,4]  
"1,2,3,4,"
```

### `foldr1`
The function foldr1 uses the final value of the list to initialize the accumulator 
```
foldr1' :: (a -> a -> a) -> [a] -> a
foldr1' _ [] = error "empty list"  
foldr1' _ [x] = x
foldr1' f (x:xs) = f x (foldr1' f xs)

ghci> foldr1' (+) [1,2,3,4,5]  
15
```

Observe that the type of `foldr1'` is `foldr1' :: (a -> a -> a) -> [a] -> a`. Which means the output must have the same type as the input.

>It is important to recognise that foldr1 is partial. Meaning that, for some values given to it, it can return an error. 

**Examples of `foldr1` include**:
```
sum' list = foldr1 (+) list
  
product' list = foldr1 (*) list
  
concat' list = foldr1 (++) list  
ghci> concat [[1,2,3], [4], [3,2,1]] [1,2,3,4,3,2,1]
 
maximum' list = foldr1 (\ x acc -> if x > acc then x else acc) list  
ghci> maximum [1,2,3,4,3,2,1]  
4
```

>Note that the first 3 examples `sum'`, `product'`, and `concat'` are all partial implementations. This means that they will crash on empty lists. A better implementation would be to use `foldr` and give initial values of `0`, `1`, and `[]`. This would ensure they are not partial.
>
>The last example `maximum'` is also partial but as there is no way to choose a default minimum value it must be partial, when only implemented using a single fold. A better implementation would be `maximum' list = if null list then Nothing else Just (foldr1 max list)`.
>
>This implementation would ensure that it is not partial using the Maybe type, which will be covered later on.

### Folding Left and Right
`foldr` processes lists starting from the right.

**For Example:**
```  
foldr (+) 0 [1..4]
= 1 + (2 + (3 + (4 + 0)))
= 10

foldr (/) 1 [1..4]  
= 1 / (2 / (3 / (4 / 1)))  
= 0.375
```

`foldl` processes list starting from the left.

**For Example:**
```
foldl (+) 0 [1..4]  
= ((((0 + 1) + 2) + 3) + 4)
= 10

foldl (/) 1 [1..4]  
= ((((1 / 1) / 2) / 3) / 4)  
= 0.0416
```

>As you can see, the order of operations can sometimes change what the result would be. For example in the case of `/`.

The types of `foldr` and `foldl` are:
```
foldr :: (a -> b -> b) -> b -> [a] -> b  
foldl :: (b -> a -> b) -> b -> [a] -> b
```

>Observe that `foldl`'s folded function has flipped input types `a` and `b` and so its folded function would look like `(\ acc x -> expression)`.

An example of where you could use `foldl` over `foldr` is:
```
reverse_list list = foldl (\ acc x -> x : acc) [] list
 
ghci> reverse_list "hello"  
"olleh"
```

>This is more efficient since you can use `:`. If you were to do this with a `foldr` you would have to use `acc ++ x` and ++ is a more expensive operation.

Exactly which fold is more efficient in each circumstance is a more complicated question but, for the most part, prefer `foldr` over `foldl`. It tends to be more efficient.