## Assembly Language
The CPU sees only binary numbers in memory, but writing code directly in binary is too hard and too prone to mistakes. 

Because of this, **assembly language** was created. This is still a very low level language, but instead of using numbers we use 3 character **mnemonics** to represent opcodes. The registers that we interact with are also given labels.

An **assembler** is used to turn our code into an executable sequence of instructions. This, while similar, is not the same as compilation of a high level program, as each line of assembly code translates to a single machine code instruction.

You can see below an example line of code, which has been annotated to show each component.
![[assembly_code_line.png]]
- A **label** can refer to the address of an instruction, or the address of a data item.
- The **mnemonic** and its **operands** are directly translated into machine code.
- **Comments** start with a semi colon
- **Instruction labels** and **comments** are optional and can be any word. They're purpose is only to make the written code much more readable.

We will be writing assembly code for the **32-bit Intel x86** architecture using **Intel** syntax. Note that the **Intel 64-Bit** architecture is called **x64**, so be careful not to get them mixed up.

Some text books and online resources use **AT&T** syntax, which will not work. If you see **%** and **$** symbols you are looking at **AT&T** syntax.
![[syntax_example_both.png]]

To make it easier to write compile and debug assembly code, we will place inside a C++ wrapper and use Visual Studio. This allows us to declare variables in C and access functions in the C standard library.

You won't need to know C or C++, just use the template and place your assembly code in the right place, which is inside the `_asm` block, called the **inline assembler**.

Our programs will look like this:
![[example_program.png]]
## Intel x86 Registers
The intel x86 CPU has a lot of registers, and we will not use most of them on this module. We have talked about **IP**, the instruction pointer, and **IR**, the instruction register in [[Lecture 2 - CPU, Fetch Execute Cycle and Instruction Sets]].

There are also 4 general purpose registers:
- **EAX** - accumulator register
- **EBX** - base register
- **ECX** - counter register
- **EDX** - data register

Notice that the **mnemonics** for these registers all start with **E** and end with **X**. The letter in the middle is the same as the first letter of the name given to them.

The names given to these registers are arbitrary. They are a convention, nothing more. I recommend sticking to conventions when programming, especially when programming in a group, as they make collaboration and debugging easier, but it is important to recognise them as just that.

Some typical uses for these registers are:
- We store **calculations** in the **accumulator register, EAX**
- We store **loop iterations** in the **counter register, ECX**

We will look at some more registers later in this course. 
## The Accumulator
Most CPUs have an accumulator register. The accumulator, **EAX**, is used for general purpose data storage and computation.

Depending on which part of the accumulator we want to access, we can refer to it by different names:
- **AL** - Refers to the first 8 least significant bits
- **AH** - Refers to the second 8 least significant bits
- **AX** - Refers to the first 16 least significant bits
- **EAX** - Refers to the full 32-bits
- **RAX** - Used when working with 64 bit systems to access the full 64-bits. We will not use this.

So for example:
- If we want to put, or move, 42 into the accumulator we can do `mov eax, 42`
- If we want to move the 16 least significant bits of a variable, `count`, into the accumulator we can do `mov ax, count`
- If we want to move the ASCII value of `'x'` into the least significant byte of the accumulator we can do `move al, 'x'`
- If we want to increment, add one to, the value in the accumulator, we can do `inc eax`.
- If we want to add 10 to whatever's in the accumulator we can do `add eax, 10`

Note that in all the examples of code above, the first operand is the destination and the second operand is the source. This is the opposite of **AT&T** syntax.
## Move Operations
We are going to go over a bunch of examples of how to use the move command `mov`. As stated above, the destination is the first operand and the source is the second operand. It is worth noting that the source operand is not changed or erased, so `mov` is actually more like a copy command.

You can move from register to register:
```
mov eax, ebx
```

You can move from memory to a register (foo is the label of the memory, this would be declared as a C variable):
```
mov eax, foo
```

You can move from a register to memory:
```
mov foo, eax
```
This overwrites whatever was in that memory.

You can put a numeric value into a register:
```
mov eax, 12
```

Or put a numeric value into memory:
```
mov foo 12
```

You cannot move directly from memory to memory, you must use a register in between.

Last lecture [[Lecture 2 - CPU, Fetch Execute Cycle and Instruction Sets]] we saw that there may be a different machine code instruction depending on where the operand is stored. When writing assembly code we don't really need to worry about this, as the assembly will handle this for us.
## Maths Operations
Remember that a single line of high level code turns into multiple machine instructions.

So 
```
int num = count1 + count2 - 10
```
is really
```
mov eax, count1
add eax, count2
sub eax, 10
mov num, eax
```
where the accumulator stores the result of each step.

