## Code Translation
Code translation is the process of turning **source code** into **object code**:
- **source code** is high level meaning that the statements and structure are written so that humans can understand it
- **object code** is as low level as you can get, and uses a specific instruction set and registers. This is what the CPU can understand.

We use a number of programs for code translation:
- **Compiler** - Translates source code into a lower level form and stores the resulting code in a file (for languages such as C, C++, etc.)
- **Interpreter** - Translates source code and performs its actions directly (for languages like Python, JavaScript)
- **Assembler** - Translates low level mnemonics (assembly code) into object code stored in a file.
- **Linker** - Combines object code files and library code into a final executable image (`.exe` file)

Generally when we say **compiled** we mean translated from one code format to another lower level format. For example Java compiles into byte code and TypeScript is compiled into JavaScript etc. Neither byte code or JavaScript are object code and both are run by an interpreter.

>The lecture slides say that a compiler compiles into **object code**, although as stated above this is not necessarily true.
>
>I am just nit-picking the slides though since it mentions byte code by name on the next slide.
## Types of Code
There are different types of code depending on the stage of compilation.

You can see a figure below which illustrates this
![[types of code.png]]

We refer to code which is **platform independent** as **portable**. Essentially this means that it does not matter which hardware it runs on. We use this to describe:
- Source code
- Any interpreted code (like intermediate Byte Code)

If we use a compiler which targets a specific platform then we turn high-level **platform independent** source code into **platform dependent** object code. This is a necessary step for the specific CPU to be able to understand our programs.

Similarly, **interpreters** (such as the JVM) are also **platform dependent**. There will be different versions of the JVM on Windows and Mac machines. This is what allows the same source code or byte code to run on different hardware.
## Compilers VS Interpreters
Compilers translate a piece of source code to another type of code. This could be byte code, object code, or another language.

For simplicity we will think of compilers as only translating into object code or machine code.

Compilers translate the whole of a source program into machine code, and keep the translation and execution phases separate. See below:
![[compiler_flow.png]]

Interpreters take a single line at a time, determine what the hardware needs to do to execute it, and then executes it. This means the translation and execution phases are the same. The only executable file which exists is the interpreter.

They both have their advantages and disadvantages.

**Pro Compiler Points:**

| Compiler                                                                                                                 | Interpreter                                                 |
| ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------- |
| They translate the whole file, and therefore have the full context as they can look ahead of the current instruction<br> | They translate line by line and therefore cannot look ahead |
| Compilation process is fast                                                                                              | The interpretation process is slower                        |
| Compiled code runs faster                                                                                                | Interpreted code runs much slower                           |
| You only need to compile once per executable                                                                             | You must interpret the code every time you run it           |
| They can check for syntax and semantic errors                                                                            | Can only check for syntax errors                            |
**Pro Interpreter Points:**

| Compiler                                  | Interpreter                                                               |
| ----------------------------------------- | ------------------------------------------------------------------------- |
| Can have complicated tools<br>            | Easier programming environment                                            |
| Syntax errors harder to locate by line    | Syntax errors easier to identify by line                                  |
| Needs careful organisation of source code | Useful for quick prototyping                                              |
| Debugging can be complicated              | Usually have better/easier debugging tools                                |
| Generated code is platform locked         | Source code is useable on any platform which has the required interpreter |
### New Programming Languages
New languages are regularly created to solve niche problems (or just as fun projects). It is much easier to design an interpreter and easier to code in an interpreted language.

As a result, **newer languages tend to be interpreted**.

However there will always be a need for compilers and people who understand them. This is because the interpreter of a new language must be a **platform dependant** executable file, which means a compiled language is necessary to write the code for the interpreter. 

You could write an interpreter in another interpreted language, but eventually a compiler will be needed somewhere for anything to run on the CPU.
## Java
Java uses both a compiler (`javac`) and an interpreter (the JVM). This requires the Java Development Kit (JDK) to be installed on the programmer's system. 

The source code is compiled into intermediate byte code using the `javac` command, and then run through the JVM interpreter using the `java` command.

The end user must have the Java Runtime Environment (JRE) installed on their system. 

You can see the full flow below
![[javac_java_flow.png]]

Python uses a similar approach. It compiles source code into byte code and then immediately interprets it. The user never evens sees the byte code.
## Types of Compiler
Early compilers were **single pass** compilers. This means that they move through the source code line by line and generate object code as they go. 

This is faster and uses less memory than the modern approach but has some fairly big disadvantages:
- It cannot perform any optimisations on the code.
- Requires all variables and symbols to be declared before they are used in the text of the file.

Modern compilers are **multi pass**. This means they read the entire source file into an internal data structure before they convert it to object code.

This is slower and uses more memory than **single pass** compilers but have some big advantages:
- Can look at the whole file and perform optimisations
- Allows the programmer to use things they define later in the file

These compilers run multiple times:
- The first run reads the whole file into the data structure
- All subsequent runs read from this data structure, not the file
- The middle runs perform optimisations
- The final run generates the object code
### Linking
There can be a lot of different source files which all have a corresponding object file. These source files can also reference library code which also exists in multiple object files.

