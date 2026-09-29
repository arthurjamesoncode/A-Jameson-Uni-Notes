## Topics

- The `IO` Type
- Reading and Writing to the Console
- `do` Blocks
## Input and Output
Sometimes programs have to do non pure things, such as:
- Print something to the screen
- Read or write a file
- Communicate over a network
- Create a GUI

Haskell, while mostly a pure language, has ways for you to do these impure things.

Impure IO code talks to the outside world and pure functional code does the interesting computation.

>IO code can call pure functions but pure functions can not call IO code.

### `getLine`
`getLine` reads a line of input from the console.

**For Example:**
```
ghci> getLine  
hello -- This line is user inputed 
"hello"
 
ghci> :t getLine  
getLine :: IO String
```
## The `IO` Type
The IO type marks a value as being impure.

If a function returns an `IO` type then it is impure, meaning that it may have side effects or return different values for the same inputs.

The `IO` type should be thought of as a box, which holds a value from an impure computation, such as a string input but the user. To get the value out we use the `<-` operator.

**For Example:**
```
ghci> x <- getLine  
hello
  
ghci> x  
"hello"

ghci> :t x
IO [Char]

ghci> :t x  
x :: [Char]
```

>You must unbox values before you can use them in pure function.

**For Example:**
```
ghci> head (getLine)  
Couldn't match expected type ‘[a]’ with actual type ‘IO String’
 
ghci> x <- getLine  
hello
  
ghci> head x  
'h'
```

### `putStrLn`
`putStrLn` prints a string on the console followed by a `'\n`.

**For Example:**
```
ghci> putStrLn "hello"  
hello
 
ghci> :t putStrLn  
putStrLn :: String -> IO ()
```

>The `()` in the return type is called "unit". It indicates that the function returns nothing useful. It is contained within the IO type showing that the function has side effects.

## Writing Our Own IO Code
We can write our own `IO` actions.

**For Example:**
```
print_two :: String -> String -> IO ()  
print_two s1 s2 = putStrLn (s1 ++ s2)

ghci> print_two "abc" "def"  
abcdef
```

>Note the return type of `IO ()`

The `do` syntax allows us to combine multiple `IO` actions.

**For Example:**
```
get_and_print :: IO ()  
get_and_print =  
	do  
		x <- getLine  
		y <- getLine  
		putStrLn (x ++ " " ++ y)
```

A do block uses the following syntax
```
do  
	v1 <- IOaction  
	v2 <- IOaction  
	...  
	vk <- IOaction  
	IOaction
```

>`v1` through `vk` hold the unboxed values of `IOaction` and then the last line is the return value.

The `<-` section can be skipped if you don't want to unbox.
``` 
echo_two :: IO ()  
echo_two =  
	do  
		x <- getLine  
		putStrLn x  
		y <- getLine  
		putStrLn y
```

`let` expressions can be used inside `do` blocks. This lets you do pure computations between IO actions.

**For Example:**
```
add_one :: IO ()  
add_one =  
	do  
		n <- getLine  
		let num = (read n) :: Int  
			out = show (num + 1)  
		putStrLn out
```

Multiple `let` expressions can be used in the same `do` block. Unboxed values are only in scope for let expressions that come after them.

**For Example:**
```
import Data.Char

ask_for_letter_in_upper_case :: String -> IO Char
ask_for_letter_in_upper_case message =
	do
		let new_message = map toUpper message
		putStrLn new_message
		s <- getLine
		let letter = head s
		return letter 
```

>The order of operations in a do block matters. If we put `letter = head s` in the first let block it would cause a "Not in scope" error.

You can also use `if` expressions inside do blocks.

**For Example:**
```
guess :: IO ()  
guess = do  
	x <- getLine  
	if x == "42"  
		then putStrLn "correct!"  
		else putStrLn "try again"
```

If statements must be the last action of a given do block and both branches must have the same type inside the `IO` box. In the example above both branches has an type of `IO ()`

>If you want to perform multiple actions inside a branch of the `if` expression you need to use a nested do block.

`do` blocks let you sequence multiple actions and **only** work with `IO` actions. `IO` code should only be a small amount of your program. The majority is pure functional code.

### Putting Values in the `IO` box
Sometimes we need to put a pure value into `IO`. We can use the `return` function to do this.

**For Example:**
```
ghci> :t "hello"  
"hello" :: [Char]
 
ghci> :t return "hello"  
IO [Char]

print_if_short :: String -> IO ()  
print_if_short str =  
	if length str <= 2  
		then putStrLn str  
		else return ()
```

In the above example both sides must have the same type, `IO ()`, so we use `return ()` in the else branch. 

>`return` does not stop execution. It is **not** like the imperative return. It just makes a pure value an `IO` value.