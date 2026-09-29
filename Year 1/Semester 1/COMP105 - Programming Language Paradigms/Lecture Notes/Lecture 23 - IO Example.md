## Topics

- IO Actions that Return Things
- Extended Programming Example

## IO Actions That Return Things
IO Actions can return information. The last line of a `do` block determines the type.

**For Example:**
```
The last line of a do block determines the return type  
get_two_ints =  
	do  
		x <- getLine  
		y <- getLine  
		let ret = (read x + read y) :: Int
		return ret
```

>Notice in the above example that the `:: Int` is required to tell Haskell what type `ret` would be. 
>
>Haskell can assume a `Num` type from the use of `+` and would have to assume a specific type that works at run-time (by default `Integer`) but it is still best to explicitly give these types. 
>
>If you give an explicit type annotation, like `get_two_ints :: IO Int` you wouldn't need to give this type explicitly in the function.

Any type can be returned in the `IO` box.

**For Example:**
```
get_char_bool :: IO (Char, Bool)  
get_char_bool =  
	do  
		x <- readLn  
		y <- readLn  
		return (x, y)
```

We can also build complex types by using this.

**For Example:**
```
get_lines :: IO [String]  
get_lines = do  
	x <- getLine  
	if x == ""  
		then return []  
		else do  
			xs <- get_lines  
			return (x : xs)
```

>Notice that we have to unbox and rebox the output of the recursion. 
>
>You won't see this until later but you can actually optimise this by using tail recursion.

## Extended Programming Example
This example will be to build a program that can print out words in ASCII art.

**For Example:**
```
  #   ###  ###    #   ###  
 # #  #  # #  #  # #  #  #  
#   # ###  ###  #   # ###  
##### #  # #  # ##### #  #  
#   # #  # #  # #   # #  #  
#   # ###  ###  #   # ###
```

We will use a list of strings to store a screen.

The list `["## ## ##", " ## ## ", "## ## ##"]` represents this screen:
```
##  ##  ##  
  ##  ##  
##  ##  ##
```

To print out a screen we can use a recursive IO action

**For Example:**
```
print_screen :: [String] -> IO ()  
print_screen [] = return ()  
print_screen (x:xs) =  
	do  
		putStrLn x  
		print_screen xs
```

Or we could use `mapM` like this :
```
print_screen :: [String] -> IO [()] 
print_screen = mapM putStrLn
```

>The second one is obviously cleaner, and since we would never use the value of `print_screen` anyway it does not matter that the type is `IO [()]` vs `IO ()`.

I'm going to skip over the rest of the pure code, but you can read it yourself if you are curious.

```
-- Creates a blank screen
make_screen :: Int -> Int -> [String]  
make_screen width height = [replicate width ' ' | _ <- [1..height]]

blank_screen = make_screen 40 6

modify_list :: [a] -> Int -> a -> [a]  
modify_list list pos new =  
	let  
		before = take pos list  
		after = drop (pos+1) list  
	in  
		before ++ [new] ++ after

-- changes a character at a certain point in a screen
set :: [String] -> Int -> Int -> Char -> [String]  
set screen x y char =  
	let  
		line = screen !! y  
		new_line = modify_list line x char  
		new_screen = modify_list screen y new_line  
	in  
		new_screen

-- sets a list of changes
set_list :: [String] -> [(Int, Int, Char)] -> [String]  
set_list screen [] = screen  
set_list screen ((x,y,c) : xs) = set (set_list screen xs) x y c

-- example letters
letter_a :: [(Int, Int, Char)]  
letter_a = map (\ (x, y) -> (x, y, '#')) [  
		(2, 0), (1, 1), (3, 1), (0, 2), (4, 2),  
		(0, 3), (1, 3), (2, 3), (3, 3), (4, 3),  
		(0, 4), (4, 4), (0, 5), (4, 5)  
	]
	  
letter_b :: [(Int, Int, Char)]  
letter_b = map (\ (x, y) -> (x, y, '#')) [  
		(0, 0), (1, 0), (2, 0), (0, 1), (3, 1),  
		(0, 2), (1, 2), (2, 2), (0, 3), (3, 3),  
		(0, 4), (3, 4), (0, 5), (1, 5), (2, 5)  
	]

-- Shifts a letter 1 space to the right
shift_letter :: [(Int, Int, Char)] -> Int -> [(Int, Int, Char)]  
shift_letter letter shift = map (\ (x, y, c) -> (x + shift, y, c)) letter
```

The following code shows how all of the above pure code can be combined into a big IO action.

```
big_letters :: [String] -> Int -> IO ()  
big_letters screen cursor =  
	do  
		c <- getLine  
		let letter = case head c of  
				'a'       -> letter_a  
				'b'       -> letter_b  
				otherwise -> []  
			new_screen = set_list screen (shift_letter letter cursor)
	print_screen new_screen  
	big_letters new_screen (cursor + 6)
```

The above code takes a line of input from the user and takes the head of this line. If it is one of the stored letters it adds this letter to the screen but shifted by the cursor. 

>The cursor is a value passed to the function that shows where the last letters end.

It then prints the new screen and recursively calls itself moving its cursor over by 6. This obviously only works for a monospace ascii art font with a size of 6.

We can turn this into a program like so:

```
main :: IO ()  
main = big_letters blank_screen 0
```

You could also make it a program that takes command line arguments that indicate the height and width of the screen.

```
Import System.Environment

main :: IO ()  
main = do
	[width_str, height_str] = getArgs
	let width  = read width_str
		height = read height_str
	screen = make_screen width height
	big_letters screen 0
```

