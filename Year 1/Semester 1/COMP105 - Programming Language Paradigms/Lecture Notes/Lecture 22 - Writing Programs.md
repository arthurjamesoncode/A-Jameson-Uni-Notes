## Topics

- Writing and Compiling Programs
- File `IO`
- Useful `IO` functions

## Writing Programs
To write a program in Haskell we write a `main` function.

**For Example:** 
```
main :: IO ()  
main = putStrLn "Hello world!"
```

>`main` always takes no arguments and returns an `IO` type.

To run the program we need to compile it.

**For Example (Unix):**
```  
$ ghc hello.hs  
[1 of 1] Compiling Main ( hello.hs, hello.o )  
Linking hello ...

$ ./hello  
Hello world!
```

To compile on windows:
- Open a terminal
- Navigate to the directory where you saved your file. For example `M:\programs`
- Compile with `ghc code.hs`, substituting `code.hs` with your file name.
- To run the code just type `code`, or the file name with no extension.

You can also compile and run code in subdirectories, but you will  
need to use "cd" to first switch to the right directory or type the whole relative path.

### Command Line Arguments
Most command line programs take arguments. `getArgs` returns those arguments as `IO String []`. This function must be imported as part of the `System.Environment` package.

**For Example:**
```
import System.Environment  

main :: IO ()  
main = do  
	args <- getArgs  
	let output = "Command line arguments: " ++ show args  
	putStrLn output

main :: IO ()  
main = do  
	[n_str, str] <- getArgs  
	let n = read n_str :: Int  
	printN str n
 
$ ./repeat_string 3 hello  
hello  
hello  
hello
```

>For readability purposes I would recommend using pattern matching to get the arguments out, like in the second example.
### Looping in IO Code
The only way to loop in IO code is to use recursion.

**For Example:**
```
printN :: String -> Int -> IO ()  
printN _ 0 = return ()  
printN str n =  
	do  
		putStrLn str  
		printN str (n-1)
```

>There are still no variables and no loops.
## File IO
To read the contents of a file we can use `readFile`

**example.txt:**
```
line one  
line two  
line three
```

**`readFile` Example:**
```
ghci> :t readFile
readFile :: String -> IO String

ghci> readFile "example.txt"
"line one\nline two\nline three\n"
```

>Note that the GHCI console automatically unboxes `IO` types and so can print the output to the console. 
>
>To use this inside a program you would need to do something like: `txt <- readFile.txt`.

To write a string to a file we can use `writeFile`

**`writeFile` Example**
```
ghci> :t writeFile
writeFile :: String -> String -> IO ()

ghci> writeFile "output.txt" "hello\nthere\n"
```

**output.txt:**
```
hello  
there

```

In [[Lecture 17 - Higher Order Functions]] we wrote a function `report` that would find the averages of a set of student marks. We can now turn this into a full program.

```
main :: IO ()  
main = do  
	[infile, outfile] <- getArgs  
	input <- readFile infile  
	writeFile outfile (report input)
```

### Complications of Lazy `IO`
This isn't covered in COMP105 at all but if you move past this module and try to do more things with files you may end up very confused. 

I'm not going to go further than how to read an entire file, edit it in some way, and rewrite it to the same file, but first you'll need to understand how reading and writing a file works.

If you are struggling already, I would recommend skipping this and coming back later.

If you've done any file editing in an imperative language you may be familiar with the idea of opening and closing a file. Essentially for most programs, if a file isn't open it cannot be written to or read. Closing the file is saying that we are done with it and don't need to read anything else from it or write anything else to it.

**For Example in Haskell:**
```
import System.IO

main = do
	handle <- openFile "file.txt" ReadWriteMode
	contents <- hGetContents handle
	putStrLn contents
    hClose handle
    return ()
```

>The above opens a file reads the contents, prints it to the screen, and then closes the file.
>
>Haskell defines operations that work on files as the type `Handle` which is what handle is here. You do not need this 

The last thing to be wary of is file locking. Essentially is one file is being worked on by a handler for some reason, it cannot be worked on by another. It is much more complicated than that but you don't need to understand that.
**For Example:**
```
import System.IO
import Data.Char

main = do
    handle <- openFile "file.txt" ReadWriteMode
    contents <- hGetContents handle
    writeFile "file.txt" (map toUpper contents)
    hClose handle
    return ()
```

The above gives the error `*** Exception: file.txt: openFile: resource busy (file is locked)`. This is because `writeFile` opens a file, given by a path, and overwrites it with the contents of the string before closing it again. Since the file is already open it is locked and cannot be opened again.

You get the same error with this:
```
main :: IO ()
main = do
    txt <- readFile "file.txt"
    let out = reverse txt
    writeFile "file.txt" out
```

>This is because of laziness.

`readFile` opens a file, reads it contents and then closes it, but because Haskell evaluates `txt` lazily it means that the file is open until Haskell needs the value of `txt` which is only on the `writeFile` line. 

Since the file is open it is locked and trying to use `writeFile` gives the error ``*** Exception: file.txt: openFile: resource busy`.

We can fix this by forcing Haskell to fully evaluate `txt`. There are a few ways to do this but asking for it's `length` is an easy one.

>For info on unless and when which will be used in the examples look ahead to "Useful IO Functions".

**For Example:**
```
import Control.Monad

