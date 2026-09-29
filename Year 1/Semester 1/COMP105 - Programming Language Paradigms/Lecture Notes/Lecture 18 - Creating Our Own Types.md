## Topics

- The `type` keyword
- the `data` keyword
- Records

## The `type` Keyword
The `type` keyword allows you to give a new name to an existing type. All types must start with capital letters.

**For Example:**
```
type String' = [Char]
 
exclaim :: String' -> String'  
exclaim str = str ++ "!"

ghci> exclaim "hello"  
"hello!"
```

>`type` is useful when you want to give a meaningful name to a complex type

**For Example:**
```
type VoteResults = [(Int, String)]

results :: VoteResults  
results = [(2, "red"), (1, "blue"), (1, "green")]
  
ghci> head results  
(2,"red")
```

>The above gives a name to the structure of vote results from the last lectures `av_voting` example. Something like this makes the code much more readable.

## The `data` Keyword
The `data` keyword is used to create entirely new types

**For Example:**
```
data Bool' = True | False  
```

The above is an implementation of the `Bool` type.
`|` should be read as "or" and each value after the `=` is a constructor that returns a value of that type. 

So `:t True` = `Bool'`.

**A Unique Example:**
```
data Direction = North | South | East | West
 
rotate North = East  
rotate East = South  
rotate South = West  
rotate West = North

ghci> :t rotate  
rotate :: Direction -> Direction
```

>The above defines a new type that can take 1 of the 4 main compass directions. `North`, `South`, `East`, `West`. It defines a function `rotate` that takes one of these values and returns the next direction when rotated clockwise.

### Type Classes
By default a new data type is not part of any type class.

```
ghci> rotate North  

No instance for (Show Direction) arising from ...
```

>Observe that GHCI cannot show the result of `rotate North` since `Direction` is not part of the show type class.

Using the `deriving` keyword we can indicate that we want a new data type to be part of an existing type class.

**For Example:**
``` 
data Direction = North | South | East | West  
deriving (Show)

ghci> rotate North  
East  
```

Haskell can automatically implement the following type classes for us:
- Show – will print out the type as it is in the code  
- Read – will parse the type as it is in the code  
- Eq – the natural definition of equality  
- Ord – constructors that come first are smaller

### Complex Constructors
More complex constructors can contain other types

**For Example:**
```
data Point = Point Int Int deriving (Show, Read, Eq)
  
ghci> Point 1 4
Point 1 4
 
ghci> read "Point 10 10" :: Point  
Point 10 10
  
ghci> Point 2 2 /= Point 3 1  
True
```

The above creates point type which represents a point in 2d space by using 2 `Int`s.

While this may seem unnecessary since you could just use a tuple (Int, Int), this sort of thing can be very useful in terms of readability. Especially with more complex examples.

>It's important to realise as well that the name of the data type `Point` and the constructor `Point` are technically different. Haskell allows us to use the same name as the type for the constructor for convenience. It can tell from context which is the type and which is the constructor.
>
>Any time it appears in a type annotation it is the type, any time it appears in a function body, or parameter it is the constructor.

To pull the data out from a complex constructor you need to use pattern matching.

**For Example:**
```
shift_up (Point x y) = Point x (y+1)  
ghci> shift_up (Point 1 1) 
Point 1 2

ghci> :t shift_up  
shift_up :: Point -> Point

--OR

move :: Point -> Direction -> Point
  
move (Point x y) North = Point x (y+1)  
move (Point x y) South = Point x (y-1)  
move (Point x y) East = Point (x+1) y  
move (Point x y) West = Point (x-1) y
  
ghci> move (Point 0 0) North  
Point 0 1
```

>To do pattern matching inside of a function you can use the `case` syntax, this will be covered in the notes from the next lecture.

Types can have multiple complex constructors containing different types.

**For Example:**
```
data Shape = Circle Float | Rect Float Float 
	deriving (Show)

ghci> :t Circle 2.0  
Circle 2.0 :: Shape
 
ghci> :t Rect 3.0 4.0  
Rect 3.0 4.0 :: Shape

area :: Shape -> Float  
area (Circle radius) = pi * radius**2  
area (Rect x y) = x * y
 
ghci> area (Circle 2.0)  
12.566371
  
ghci> area (Rect 3.0 4.0)  
12.0
```

>Observe above that the `Shape` type can either represent a circle, with one float value indicating it's radius, or a rectangle with 2 float values indicating its width and height.

## Records
You can use data types to build custom records.

**For Example:**
```
data Person = Person String String Int String
 
get_first_name (Person x _ _ _) = x  
get_second_name (Person _ x _ _) = x  
get_age (Person _ _ x _) = x  
get_nationality (Person _ _ _ x) = x
 
ghci> get_age (Person "joe" "bloggs" 25 "UK")  
25
```

The above is pretty hard to read so Haskell provides us with a record syntax to make this easier.

**For Example:**
```
data Person = Person {  firstName :: String,  
						secondName :: String,  
						age :: Int,  
						nationality :: String}  
									deriving(Show)

ghci> Person "joe" "bloggs" 25 "UK"  
Person {firstName = "joe", secondName = "bloggs", age = 25, nationality = "UK"}
```

>This makes the types much easier to read as each attribute is given an explicit name.

When creating a record like this, Haskell automatically creates "getter" functions for each of the attributes.

**For Example:**
```
gchi> let joe = Person "joe" "bloggs" 25 "UK"  
gchi> firstName joe  
"joe"

ghci> secondName joe  
"bloggs"
```

This syntax also allows for you to create records while passing attributes out of order. You cannot do this without record syntax.

**For Example:**
```
data Example = Example { a :: String, b :: Int}  
	deriving (Show)
	
ghci> Example "one" 2  
Example {a = "one", b = 2}
 
ghci> Example {b = 3, a = "zero"}  
Example {a = "zero", b = 3}
```