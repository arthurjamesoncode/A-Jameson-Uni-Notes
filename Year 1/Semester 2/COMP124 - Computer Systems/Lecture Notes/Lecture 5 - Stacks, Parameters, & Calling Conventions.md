## How Do We Return After Calls
At the end of [[Lecture 4 - Loops, Arrays, and Subroutines|Last Lecture]], we started to talk about subroutines.

We move to the start of a subroutine by using the `call` instruction. We then use the `ret` instruction to return to where we called from.

So how does `ret` know where to send us back to?

We could use a special register in the CPU to store the return address, and then, when we want to return, we can just move that instruction back to the instruction pointer.

But then how do we handle nested calls and returns? Most complex programs use multiple subroutines that call each other in a nested manner, and if we used this register system then as soon as we make a second call we lose the return address for the first call.

So we need a way to store an arbitrary number of nested return addresses. We can't use CPU registers because we can't predict how many we'll need, and deeper levels of nesting will need more storage. 

This means that we will need to store them in **main memory**, specifically in a **stack**.
## The Stack
Stacks exist in high level programming as a useful data structure, which stores and retrieves values in a specific order.

They are **"Last In, First Out" (LIFO)** data structures. Think about a stack of plates, you can only take the top one off, and if you want to add something to the stack you have to place it on the top, meaning the plate placed most recently will have to come off first.

For comparison, **queues** are **"First In, First Out" (FIFO)** data structures.

Stacks have 2 operations:
- **push** - add something to the stack
- **pop** - remove something from the stack

A stack exists for each process that happens on the CPU, and lives in the **main memory** allocated to that process.

It's treated separately from the rest of memory, and is accessed directly through CPU registers.
### Machine Level Stacks
The Intel x86 architecture uses main memory for the stack, but accesses it through a register. **ESP**, the stack pointer register, always points to the memory address of the top item in the stack.

>Note that, although we refer to things being **on top** of the stack, the stack actually grows downwards in memory.

The `push` instruction is used to add something to the stack. It:
- Decrements **ESP** so it points to the next free area of memory on the stack;
- Writes the data item in the register operand to that address (the *top* of the stack).

The `pop` instruction is used to remove something from the stack It:
- Moves the data addressed by **ESP** into the given register
- Increments **ESP** by the correct amount to remove the item from the stack. Note that the data still remains in memory until we overwrite it.

It is the job of the programmer to keep the stack clean and ensure that items are removed when no longer needed.

Below you can see how the memory is laid out.
![[memory_layout.png]]
You can see that the program and the stack start at opposite sides of the allocated memory. If it is ever the case that the stack grows so large that it overlaps the program in memory, we call this a **stack overflow** error.
### Call and Return
Now we can define precisely what we mean by call and return in terms of subroutines.

The `call` instruction:
- Takes the current value of the instruction pointer and **pushes** it onto the stack;
- Puts the address of the subroutine into the instruction pointer;
- Therefore causes the next instruction to be fetched to be the first instruction in the subroutine.

The `ret` instruction:
- **Pops** the top item off the stack and places it into the instruction pointer;
- Therefore cause the next instruction to be fetched to be the instruction after the original `call` instruction.

The use of the stack means nested subroutines will return properly because the top-most return address on the stack will be from the most recent `call` instruction.
### Manipulating the Stack Pointer
We can change the value of **ESP** directly from our code. When doing so we have to be careful of **pushes** and **pops** so that everything matches up.

Manipulating `esp` allows us to quickly clean off multiple bytes if we don't need the data. We'll often do this after pushing parameters for a subroutine call.

To take 8 bytes off the stack, since it grows downwards, we add 8 to the value of `esp`:
```
add esp, 8
```

Remember that items on the stack are still in memory, but no longer available. It will be overwritten by the next `push` instruction.

We can still inspect the content of any memory location by using the value in `esp` and an offset value.
## Subroutine Parameters

### Pass by Value
A simple subroutine like the one below, uses **pass by value**, meaning that the values the subroutine needs are copied into registers which will then be used by the subroutine.

The below code, places the values of 2 numbers into the accumulator and base register and then calls `bigger`. Inside bigger the values are compared and if the value in the accumulator is smaller, the bigger value is moved into it.

