## Tuples
Functions always return something, but sometimes we need them to return more than one thing. Tuples let us do exactly that.

A tuple lets us bind 2 or more values into a single value. For example:
```
(1, 2)

("A", "few", "words")

(6, "six")
```

Tuples can be any size, but must have at least 2 elements. The size of them should be thought of as being fixed, and they can mix types. So 
```
(1, "Two", 3, "Four", 5, "Six")
```
is a perfectly valid tuple.

You can see some examples of using tuples in functions below:
```
area_and_perimeter r = (pi * r * r, 2 * pi * r) 

ghci> area_and_perimeter 1 
(3.141592653589793,6.283185307179586) 

rect_area (width, height) = width * height 

ghci> rect_area (2, 4) 8
```

If you look at the second example you can see that we can pass a tuple to a function. The syntax of this is much closer to what you'd expect from an imperative language. So you can see
```
f (a, b) = a + b

-- Does the same thing as

f a b = a + b
```

While both of these work, there are some good reasons to prefer the standard syntax over using a tuple. You can read more about this in [[Lecture 11 - Types]] under partial application, but I recommend continuing in order.
### Accessing Data in Tuples
When using two element tuples `fst` gives the first element and `snd` gives the second.

So 
```
ghci> fst (1,"hi")
1

ghci> snd (1, "hi")
"hi"
```

If you want to access elements of tuples with a size greater than 2, you must use pattern matching.

```
f (a, b, c) = a + b + c

ghci> f (1, 2, 3)
6
```
### Lists
A list is a collection of elements. Lists in Haskell can have any number of elements, including 0.

For example:
```
[]
[1]
[1, 2]
```

You can join lists using the `++` operator.

```
ghci> [1,3,4] ++ [2,5,6]
[1,3,4,2,5,6]
```

Strings in Haskell are actually just lists of characters. 
```
ghci> ['a','b','c']
"abc"
ghci> ['a']
"a"
```

>Notice that characters and strings are differentiated by strings having double quotes and characters having single quotes.

This means that any operation that can be done on lists can also be done on strings.

The `!!` operator gets a specified element from a list. Lists are 0 indexed `list !! 0` will get the first element of `list`.

For example:
```
ghci> [1, 2, 3, 4, 5] !! 1
2
```

>Note that lists in Haskell are singly linked lists. This means that random access is expensive as to access the $n$th element Haskell has to walk through the first $n-1$ elements.
### Processing Lists
Since Haskell uses linked lists we usually process lists from the front. 

The function `head` gives the first element and the function `tail` gives everything except the first element. 
```
ghci> head [1,2,3,4,5]
1

ghci> tail [1,2,3,4,5]
[2,3,4,5]
```
The names for the values these functions get are the same as the functions. So, in this example, `1` is the head of the list and `[2,3,4,5]` is the tail.

The `:` operator is called "cons" and glues a new head onto an existing list. This actually lets us build full lists just using `:` and `[]`

For example:
```
ghci> 2:[3,1,5,6]
[2,3,1,5,6]

ghci> 'a':'b':'c':[]
"abc"
```

We can also process lists using `last` and `init`. `last` is like the inverse of head and gives the last element of a list. `init` is like the inverse of tail and gives everything except the last element of the list.

Remember that, as Haskell lists are singly linked lists, using both of these functions is expensive.