---
cssclasses:
  - flashcards
---
## Code Translation
### What is code translation?
Code translation is the process of turning **source code** into **object code**. It can also refer to turning one programming languages source code into another
### What types of code exist and what are they?
- **Source code** is high level code written so that humans can understand it
- **Byte code** is low level code written to be executed by an interpreter or virtual machine
- **Assembly code** is low level code written in a CPU dependent assembly language
- **object code** is as low level as you can get, and uses a specific instruction set and registers. This is what the CPU can understand.
### What programs do we use for code translation?
- **Compiler** - Translates source code into a lower level form and stores the resulting code in a file (for languages such as C, C++, etc.)
- **Interpreter** - Translates source code and performs its actions directly (for languages like Python, JavaScript)
- **Assembler** - Translates low level mnemonics (assembly code) into object code stored in a file.
- **Linker** - Combines object code files and library code into a final executable image (`.exe` file)
### What types of code are hardware dependent?
Assembly language and object code depend on the hardware of the system which executes them.

Source code and byte code are compiled/interpreted into hardware dependent code.
### What are the benefits of compilers over interpreters?
| Compiler                                                                                                                 | Interpreter                                                 |
| ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------- |
| They translate the whole file, and therefore have the full context as they can look ahead of the current instruction<br> | They translate line by line and therefore cannot look ahead |
| Compilation process is fast                                                                                              | The interpretation process is slower                        |
| Compiled code runs faster                                                                                                | Interpreted code runs much slower                           |
| You only need to compile once per executable                                                                             | You must interpret the code every time you run it           |
| They can check for syntax and semantic errors                                                                            | Can only check for syntax errors                            |

### What are the benefits of interpreters over compilers?
| Compiler                                  | Interpreter                                                               |
| ----------------------------------------- | ------------------------------------------------------------------------- |
| Can have complicated tools<br>            | Easier programming environment                                            |
| Syntax errors harder to locate by line    | Syntax errors easier to identify by line                                  |
| Needs careful organisation of source code | Useful for quick prototyping                                              |
| Debugging can be complicated              | Usually have better/easier debugging tools                                |
| Generated code is platform locked         | Source code is useable on any platform which has the required interpreter |
### How is Java code translated to object code?
Java uses a compiler `javac` to translate `.java` files into byte code files. These byte code files are then run by the Java Virtual Machine.
### What two types of compiler exist?
The two types of compiler are:
- Single pass - Go line by line generating object code as they go (early compilers)
- Multi pass - Read the file into an internal data structure before generating object code (modern compilers)
### What are the benefits of multi pass compilers?
- They can look at the whole file and perform optimisations. 
- The programmer can use things defined lower down in the file itself.
### What is linking?
Linking is the process of joining together all the different object files into a single executable image.

This links together all the different compiled source code and library functions.
### What are the components of a programming language?
Every programming language has 3 components:
- The lexical component - A list of all legal keywords and their meaning
- The syntactical component - The form and structure of legal expressions
- The semantic component - Adds meaning to legal expressions
### What is a grammar?
A grammar is a set of formal syntax rules. 

Simple rules are defined in terms of elementary symbols/keywords and more complex rules are defined in terms of these simple rules.
### What is a token?
A token is the smallest possible group of characters that has a valid meaning.
### What is Extended Backus-Naur Form?
EBNF is a precise grammar used by the compiler. 

It defines production rules from other non-terminal rules and terminal symbols.
### What does EBNF syntax look like and mean?
```EBNF
if-else = “if”, “(“, bool-expression, “)”, code-block, [ “else”, code-block ] ; 

code-block = statement | “{“, { statement }-, “}” ;
```

The names of rules are on the left before the `=`. On the right is a valid expression.

The full syntax meanings are below
![[iso_ebnf.png]]
## The Compilation Process
### What are the 5 steps of compilation?
Compilation involves 5 main steps:
- Lexical Analysis
- Syntax Analysis
- Semantic Analysis
- Code Generation
- Code Optimisation
### What is lexical analysis?
Lexical analysis is also known as **scanning**, and so we call the program which does this a **scanner**. 

A scanner uses whitespace and punctation to identify relevant sequences of characters. This is often implemented as a **finite state machine** and some can use **backtracking** to look at surrounding context. 

