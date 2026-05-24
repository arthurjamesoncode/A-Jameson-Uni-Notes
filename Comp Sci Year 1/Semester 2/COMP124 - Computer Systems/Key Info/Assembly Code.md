## Assembly Language Overview
### What is assembly language?
Assembly language is a human readable version of machine code. It uses simple mnemonics to represent machine code instructions.
### How do we convert assembly language to machine code?
We convert assembly language to machine code using an assembler.
### What makes up a line of assembly code?
A line of machine code can be seen below
![[assembly_code_line.png]]
- A **label** can refer to the address of an instruction, or the address of a data item.
- The **mnemonic** and its **operands** are directly translated into machine code.
- **Comments** start with a semi colon

**Instruction labels** and **comments** are optional and can be any word. They're purpose is only to make the written code much more readable.
## Registers & Operations
### What general purpose registers can we use when writing assembly code?
The general purpose registers available to us include:
- **EAX** - accumulator register
- **EBX** - base register
- **ECX** - counter register
- **EDX** - data register
### What purposes are typical for these registers?
Some typical uses are:
- We store **calculations** in the **accumulator register, EAX**
- We store **loop iterations** in the **counter register, ECX**
### How can we access certain parts of the accumulator register?
We can refer to specific parts of the EAX with:
- AL - The least significant byte
- AH - The second least significant byte
- AX - The two least significant bytes
- EAX - The full 32 bits
- RAX - The full 64 bits in a 64 bit system
### What operation can we use to transfer data and how?
We can use the `mov` operation to transfer data for example:
```
mov eax, ebx
```
The first operand is the destination, the second operand is the source. The data is not deleted from the source so `mov` functions like a copy.
### What maths operations are available?
There are maths operations available for:
- Adding - `add`
- Subtracting - `sub`
- Multiplying - `mul`
- Dividing - `div`
### How is each one used?
`add` takes two operands:
- The first **must** be a register containing a value
- The second can be any value
The result is stored in the first operand

`sub` takes two operands:
- The first must be a register containing a value
- The second can be any value
- The second value is subtracted from the first
The result is stored in the first operand

`mul` takes one operand:
- It must be a register holding the value to multiply by
- The value in the first operand is multiplied by the value in `eax`
The result is stored in `eax`

`div` takes one operand:
- It must be a register holding the divisor (denominator)
- The numerator is made up of the the `edx` and the `eax`
- The `edx` is the most significant 4 bytes
- The `eax` is the least significant 4 bytes
- Computes a quotient and remainder
The quotient is stored in `eax` and the remainder is stored in `edx`
## Status Flags, Jumps, & Loops
### What is the status flags register?
The status flags register stores a number of boolean values. Each bit of the register represents a different flag.
### What flags are needed for this module?
We care about 4 flags for this module, and they are:
- **CF** - carry flag - previous operation had a carry from the most significant bit
- **ZF** - zero flag - previous operation had a zero result
- **SF** - sign flag - previous operation had a negative result
- **OF** - overflow flag - previous operation was too big to fit in memory
If the conditions above aren't satisfied all of these flags are 0, otherwise they are 1. 
### What is the unconditional jump instruction?
`jmp` is the unconditional jump instruction
### How many flag jump instructions are there for this module and what are they?
There are 8 flag jump instructions, 2 for each flag. These are:
- `jc` - jump if carry flag is set
- `jnc` - jump if carry flag is not set
- `jz` - jump  if zero flag is set
- `jnz` - jump if zero flag is not set
- `js` - jump is sign flag is set
- `jns` - jump is sign flag is not set
- `jo` - jump if overflow flag is set
- `jno` - jump if overflow flag is not set
### What does the `cmp` instruction do?
The `cmp` instruction compares two values. Internally this command subtracts one operand from the other without changing either operand. If the values are the same, this sets the zero flag.
### How many compare jump instruction are there and what are they?
There are 6 jump instructions which rely on the `cmp` instruction
- `je` - ==
- `jne` - !=
- `jg` - >
- `jge` - >=
- `jl` - <
- `jle` - <=
These instructions only work if they immediately follow a `cmp` instruction
### How can we construct loops and how can they be optimised?
Loops can be created by combining conditional jumps with compare instructions.

We can optimise a for-loop slightly by counting down instead of up. This let's us skip the `cmp` instruction and use `jnz` to jump back only if the last operation had a non-zero result.