To pull all of these together into a final executable program image, we need to use a **linker**.

You can look to the figure below for a visualisation:
![[linker_flow.png]]

Linking can either be **static** or **dynamic**. The difference between these was covered in [[Lecture 16 - Memory Manager, Addresses, & Segmentation#Using Library Routines|this lecture]].
## Programming Languages
Programming languages are all built off of a similar set of components:
- The lexical component
- The syntactical component
- The semantic component

The **lexical component** is a list of all **legal keywords** allowed in the language, and there meaning (the action/effect of the keyword). This is things like `import`, `public`, `else`, `while`, etc.

The **syntactical component** defines the form and structure of **legal expressions** in the language. For example, in java:
```java
double private x;
```
gives a syntax error but
```java
private double x;
```
does not.

The semantic component adds meaning to **legal expressions**, which are made from keywords and syntax structures. This defines what should be done when executing a particular fragment of code. For example, it defines which action should be taken when the code is an `if-else` statement:
- Test the condition
- Execute `if` part if true
- Execute `else` part if false

We need to have a precise description of a programming language so that the translator can:
- Analyse the source code 
- Apply optimisations
- Generate correct and unambiguous object code

A **grammar** is a set of formal syntax rules. Simple rules are defined in terms of elementary symbols/keywords and more complex rules are defined in terms of these simple rules.

A single source file is just a text file that contains characters. The translator groups characters together into **tokens** which represent keywords, brackets, etc.

A **token** is the smallest possible group of characters that has a valid meaning. Grammar rules define the correct order of tokens. 

We can represent grammar rules as a set of diagrams. This can make  it easier for us to understand.

You can look below to see an example diagram of an `if-else` expression and a `code block` expression.
![[syntax_diagram.png]]

Expressions are formed from one or more tokens. Some expression contain other expressions, like how an if-else statement contains a boolean expression and 2 code blocks. We call these expressions **non-terminal**.

Other expressions are **terminal** meaning they are defined in their final form with simple characters. This could be something like a 
**boolean expression** or an **arithmetic expression**. These would be 
## Extended Backus-Naur Form
The translator uses a more precise grammar called **extended Backus-Naur form** (EBNF).

This defines production rules from **non-terminal rules** and **terminal symbols**.

The EBNF grammar looks like this
```EBNF
if-else = “if”, “(“, bool-expression, “)”, code-block, [ “else”, code-block ] ; 

code-block = statement | “{“, { statement }-, “}” ;
```

Terminal symbols are defined in quotes, either single or double (up to the programmer).

The comma character concatenates expressions and symbols to form new expressions. 

EBNF syntax uses symbols to mean certain things. This is why, if we want to match these symbols (such as semi-colons or square brackets), we must indicate so by using quotes.

Every aspect of the language must be defined this way. For reasonably complex languages there will be hundreds of rules. Java, for example, has about 120.

There are multiple types of EBNF and so you will see slightly different syntax depending on which reference you look at. For this module we will be using **ISO EBNF**.

![[iso_ebnf.png]]

Let's see if we can define some EBNF rules for numbers.
```EBNF
digit    = "0"|"1"|"2"|"3"|"4"|"5"|"6"|"7"|"8"|"9";
unsigned = {digit}-;
integer  = unsigned | "+", unsigned | "-", unsigned
fraction = ".", unsigned;
decimal  = unsigned | fraction | unsigned, fraction;
```
A programming language using these grammar rules is now equipped to recognise any type of number.

We can also use EBNF to define rules for **legal identifiers** in a language.
```ebnf
lower = “a”|”b”|”c”|”d”|”e”|”f”|
        ”g”|”h”|”i”|”j”|”k”|”l”|
        ”m”|”n”|“o”|”p”|”q”|”r”|
        ”s”|”t”|”u”|”v”|”w”|”x”|
        ”y”|”z”; 
upper = “A”|”B”|”C”|”D”|”E”|”F”|
        ”G”|”H”|”I”|”J”|”K”|”L”|
        ”M”|”N”|“O”|”P”|”Q”|”R”|
        ”S”|”T”|”U”|”V”|”W”|”X”|
        ”Y”|”Z”; 
letter = lower | upper; 
varname = letter, { letter | digit };
```

This rule in plain English is: "variable names must start with a letter, and can be made up of letters and digits"

Now given a string of characters we can work out whether we have a valid match:
- `zbcv99` is valid
- `a9fg28p` is valid
- `7ghbgf` is invalid
- `!56tgfh` is invalid

If you wanted to allow underscores we could change the `varname` rule to 
```ebnf
varname = letter, { letter | digit | "_"};
```

If we wanted to allow a single optional underscore at the start of a variable name we could change the rule to
```ebnf
varname = [ "_" ], letter, { letter | digit | "_"};
```

The compiler will try and match the source code against the EBNF grammar of the language. The language itself uses whitespace, brackets and semicolons to help provide structure.

A syntax error is generated if the translator cannot match **every** part of the source code to an EBNF grammar. The error messages often won't point to the exact line where the problem happened.