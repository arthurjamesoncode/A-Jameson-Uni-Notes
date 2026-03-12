## If
In order to do more complicated things in a programming language, we need to be able to make some conditional decisions. This comes in the form of `if` statements.

In imperative languages, `if` changes the control flow.
```
if (x == 10) {
	//do stuff
} else {
	//do other stuff
}
```
So if a condition is true, some code is run. If it is false, some different code is run.

This concept does not exist in functional programming, but we do still have an if.
```
gt10 x = if x > 10 then "yes" else "no"
```

You can view `if` in Haskell as a function that takes 3 arguments:
- Argument 1 is a boolean condition - in our example `x > 10`
- Argument 2 is the value to be returned if argument 1 evaluates to `true` - in our example `"yes"`
- Argument 3 is the value to be returned if argument 1 evaluates to `false` - in our example `"no"`

The only difference between `if` and the other functions we've seen is that it requires us to write `then` before our second argument and `else` before our third argument.

In imperative languages, the `else` statement is optional, as sometimes you only want to run code if a condition is true and otherwise you don't want to run anything.

In a functional language, the `else` statement is mandatory, as `if` is a pure function and all pure functions **must** return a value.

So
```
f x = if x > 10 then 1 else 0
```
is fine but 
```
f x = if x > 10 then 1
```
will cause an error.

In Haskell, it is also true that both branches of an `if` statement must have the same type. This is because Haskell is a strongly typed language, and functions are only allowed to return a single type.

This is something we will come back to in a later lecture, but for know just understand that
```
if x == 1 then 1 else 0
--AND
if x /= 1 then "Yes" else "No"
```
are correct if statements and that 
```
if x > 10 then 1 else "no"
```
will cause an error.

So the full structure of an if is 
```
if A then B else C
```
where `A` evaluates to a boolean value and `B` and `C` evaluate to the same type.

You can place any function, as long as it returns the correct type, in place of `A`, `B`, or `C` allowing you to create very complex `if` statements.

The functional if does actually exist in a lot of imperative languages and is called the **ternary operator**.
## Let
Sometimes we want to use an expression multiple times. For example:
```
f x = (x * x - 4) + sqrt (x * x - 4)
```

The problem is that it is clunky and unreadable to write out `(x * x - 4)` twice and so we can use a `let` expression to give this a label. So instead we can write
```
f x = let s = (x * x - 4) in s + sqrt s 
```

The syntax for a `let` expression is:
```
let <bindings> in <expression>
```
Where:
- `<bindings>` gives names to some expressions;
- `<expression>` uses those bindings

You can also bind more than 1 name in a let expression. Meaning you can do
```
f x = let a = x; b = x^2 in a + b
```

Importantly, when you create a `let` expression, you are **NOT** defining variables. The value of variables can change over the run time of a subroutine, This is not the case for bindings defined in `let` expression. These bindings are simply **labels** for expressions.

This means that 
```
f x = let a = x * x; a = a + 1 in a
```
gives an error.

You can use let to bind names in `ghci`
```
ghci> let a = 1 
ghci> let b = 2 
ghci> max a b 
2
```
### The Layout Rule
Often it is cleaner to display code over multiple lines, but we need to consider Haskell's' layout rule.

Haskell's layout rule is that each definition at the same level should start on exactly the same column. 

You can see examples of this below:
```
f x y z = 
	let 
		a = x * x 
		b = y * y 
		cc = z * z 
	in 
		a * a + b * b

cylinder r h = 
	let sideArea = 2 * pi * r * h 
		topArea = pi * r ** 2 
	in sideArea + 2 * topArea
```
Notice how in these examples, we don't need to separate bindings by using `;` since each binding is on it's own line.

You can ignore the layout rule if you use `{}` to surround your blocks of code. However, when doing that you must separate different "lines" of code with `;`. I recommend never doing this since the layout rule makes code easier to read.