For example:
```
	   mov ecx, 10  ; use count register to count iterations 
floop: add sum, ecx ; update sum 
	   dec ecx      ; decrease loop counter  
	   jnz floop    ; if the loop counter is not 0, go round again
```
### What does the `loop` command do?
The `loop` command decrements `ecx` by one and then jumps if `ecx` is not 0.
## Memory Addresses, & Arrays
### How can we get the memory address of a declared variable?
We can get the memory address of a declared variable (in a C wrapper as shown in the labs) by using the `lea` command.

`lea` stands for "load effective address" and loads the memory address of the second operand into the first operand (which must be a register).
### How do we pass a value stored at an address (which is stored in a register) as an operand?
If we want to pass the value at an address which is stored in a register as an operand we need to use **register indirect mode**.

We indicate register indirect mode by using square brackets. For example:
```
lea ebx, age   ; age is arbitrary label
mov eax, [ebx] ; register indirect mode
```
### What is an array?
An array is a collection of items (of the same size) stored consecutively in memory.
### How can we access their elements in assembly code?
We can access the elements of an array in assembly code by accessing the memory location of the first element of the array and adding an offset. This works because we know the size of each element.
## The Stack
### What is a stack data structure and what operations can be performed on it?
A stack is a last in first out (LIFO) data structure. It has two main operations:
- **push** - add something to the stack
- **pop** - remove something from the stack
### Where are stacks used for programs running on the CPU?
Each program/process running on the CPU has it's own stack. This is stored in the the main-memory (RAM) allocated for that program/process. The base of the stack is the "top" (highest index) of the memory allocated for that process. 
### How does the stack grow?
The stack grows downwards in memory.
### What is `esp`?
`esp` is the Stack Pointer Register. It points to the current "top" (really bottom) of the stack.
### What is stack overflow?
Stack overflow is when the program instructions and the stack overlap. I.e. `esp` is less than `eip`.
### What do the stack operations look like for machine level stacks?
The `push` instruction:
- Decrements **ESP** so it points to the next free area of memory on the stack;
- Writes the data item in the register operand to that address (the *top* of the stack).

The `pop` instruction:
- Moves the data addressed by **ESP** into the given register
- Increments **ESP** by the correct amount to remove the item from the stack. Note that the data still remains in memory until we overwrite it.
### How can we quickly remove multiple items from a machine level stack?
Since the stack grows downwards in memory we can quickly remove multiple items by **adding** to the value of the stack pointer. If every item is 4 bytes `add esp, 8` would remove 2 items (and so on).
## Subroutines & Calling Conventions
### What is a subroutine?
A subroutine is a portion of code that can be run repeatedly (called) with different pieces of data (parameters).
### How do we write and call subroutines in assembly?
Any subroutine starts at a label and ends with a `ret` instruction. To call the subroutine we use the `call` instruction.
### Where is the return address for a subroutine call stored?
The address that `ret` returns to is stored on the stack.
### What are the `call` and `ret` instructions actually doing?
The `call` instruction:
- Takes the current value of the instruction pointer and **pushes** it onto the stack;
- Puts the address of the subroutine into the instruction pointer;
- Therefore causes the next instruction to be fetched to be the first instruction in the subroutine.

The `ret` instruction:
- **Pops** the top item off the stack and places it into the instruction pointer;
- Therefore cause the next instruction to be fetched to be the instruction after the original `call` instruction.

### How do we pass parameters to a subroutine?
We can pass parameters by either:
- Placing them into registers
- Placing them onto the stack
### What does "pass by value" and "pass by reference" mean?
When we pass parameters by either of these ways we either:
- Pass them by value - Pass their actual values into the subroutine
- Pass them by reference - Pass their memory locations into the subroutine
### How are return values stored?
Return values can either use registers or the stack the same as parameters.
### What is a calling convention?
When subroutines are written and called the caller and callee must agree on a number of things:
- What order the parameters will be pushed to the stack?
- Is the caller or callee responsible for clean up?
- Where the return value will be placed?

A calling convention is an agreement of who does what.
### What must the caller/callee do if responsible for clean up?
If the caller is responsible for cleaning the stack, they must access stacked parameters using the stack pointer and an offset.

