## Recursion and Memory Use
To see the extensive memory use of recursion we can look at an example of how factorial is evaluated.

**For Example:**
```
fact 1 = 1  
fact n = n * fact (n-1) 

fact 4  
> 4 * fact 3  
> 4 * (3 * fact 2)  
> 4 * (3 * (2 * fact 1))  
> 4 * (3 * (2 * 1))  
> 24
```

The example above builds up a **call stack**. Each recursive call adds a new value to this stack and we can only evaluate when we hit the base case. This can cause crashes due to running out of memory if the stack gets too big.

>This is actually where the name `Stack Overflow`.

We can fix this using a tail recursive functions.
## Tail Recursive Functions
A function is tail recursive if there is nothing left to do after the recursive call.

**For Example:**
```
is_even 0 = True  
is_even 1 = False  
is_even n = is_even (n-2)
 
is_even 4  
> is_even 2  
> is_even 0  
> True
```

Observe how in the example above is even doesn't build up a call stack. This means the function is more memory efficient.

>In a lazily evaluated language this happens automatically (as long as something forces the evaluation of arguments) but in strictly evaluated languages they would need to feature something called "Tail Call Optimisation" or TCO.
>
>This is because a lazily evaluated function would see that it returns a function call, return it and then go back into the function to actually evaluate what the call was. This, since it goes back and then into, doesn't build up a call stack.
>
>A strictly evaluated function would, by default, reach the end of its call, see that it returned a function call and then go straight in to evaluate it. This does build up a call stack. TCO essentially is an optimisation that allows the same level of the call stack to be used to evaluate the function call.
>
>Most imperative language compilers have some form of TCO built into them making tail recursion important in all languages.

### Writing Tail Recursive Functions
To write a tail recursive function we can:
- Add an accumulator as an argument  
- Initialise it some value
- Modify it with each recursive call

>This works just like folds and scans

**For Example:**
```
fact_tail 1 acc = acc  
fact_tail n acc = fact_tail (n-1) (acc * n)  
factorial n = fact_tail n 1
```

In strict evaluation, as there is some kind of TCO, it the call looks like this:
```
factorial 4  
> fact_tail 4 1  
> fact_tail 3 4  
> fact_tail 2 12  
> fact_tail 1 24  
> 24
```

As you can see, no call stack is built up.

In lazy evaluation, it's not so simple:
```
factorial 4  
> fact_tail 4 1  
> fact_tail 3 (4*1)  
> fact_tail 2 (3*4*1)  
> fact_tail 1 (2*3*4*1)  
> 24
```

>The memory problem is just transferred to the argument.

We can fix this using `$!`

**For Example:**
```
fact_tail 1 acc = acc  
fact_tail n acc = fact_tail (n-1) $! (acc * n)  
factorial n = fact_tail n 1
```

## Folds and Tail Recursion
`foldl` is naturally implemented via tail recursion, and should be preferred over `foldr` in strict languages.

```  
foldl f acc [] = acc  
foldl f acc (x:xs) = foldl f (f acc x) xs
  
ghci> foldl (+) 0 [1,2,3,4,5]  
15
```

In Haskell however `foldl` is not strictly evaluated so runs into the same problem, where the memory usage problems are just passed to the accumulator. To get around this we can use `foldl'` which is a strict version of `foldl` available in the `Data.List` package.

**For Example:**
```
foldl' f acc [] = acc  
foldl' f acc (x:xs) = (foldl' f $! (f acc x)) xs
```

### Left Folds and Laziness
Left Folds can destroy laziness since we need to get to the end of the list to get the accumulator.

**For Example:**
```
ghci> let f = foldr (\ x acc -> x : acc) [] [1..]  
ghci> take 4 f  
[1,2,3,4]

ghci> let g = foldl (\ acc x -> acc ++ [x]) [] [1..]  
ghci> take 4 g  
<never terminates>
```

This means that in Haskell you should prefer `foldr` since it can preserve laziness.

If we know that laziness won't help, because we are going the fold the whole list anyway, we may as well use `foldl'` as this will use less memory than `foldr` due to not building a call stack.

`foldl` by itself has no advantages when compared to these other functions. It both destroys laziness and builds a call stack so there is no real reason to use it at all.