main :: IO ()
main = do
  txt <- readFile "file.txt"
  let out = reverse txt
  when (length out > 0) $ writeFile "file.txt" out
```

Because length forces Haskell to evaluate the whole of `out`, and therefore `txt`, `readFile` has actually finished its operation and closed the file. 

Interestingly `readFile` will always perform the full operation of reading and closing its file as long as any part of the string is needed by Haskell. So an optimisation that could be made to the above code is:
```
import Control.Monad

main :: IO ()
main = do
  txt <- readFile "file.txt"
  let out = reverse txt
  unless (null out) $ writeFile "file.txt" out
```

Which is faster as null is a faster operation that length.

Below are some interesting behaviours that show how the evaluation works. 

**file.txt:**
```
test writing
a file with
a few lines
```

>Note `:sprint` shows what a value is as Haskell has evaluated it up to that point. Notice more information showing up about `str` as we evaluate expressions that include it.

**GHCI Evaluation Examples:**
```
--String Example
ghci> str = "test"
ghci> :sprint str
str = _

ghci> null str    
False
ghci> :sprint str
str = 't' : _

ghci> length str
4
ghci> :sprint str
str = "test"

--File Example
ghci> txt <- readFile "file.txt"
ghci> :sprint txt
txt = _

ghci> null txt
False
ghci> :sprint txt
txt = 't' : 'e' : 's' : 't' : ' ' : 'w' : 'r' : 'i' : 't' : 'i' :
      'n' : 'g' : '
' : 'a' : ' ' : 'f' : 'i' : 'l' : 'e' : ' ' : 'w' :
      'i' : 't' : 'h' : '
' : 'a' : ' ' : 'f' : 'e' : 'w' : ' ' : 'l' :
      'i' : 'n' : 'e' : 's' : _
      
ghci> length txt
36
ghci> :sprint txt
txt = "test writing
a file with
a few lines"
```

>Notice how, even though Haskell only requires the first character of a string to determine that `null str` is true but after `null txt` it gives the full string, the only thing Haskell doesn't know is that it knows the whole string.
>
>This is because `readFile` either has read none of the file and the file is open, or it has read all of the file and is closed.
## Some Useful IO Functions

### `print`
`print` is the same as `(putStrLn . show)`

**For Example:**
```
print_stuff = do  
	print "hi"  
	print 1  
	print [1,2,3]  
	print False
	
ghci> print_stuff
"hi"
1
[1,2,3]
False
```

>Observe how `print "hi"` outputs `"hi"` when `putStrLn "hi"` outputs `hi`. 
>
>When you want to output strings, unless you want to output what that string looks like in code, you should use `putStrLn` and not print.

### `putStr`
`putStr` prints a string without a new line character at the end.

**For Example:**
```
print_three a b c = do  
	putStr a  
	putStr b  
	putStr c  
	putStr "\n"
	  
ghci> print_three "one" "two" "three"  
onetwothree
```

### `readLn`
`readLn` gets a line of input and then calls `read`

**For Example:**
```
readLn' :: Read a => IO a  
readLn' = do  
	x <- getLine  
	return (read x)  

add_one :: IO ()  
add_one = do  
	x <- readLn  
	putStrLn (show (x + 1))

ghci> add_one 1
2
```

### `forever`
`forever` repeats an `IO` action forever and is in the `Control.Mondad` package.

**For Example:**
```
ghci> import Control.Monad  
ghci> forever (putStrLn "hi")  
hi  
hi  
hi  
hi  
...
 
import Control.Monad  
import Data.Char

process :: IO ()  
process = do  
	putStrLn "Give me some input: "  
	l <- getLine  
	putStrLn (map toUpper l)
 
main = forever process
```

>The second example above continues to ask the user for an input before printing that input out in upper case forever.

### `sequence`
`sequence` performs a list of IO actions.

**For Example:**
```
ghci> :t sequence
sequence :: [IO a] -> IO [a]

ghci> sequence [getLine, getLine, getLine]  
one  
two  
three
["one","two","three"]
```

>The final line is the return value of `sequence`

`sequence` works well with map.

**For Example:**
```
ghci> sequence . map print $ [1,2,3]  
1  
2  
3  
[(),(),()]
```

### `mapM`
`sequence . map` was such a commonly used pattern that `mapM` was added. It essentially does the same thing.

**For Example:**
```
ghci> mapM print [1,2,3,4]  
1  
2  
3  
4  
[(),(),(),()]
```

### `when` and `unless`
`when` executes an IO action if a condition is true and `unless` executes an IO action if a condition is false.

**For Example:**
```
ghci> :t when
when :: Bool -> IO () -> IO ()

ghci> when True (print "hi")  
"hi"  
ghci> when False (print "hi")  
ghci>  

ghci> :t unless
unless :: Bool -> IO () -> IO ()

ghci> unless False (print "hi")  
"hi" 
ghci> unless True (print "hi")
ghci> 
```

>`when` and `unless` are in the `Control.Monad` package.