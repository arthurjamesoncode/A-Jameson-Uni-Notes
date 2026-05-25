## The Compilation Process
Compilation involves 5 main steps:
- Lexical Analysis
- Syntax Analysis
- Semantic Analysis
- Code Generation
- Code Optimisation

The compiler analyses the entire code at each step. Meaning they can view each line of code with the surrounding context/ This means that efficient and optimised machine code can be generated.

Interpreters use the first three steps to find the next instruction but, since they can't look ahead, they can't do any optimisations.

The Java compiler uses all 5 steps to produce optimised bytecode that is then interpreted by the Java Virtual Machine.
## Lexical Analysis
Lexical analysis is also known as **scanning**, and so we call the program which does this a **scanner**.  

A scanner uses whitespace and punctation to identify relevant sequences of characters. This is often implemented as a **finite state machine** and some can use **backtracking** to look at surrounding context. 

This turns the code into a series of **lexemes** (tokens).

After this step the compiler has a list of the tokens which make up the program:
- Identifiers - Variable, parameter, method/function names
- Keywords - Language specific words which have a function
- Separators - Brackets and Punctuation
- Operators - Mathematical symbols which can be evaluated
- Literals - Strings, numbers, or other constant values
- Comments - These are completely removed since they only provide value to the programmer, not the execution of the program

Take the following line of source code 
```
total = (a + b) * vat;
```

The scanner will split this into a list of tokens based on whitespace and punctuation. The list from this line of code will be
```
IDENTIFIER total
EQUALS
OPEN_PAREN
IDENTIFIER a
PLUS
IDENTIFIER b
CLOSE_PAREN
MULTIPLY
IDENTIFIER vat
SEMICOLON
```

This list of tokens is then passed to the next step: **Syntax Analysis**.
## Syntax Analysis (Parsing)
Syntax analysis is also known as **parsing**, and so we call the program that does it a **parser**.

This is the stage where the list of tokens is checked to see if forms a valid program.

The parser knows all the **grammars** for the language. It checks the sequence of tokens to see which rules they match. This is often implemented as a recursive algorithm with backtracking. 

The output of a parser is an **abstract syntax tree** (AST).

The syntax is correct if the entire list of tokens can be matched to a sequence of valid rules. If one or more tokens cannot be matched, then there must be a syntax error which stops the compiler and outputs a message.

The AST arranges the raw list of tokens we were given by the **scanner** into a data structure which represents all the different parts of the code. This is what is passed to the next step.

If we define a simple modulo function like so
```c
int modulo(int x, int y) { 
	int result = (x % y); 
	return result; 
}
```

We can then run the C compiler to see it's syntax tree
![[ast_example.png]]

>Stuart glosses over this bit so I don't think we would be asked to construct an AST in the exam.
## Semantic Analysis
Semantic analysis adds meaning to the program:
- Each identifier is added to a **symbol table**
- Type checking (if applicable) is performed
- Variable usage and function calls are bound to their definitions
- Memory requirements are determined for variables, parameters, etc.
All of this information is used to augment the nodes of the syntax tree.

The compiler will stop and output a message if a semantic check fails:
- If there is a type mismatch
- If undeclared variables are used
- If a reserved keyword is used as an identifier
- If an identifier is declared multiple times
- Using a variable not in the current scope

The outputs of this step are the **augmented syntax tree** and the **symbol table**.
## Code Generation
Code generation turns the abstract syntax tree into actual machine code instructions.

First, it adds instructions to reserve enough memory for each variable in the **symbol table**. Then it walks through each node in the syntax tree and turns them into instructions the CPU can understand. As long as the compiler walks node by node the code will be generated in the correct order.

The code generator must:
- Specify the correct instructions based on the CPU instruction set
- Select the appropriate registers to hold variables during calculations
- Create a subroutine (with a label) for every high level function in the syntax tree
- Add jump instructions to implement each condition and loop in the syntax tree
- Add call, push, pop instructions to set up subroutines with correct parameters
- Add debugging information (optionally) so the programmer can step through code.

The generated machine code is the output of the compiler.

>Some compilers may convert to assembly code first, but most go straight to machine code. 
>
>Since machine code is not readable, it may be helpful to imagine them changing to assembly code only. The example we show does this.

Using the C compiler we can view the generated assembly code for the `module` function we created. 
![[generated_assembly.png]]

## Code Optimisation
During the optimisation step the code is analysed to see if there are any ways to:
- Reduce the amount of code
- Eliminate repeated operations
- Reorganise parts of the program to execute faster

Code Optimisation is not really is own separate step, it can happen during:
- Scanning
- Parsing
- Code Generation

There are a lot of techniques which you can read about [here](https://en.wikipedia.org/wiki/Optimizing_compiler), but all the ones within the scope of the module will be talked about in the remainder of this note.

There are a lot of simple code optimisation techniques:
- **Remove redundancy** - Store calculated results so that they can be used again later instead of performing the calculation again
- **Remove code** - Remove unnecessary calculations and intermediate variables
- **Unroll loops** - (Sometimes) Generate the same instructions in a linear manner instead of jumping back in the code. In some cases this helps with CPU instruction pre-fetching.
- **Reverse loops** - Make it so the loop counter counts in the opposite direction. We saw in [[Lecture 4 - Loops, Arrays, and Subroutines#For Loop|this lecture]] how this can decrease the number of required instructions.
- **Increase Locality** - Put related code and data near each other in memory. This helps ensure that following the principle of locality is beneficial to performance.
- **Use parallelism** - Make use of multiple CPU cores by identifying and arranging instructions which can be performed concurrently
- **Fold constants** - Replace calculations that use constants with their results instead of performing the calculations.

There are also some slightly more complicated ways to optimise code. We will go over these now:
### Loop Invariant Code
Take the following for loop
```c
for(int i = 0; i <= n; i++) {
	foo = amp + 5
	sum = sum + (foo * i)
}
```

In this loop the value of `foo` is calculated every iteration. However `5` is a constant and `amp` doesn't have it's value changed by the loop so calculating this every time is redundant. This is an example of **loop invariant code**.

As part of the code-optimisation step the compiler will look for loop invariant code and move it to before the loop. So the above for loop would become
```c
foo = amp + 5
for(int i = 0; i <= n; i++) {
	sum = sum + (foo * i)
}
```
### Strength Reduction
Consider the following for loop
```c
sum = 0
for(int i = 0; i <= n; i++) {
	sum = sum + i;
}
```

This loop can be removed completely and replaced with the simple calculation 
```c
sum = n * (1 + n) / 2
```

>You can see a proof that these are the same thing in [[Lecture 8 - Indirect Proof Continued and Proof By Induction]] from the COMP109 module

This statement always gives the same value but uses fewer instructions and variables, and completely removes the need to jump back in machine code.

Strength reduction replaces less efficient code with more efficient code if possible.

These kinds of optimisations can make the code harder to understand. If you were unfamiliar with the proof/trick you may not understand that
```c
sum = n * (1 + n) / 2
```
sums all integers between 0 and n but the less efficient loop is much clearer to a human.
## Linking Phase and Symbol Resolution
A large program will be split across multiple source files and each file is compiled separately into its own object file.

Source files often refer to each other or libraries through `import`, `#include` etc. This lets symbols that we define in 1 file to be used in another.

The linker is responsible for combining individual object files into the final executable image:
- It can see the symbol table in each object file and imported library
- It will look for a symbol call `main` which it treats as the starting point of the file
- It will cross-check symbol tables to make sure every reference is valid

The linker will stop and output an error message if:
- The code uses a symbol that isn't defined
- There is no symbol called `main`