The subroutine then returns to the instruction after the call, which places the value in the accumulator into the `max` variable (which would be defined in C++).
```
; SUB bigger 
bigger: cmp eax, ebx 
		jl second 
		ret 
second: mov eax, ebx 
		ret 
; END bigger 
… 
mov eax, num1 
mov ebx, num2 
call bigger 
mov max, eax 
…
```

> It's worth noting that this is purely for example, we would never need a subroutine like this as `cmp` is already a command.

This method of passing parameters requires the **caller** and **callee** to agree on which registers to use for the parameter and the return value.
### Pass by Reference
Consider a subroutine that swaps two variables, meaning it exchanges values in memory.

For this subroutine, it would need to know the addresses of each variable not just the values. To make a subroutine like this we would need to **pass by reference**, meaning that we pass the memory addresses as parameters.

```
; SUB swap 
swap: mov ecx, [eax] 
	  mov edx, [ebx] 
	  mov [ebx], ecx
	  mov [eax], edx 
	  ret 
; END swap 
… 
lea eax, num1 
lea ebx, num2 
call swap …
```

>Recall that `lea` stands for "load effective address" and moves the address of a variable into a register.

To pass parameters this way, we still need the **caller** and the **callee** to agree on which registers to use.

Note that the `xchg` instruction in intel x86 architecture swaps the values inside two registers. One operand can be a memory label but this is slow due to **locking**. For info on this view [[Lecture 18 - Threads, Concurrency, & Race Conditions]].
### Stacking Parameters
In the examples given above, we use registers to pass the parameters to the subroutine. This is fine for subroutines with only a few parameters, but:
- There are only a few registers and they might already be in use for other data
- The caller and callee must agree on which registers to use 

This can be very limiting, and therefore a better way to pass parameters is to **push them to the stack**:
- The caller pushes the parameters before making the call
- The callee pops (or otherwise accesses) the parameters and performs it's computation

After passing parameters in this way the stack must be **cleaned**.

The caller and callee must both agree on both the order of the parameters and who cleans the stack.

For example consider the program below:
```
; SUB area
area: pop ebx
	  pop edx
	  pop eax
	  mul edx
	  push ebx
	  ret
; END area

...

push width
push height
call area
mov result, eax
```
In this example the callee, the subroutine itself, cleans the stack. 

Before call is used, the parameters `width` and `height` were pushed onto the stack. When `call` is used the return address is pushed onto the stack.

This means that inside the subroutine, the return address is **popped** into the base register, the parameters are then moved into the accumulator and data register, and the return address (still in the base register) is pushed back onto the stack after the calculation and before the `ret` instruction.

Now consider the example below:
```
; SUB area
area: mov eax, [esp+4]
	  mul [esp+8]
	  ret
; END area

...

push width
push height
call area
add esp, 8
mov result, eax
```
In this example the caller cleans the stack.

The data this time is accessed by using the value in `esp` with an offset, `[esp+offset]` is the syntax for that. This means we don't need to store the return address, as it always stays at the top of the stack.

The stack is then cleaned afterwards by the `add esp, 8` line directly following the `call area`
line.
## Calling Conventions
The caller and callee need to agree a calling convention:
- What order will the caller push parameters to the stack
- If callee is responsible for clean-up it must pop parameters as it uses them. It must also pop and save the value of the return address.
- If caller is responsible for clean-up it must access parameters using the stack pointer and an offset. It must take into account the return address when calculating offset.
- Where will the return value be placed (in the examples above this is `eax`.

Forgetting about the return address will lead to unexpected results.
### Intel x86 Calling Conventions 
The Intel x86 (32-bit) architecture defines four calling conventions 
- **cdecl** – Push parameters on stack in reverse order (right to left); **caller** cleans stack 
- **fastcall** – First two parameters in ECX/EDX, rest reversed on stack; **callee** cleans stack 
- **stdcall** – Push parameters on stack in reverse order; **callee** cleans stack
- **thiscall** – First parameter in ECX, rest reversed on stack; **callee** cleans stack 

The previous examples illustrated **stdcall** (Example A) and **cdecl** (Example B) 

The **fastcall** and **thiscall** conventions are ‘faster’ if you have few parameters but they ‘pollute’ the registers that might be better used for something else.

In future lectures we will call external C libraries to help with input and output. These library routines expect us to use the cdecl convention (C declaration). External code is a ‘black box’ so we don’t know which registers it uses or modifies