## Processing Lists
Often when we use a loop in imperative programming, it is to traverse some kind of list. 

In Haskell, we traverse lists in by using **recursion**.

For example, consider a function meant to traverse a list of numbers and return the sum of the whole list. We can write this function in Haskell.

First we need a base case. For this we can use an empty list, as the sum of an empty list is always 0. Then for any non empty list, we can just take the value of the first element and add it to the sum of the rest of the list.

If we recall that `head` gives the first element of a list and `tail` gives the rest of the list then we can write a program to do this like so:
```
sum' [] = 0
sum' ls = head ls + sum (tail ls)
```

We can use **pattern matching** on a list to elegantly split it into the head and tail. If we do this, we can rewrite our program like:`
```
sum' [] = 0
sum' (x:xs) = x + sum xs
```

## Building Lists
We can also use recursion to build lists.

If we recall the cons operator (`:`), then we can build lists by recursively gluing elements on to the front of a new list.

Consider a function which takes a positive integer and returns a list of the numbers up to that point in descending order.

We can build such a function like so
```
down_from 0 = []
down_from x = x : down_from (x-1)

ghci> down_from 5
[5,4,3,2,1]
```
## Transforming Lists
We can also write functions that **transform** lists.

Consider a function which takes a list of numbers as an input and returns a new list which contains the squares of all the numbers from the input list.

We can use `:` and recursion to write this function like so:
```
square_list []     = []
square_list (x:xs) = x*x : square_list xs

ghci> square_list [2,3,4]
[4,9,16]
```
## Advanced List Functions
You can use pattern matching to access multiple elements of a list at once.

Consider a function which wanted to add the adjacent elements of a list. We could write this function like so:
```
add_adjacent []       = [] 
add_adjacent [x]      = error "Odd number of elements" 
add_adjacent (x:y:xs) = x+y : add_adjacent xs

ghci> add_adjacent [1,2,3,4,5,6] 
[3,7,11]
```

Note that we don't need to consume the next element after accessing it.

Consider a function that takes a list of numbers and returns a new list of each number added to it's immediate successor. We can write this like so:
```
add_next [] = error "Not enough elements" 
add_next [_] = error "Not enough elements" 
add_next [x,y] = [x+y] 
add_next (x:y:xs) = x+y : add_next (y:xs) 

ghci> add_next [1,2,3,4,5] 
[3,5,7,9]
```

We can also break the list down in more complex ways, for example using the functions `take` and `drop`.

Consider a function that groups a list into sub-lists of `n` adjacent elements. We could write such a function like so:
```
group n [] = [] 
group n list = 
	let 
		first = take n list 
		rest = drop n list 
	in 
		first : group n rest 
	
ghci> group 4 [1..12] 
[[1,2,3,4],[5,6,7,8],[9,10,11,12]]
```