Addition and subtraction work as you would expect with the given register. Remember that the register where the result is stored must be the first operand.

Multiplication, however, only takes a single operand, which must be a register. It multiplies whatever is in the accumulator by the value in the operand and stores it in the accumulator.

So
```
mov eax, 10
mov ebx, 12
mul ebx
```
Actually stores 120 in the accumulator.

Division is also a bit trickier. 

Division uses a 64-bit dividend where:
- The most significant 4 bytes are formed from the data register and
- The least significant 4 bytes are formed from the accumulator

The divisor must be stored in another register.

So if we wanted to do $120\div 9$ then we could do
```assembly
mov ebx, 9   ; places our divisor into the base register
mov edx, 0   ; clears the most significant 32 bits of the dividend
mov eax, 120 ; places our dividend into the accumulator
div ebx      ; divides our dividend by our divisor
```

Division in assembly is integer division, meaning that the result will be an integer and there may be a remainder. The result of a division is stored in the accumulator, while the result is stored in the data register.

This operation will set some status flags if the result is too big or if you try to divide by zero.
## Status Flags Register
The Intel x86 CPU has a special register where each bit represents a true/false status. There are many flags that we will not use, but there are a few which are of interest to us.

These are:
- **CF** - carry flag - previous operation had a carry from the most significant bit
- **ZF** - zero flag - previous operation had a zero result
- **SF** - sign flag - previous operation was positive (0) or negative
- **OF** - overflow flag - previous operation was too big to fit in memory

We can use jump instructions to check flags and take appropriate action.

## Jumps
An unconditional jump uses the mnemonic `jmp` and will move the instruction pointer to the given address label.

So we could do
```
	   mov eax, 10
begin: add eax, 10
	   jmp begin
```
This would create an infinite loop as the `jmp` command unconditionally always moves back to the previous line. This would result in 10 being added to the value in  accumulator repeatedly until the value gets too big and there is an overflow.

Jumping is unrestricted, but make sure to take care to avoid "spaghetti" code with jumps all over the place.

This forms the basis of implementing loops in assembly code but we obviously want them to terminate properly, which requires some conditional jumps.
### Conditional Jumps
A conditional jump will only happen if a certain condition is true. If the condition is false, the instruction pointer just moves to the next instruction. This allows us to write code that behaves the same as an if statement, or a loop, in high level languages.

There are various jump instructions that test different status flags:
- `jc` - jump if carry flag is set
- `jnc` - jump if carry flag is not set
- `jz` - jump  if zero flag is set
- `jnz` - jump if zero flag is not set
- `js` - jump is sign flag is set
- `jns` - jump is sign flag is not set
- `jo` - jump if overflow flag is set
- `jno` - jump if overflow flag is not set

You can see that the mnemonics for these do something to help you remember the action. `j` means jump, `n` pretty much always means "not" or "no", and the last character is the first letter of the flag that it tests.

So, for example:
```
num = num - 10;
if (num == 0) {
	num = 100;
}
```
Is the same as
```
	   mov eax, num
	   sub eax, 10
	   jnz store
	   mov eax, 100
store: move num, eax
```

In both cases the end result depends on the value of `num`. If `num` is 10 at the start, it will be replaced with 100. Otherwise, it will be decremented by 10 and that is it.

In the high level code, it's easy to see the code block that belongs to the `if` statement. If the condition is true, we run some code we otherwise would not.

In the assembly code, we reverse the condition to make it more efficient. If the condition is false, we skip the code we would execute if the condition is true.

The `cmp` instruction compares two values. Internally this command subtracts one operand from the other without changing either operand. If the values are the same, this sets the zero flag.

So `cmp eax, ebx` compares the values stored in `eax` and `ebx`. If we place a jump instruction directly after this we can respond to the result:
- `je` - jumps if the operands are equal
- `jne` - jumps if the operands are not equal
- `jg` - jumps if the first operand is greater than the second
- `jle` - jumps if the first operand is less than or equal to the second
- `jl` - jumps if the first first operand is less than the second
- `jge` - jumps if the first operand is greater than or equal to the second

It's very important to remember that these jump instructions only work as expected if they immediately follow a `cmp` instruction.

So using this we can implement an IF-ELSE statement in assembly.

```
if (num > 0) {
	pos = pos + num;
} else {
	neg = neg + num
}
```
is the same as
```
	   mov eax, num
	   cmp eax, 0
	   jg postv
negtv: add neg, eax
	   jmp endif
postv: add pos, eax
endif: ...
	   ...
```

You can assume this statement is part of a loop that reads numbers from the user and keeps running totals of the positive and negative umbers entered.

If the number is negative the first jump doesn't happen but then we must jump `jmp` to the `endif` label to avoid executing the code to handle positive numbers.