This turns the code into a series of **lexemes** (tokens).
### What types of tokens are there?
There are 6 types of token:
- Identifiers - Variable, parameter, method/function names
- Keywords - Language specific words which have a function
- Separators - Brackets and Punctuation
- Operators - Mathematical symbols which can be evaluated
- Literals - Strings, numbers, or other constant values
- Comments - These are completely removed since they only provide value to the programmer, not the execution of the program
### What is Syntax Analysis?
Syntax analysis is also known as **parsing**, and so we call the program that does it a **parser**.

This is the stage where the list of tokens is checked to see if forms a valid program.

The parser knows all the **grammars** for the language. It checks the sequence of tokens to see which rules they match. This is often implemented as a recursive algorithm with backtracking. 

The output of a parser is an **abstract syntax tree** (AST).
### How does the parser know that the syntax is correct?
The syntax is correct if the entire list of tokens can be matched to a sequence of valid rules. 

If one or more tokens cannot be matched, then there must be a syntax error which stops the compiler and outputs a message.
### What is semantic analysis?
Semantic analysis adds meaning to the program:
- Each identifier is added to a **symbol table**
- Type checking (if applicable) is performed
- Variable usage and function calls are bound to their definitions
- Memory requirements are determined for variables, parameters, etc.
All of this information is used to augment the nodes of the syntax tree.

The outputs of this step are the **augmented syntax tree** and the **symbol table**.
### When does the semantic check fail?
The compiler will stop and output a message if a semantic check fails:
- If there is a type mismatch
- If undeclared variables are used
- If a reserved keyword is used as an identifier
- If an identifier is declared multiple times
- Using a variable not in the current scope
### What is code generation and how does it work?
Code generation turns the abstract syntax tree into actual machine code instructions.

First, it adds instructions to reserve enough memory for each variable in the **symbol table**. 

Then it walks through each node in the syntax tree and turns them into instructions the CPU can understand. As long as the compiler walks node by node the code will be generated in the correct order.

The code generator must:
- Specify the correct instructions based on the CPU instruction set
- Select the appropriate registers to hold variables during calculations
- Create a subroutine (with a label) for every high level function in the syntax tree
- Add jump instructions to implement each condition and loop in the syntax tree
- Add call, push, pop instructions to set up subroutines with correct parameters
- Add debugging information (optionally) so the programmer can step through code.

The generated machine code is the output of the compiler.
### What is compiler code optimisation?
During compilation the code is analysed to see if there are ways to:
- Reduce the amount of code
- Eliminate repeated operations
- Reorganise parts of the program to execute faster
### When can code optimisation happen?
During:
- Scanning
- Parsing
- Code Generation
### How many optimisation techniques do we need to know and what are they?
We need to know 9 optimisation techniques:
- **Remove redundancy** - Store calculated results so that they can be used again later instead of performing the calculation again
- **Remove code** - Remove unnecessary calculations and intermediate variables
- **Unroll loops** - (Sometimes) Generate the same instructions in a linear manner instead of jumping back in the code. In some cases this helps with CPU instruction pre-fetching.
- **Reverse loops** - Make it so the loop counter counts in the opposite direction. We saw in [[Lecture 4 - Loops, Arrays, and Subroutines#For Loop|this lecture]] how this can decrease the number of required instructions.
- **Increase Locality** - Put related code and data near each other in memory. This helps ensure that following the principle of locality is beneficial to performance.
- **Use parallelism** - Make use of multiple CPU cores by identifying and arranging instructions which can be performed concurrently
- **Fold constants** - Replace calculations that use constants with their results instead of performing the calculations.
- **Move loop invariant code** - See below
- **Strength reduction** - see below
### What is loop invariant code, and how can it be optimised?
Loop invariant code is code that computes a result every iteration of a loop despite the computation not changing.

It can be optimised by moving it before the loop.
### What is strength reduction?
Strength reduction is when less efficient code is replaced with more efficient code. For example
```c
sum = 0
for(int i = 0; i <= n; i++) {
	sum = sum + i;
}
```
becomes
```c
sum = n * (1 + n) / 2
```
### What must the linker do after compilation and how?
After compilation the linker must combine all the different object code files into a single executable image. 

It can do this because it can see the symbol table in each object file and imported library
- It will look for a symbol call `main` which it treats as the starting point of the file
- It will cross-check symbol tables to make sure every reference is valid
### What will cause the linker to output an error?
The linker will stop and output an error message if:
- The code uses a symbol that isn't defined
- There is no symbol called `main`