If the callee is responsible for cleaning the stack, they must pop the parameters as it uses them after popping and saving the value of the return address.
### What calling conventions are there for Intel x86 architecture?
The Intel x86 architecture defines 4 calling conventions:
- **cdecl** – Push parameters on stack in reverse order (right to left); **caller** cleans stack 
- **fastcall** – First two parameters in ECX/EDX, rest reversed on stack; **callee** cleans stack 
- **stdcall** – Push parameters on stack in reverse order; **callee** cleans stack
- **thiscall** – First parameter in ECX, rest reversed on stack; **callee** cleans stack 
## External Subroutines & IO
### What calling convention must we use for C subroutines?
We must follow the cdecl calling conventions for C subroutines. This means we:
- Push the parameters to the stack in reverse order
- The caller cleans the stack
### How can we output things to the console?
We can output text to the console using the `printf` subroutine from C. 

It takes the parameters (in order):
- A string which may contain format specifiers
- Any number of values which should fit those format specifiers in order
### How can we take input from the console?
We can take input from the console using the `scanf` subroutine from C.

It takes the parameters (in order):
- A format specifier as a string
- The memory address where the data should be stored

### What is a format specifier and what format specifiers do we need to know for this course?
Format specifiers tell a program what kind of data you are expecting.

We need to know 4 format specifiers for this course. They are:
- `%d` - decimal integer
- `%s` - string
- `%c` - character
- `%f` - floating point number
### What is a call preserved register and how do we save values of non-call preserved registers?
A call preserved register is a register whose values are automatically preserved by any C library routines. 

If a register is not call preserved its value must be pushed onto the stack before any parameters are pushed and the call is made. 

It can then popped back into the register after the call has returned and the stack has been cleaned (if the caller must clean stack).
### What registers are call preserved?
There are 5 call preserved registers. They are:
- **ESI** - Source index register (Not used in any code on this module)
- **EDI** - Destination index register (Not used in any code on this module)
- **EBX** - Base register
- **EBP** - Stack base pointer
- **ESP** - Stack pointer


## Local Variables and Stack Frames:
### What are local variables?
Local variables are variables which only exists for the run time of a subroutine and cannot be accessed anywhere else?
### How can we store local variables in assembly code?
We can store local variables on the stack.
### What is a stack frame?
A stack frame holds all the data needed by a specific subroutine such as:
- Parameters
- Return address
- Local variables
There can be many stack frames on the stack at any given time
### What is `ebp` and how can we use it?
`ebp` is the stack base pointer. This points to the start of the current stack frame.

We don't need to use `ebp` to access anything since we already have `esp` and the `pop` and `push` instructions, but we could use `ebp` with an offset to access things near the start of the stack frame.

I think this would be bad practice though, since it goes against the FIFO nature of the stack and could cause problems if you were, for instance, saving the values of non-call preserved registers.
### How are stack frames and nested stack frames built?
Before any subroutine is called:
- **ESP** always points to the top of the stack
- **EBP** initially points to the base of the stack

When a subroutine is called:
- Parameters are pushed onto the stack first;
- The return address is then pushed;
- The value of **EBP** is then pushed;
- Local variables are reserved on the stack, causing **ESP** to change further.
- The current value of **ESP** is put into **EBP**, beginning a new stack frame.

When the subroutine is ready to return:
- Local variables are popped/removed from the stack;
- The top value is popped into **EBP**, restoring the previous stack frame;
- The top value is popped into **EIP**, moving the execution back the return address;

![[nested_stack_frames.png]]
## Recursion & String Handling
### What is recursion?
Recursion is when a function calls itself. Recursive functions will have some kind of "base case" that ensures that they do not go on forever.
### How can we do recursion in assembly code?
We can do recursion in assembly code by checking for our base case and using conditional jumps to determine what is done.
### What are strings?
Strings are collections of characters. For this module we only care about ascii characters meaning each character only takes up one byte.

The last byte of a string is used to store the string terminator character (NUL or 0).
### How can we load and manipulate strings in assembly?
In assembly we load the address of the first character and continuing to read and manipulate characters until we get to the string terminator.

To get the first character of a string we can do
```asm
lea eax, msg
movzx edx, byte ptr [eax]
```
`movzx` stands for "move zero extend" and essentially means to pad the rest of the register with 0s. The `byte ptr` instructions tell the `movzx` instruction that the address passed to it is actually a pointer to a single byte in memory. 
### How can we get the length of a string?
We can get the length of the string by using the external `strlen` subroutine from C.

To use it we need to include it in our code
```C
#include <string.h>
```

It takes a single parameter, the address of the string.

We call it with the `cdecl` calling convention.