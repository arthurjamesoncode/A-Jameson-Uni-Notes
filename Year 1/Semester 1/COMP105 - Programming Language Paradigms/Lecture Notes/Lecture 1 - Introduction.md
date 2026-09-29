## Programming Paradigms
There are a few different programming paradigms, which change the way in which we are able to write code. Some programming languages only support one paradigm and enforce code to be written in that paradigm, other programming languages can support multiple and you can choose in which paradigm you want to write code.

Most programming languages are what we call **Imperative** these are the languages you are likely to have experience in and you can a see list of many of them below.

**Imperative Languages:**
Ada, ALGOL, BASIC, Blue, C, C++, C#, Ceylon, CHILL, COBOL, D, eC, FORTRAN, GAUSS, Go, Groovy, Java, Javascript, Julia, Lua, MATLAB, Machine language, Modula-2, Modula-3, MUMPS, Nim, Oberon, Object Pascal, Pascal, Perl, PHP, PROSE, Python, Ruby, Rust, Swift, Wolfram Language

Other programming languages are called **Functional**, this is the focus of this course and you can see a list of many of these below.

**Functional Languages:**
Agda, Charity, Clean, Coq (Gallina), Curry, Elm, Frege, Futhark, Haskell, Hope, Idris, Joy, LISP, Mercury, Miranda, OCaml, Owl Lisp, Purescript, QML, SAC, SequenceL, Scheme, SML

If we look at an example we can see how these paradigms are different to each other.
### Factorial Example
Consider the **factorial** function from maths. $n$ factorial, is given by $$
n\times(n-1)\times(n-1)\times \cdot\cdot\cdot \times2\times1
$$so `factorial(5)` would compute $$
5\times4\times3\times2\times1=120
$$
In Python, an imperative language, we can implement this like so:
```
def factorial(n):
	answer = 1
	current = 1
	while current <= n:
		answer = answer * current
		current = current + 1
	return answer
```
Imperative languages, like this, tells a machine how to compute the answer by:
- Defining some variables
- Executing some code within a loop
- Repeating this code until a condition is met

However if you were a mathematician you would write $$
\text{factorial}(n) =
\begin{cases}
n \times \text{factorial}(n) & \text { if } n > 0 \\
1 & \text { if } n=0
\end{cases}
$$Functional programming allows us to define functions in a very similar way.

Python, while an imperative language, does allow us to write code in a functional way as well.

Written in Python using a functional approach we can get
```
def factorial(n):
	if n > 1:
		return n * factorial(n-1)
	else:
		return 1
```

The big difference between this an coding in an imperative way is this way:
- No variables are declared
- No explicit loops are used (instead we use recursion)

These are the hallmarks of functional programming.
## This Module
In this module both functional and imperative programming are studied, but, as this module is designed for people who have experience with imperative programming languages, the focus is on the functional style with a bit of time spent comparing the two styles.

This module teaches Haskell, a pure functional language. This means that Haskell enforces code to written in a functional way, you can do imperative programming easily in Haskell.
### Why Functional Programming
Learning functional programming can help you in a few ways.

Firstly there are many industrial users of functional programming, such as Jane Street, Credit Suisse, Facebook. On top of this parallel systems are becoming more prominent, such as multi-core GPUs etc, and functional programming is great for these systems.

Although, it's certainly true that most industrial programming will be done in an imperative language. However, learning functional programming can help you become a better imperative programmer.

This is because most imperative languages still support functional programming, and sometimes the functional style is more appropriate for certain problems. Being aware of all the tools at your disposal can only help you.

Also, learning functional programming can help prepare you for computer science education. This is because algorithms in CS are often presented in a functional way, and we use the functional paradigm in the analysis of algorithms. This means that knowing functional programming can help you translate all of this into real code.
