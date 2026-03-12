## Functions
A **function** is something which takes an input and produces an output. For example the function `square(x) = x^2` takes and produces the following inputs and outputs:
- Input 1 - Output 1
- Input 2 - Output 4
- Input 3 - Output 9
- etc.

This is the mathematical definition of functions, which differs slightly from functions in most programming languages.

Below you can see an example of a function in the imperative programming language, Python.
```Python
def square(x):
	return x * x
```

As you can see this works identically to the square function we wrote above, but *functions* in  python, or other imperative languages. can actually do a lot more than functions in maths. We call these types of functions **subroutines**, and the functions from maths **pure functions**. 

We will go over the difference in a bit, but it is important to note that every function can be implemented as a subroutine, but some subroutines are **not** functions.
### Pure Functions
In a pure function the only thing that matters is the inputs and outputs. The specific implementation of the function does not matter and we can treat it as a black box. 

This is because pure functions:
- Have no side effects, meaning that they never affect the **global** state;
- Always return a value;
- Are deterministic, meaning that the same inputs will always result in the same outputs.

This means that pure functions only affect the world through their return values, allowing us to not care about the implementation details as all that matters is what we get out of the function.

Subroutines do not have to follow either of these rules. They can have side effects, don't have to return a value, and they can be stochastic (non-deterministic).

This means that we need to understand how things are implemented when we are using subroutines as the implementation details could affect the result that we get.

When using pure functions it's always true that
```
f(1) + f(2) = f(2) + f(1)
```
but when using subroutines whether 
```
f(1) + f(2) = f(2) + f(1)
```
depends on the specific implementation of `f`. If `f` has side effects that change depending on the order the functions are called they won't be the same. If `f` involved randomness such as choosing a random number between 0 and it's input the results may not be the same.
## Functional Programming
In functional programming, **everything is a pure function.** We build everything out of pure functions, and combine simple functions to get more complex ones.

This leads to a completely different style of programming, but still allows us to do everything that imperative programs can.

Imagine an imperative language where every subroutine only has 1 line and immediately returns a value. That's a lot closer to what functional programming is.

Every line of a functional program has the form
```
f(x) = <an expression or another function>
```
and we build functions from other functions
```
f(x) = square(x) + x

g(x) = h(i(x), j(x))
```

Functional programming has no concept of a variable as variables rely on side effects to operate, meaning that a pure function cannot use variables.

Functional programming doesn't allow loops as loops require variables to operate. Functional programming uses recursion instead.

In fact there is no **control flow** at all, everything is a function application. Things are defined by applying functions to different things, and nothing else.
### Necessary Side Effects
Sometimes we need side effects. This is mostly true when communicating with the user in some way. Our programs need to show something on the screen, or read some input from the keyboard. 

These are examples of side effects, so how do functional languages manage this?

The answer is that they allow ways to perform IO operations, but only a small amount of the code needs to communicate. The rest can be pure functional.

In terms of this module, we will study the pure functional bit first and come back to IO near the end. You can look to [[Lecture 21 - IO]] and further to see how this works, but you may not understand much if you skip ahead.