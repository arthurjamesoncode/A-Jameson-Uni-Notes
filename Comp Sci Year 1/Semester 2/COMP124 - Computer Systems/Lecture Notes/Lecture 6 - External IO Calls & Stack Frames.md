## External Subroutines 
Input and output are difficult in pure assembly coding but generally this is how it would work:
- Specific registers would be used to point to the address of either the **source** of the output data or the **destination** for the input data.
- A CPU interrupt would be triggered to pass control to the operating system.
- Device drivers would then handle the I/O by liaising with hardware.

This is a bit outside the scope of this module so we won't be doing it. Instead we will be utilising subroutines from C in order to handle IO.
## Program Output
[[Lecture 5 - Stacks, Parameters, & Calling Conventions#Calling Conventions|Last lecture]] we looked at how we can pass parameters into subroutines, along with various calling conventions. We can pass parameters into C subroutines in exactly the same way, we just need to be sure that we follow the C calling convention, **cdecl**. You can read about this in last lectures note.

The two I/O subroutines that we will use from the standard C library are:
- `printf` - which sends a formatted output to the console.
- `scanf` - which waits for input from the console.

To output things using `prinf` we must know that:
- It takes a string variable or literal as its first parameter;
- We must pass the address of the string by **reference** in our assembly code.

So what we need to do on this module is:
- Define the string a C variable outside the assembly code block (bit of a cheat for simplicities sake);
- Then find the address of the string in our assembly code block using `lea`.

Since we are following the **cdecl** calling convention we must:
- Push the parameter to the stack;
- Clean up the stack after calling.

Strings should also be passed by reference into `printf`.

Below is a full example of how we will output a static string:
```
#include <stdio.h>
#include <stdlib.h>

int main (void) {
	char msg[] = “Hello World\n”; 
	
	_asm { 
		lea eax, msg ; Get address of string 
		push eax ; Set up parameter 
		call printf ; Call external routine 
		pop eax ; Clean up stack 
	} 
	
	return 0; 
}
```
## Corrupted Registers
Consider the following assembly code block:
```
	   mov ecx, 10 
floop: lea eax, msg 
	   push eax     ; push our parameter
	   call printf 
	   pop eax      ; clean the stack
	   loop floop
```

If you recall the `loop` instruction jumps to the **address label** provided and decreases the counter register `ecx` by 1 is the value in `ecx` is greater than 0. 

The problem is we don't know exactly what happens inside any external subroutine. They (almost certainly) will use registers meaning they will overwrite any values we have stored in them.

In this case the loop counter would be corrupted, meaning that our `loop` instruction won't function like we want it to. To get around this we need to store and reassert any values in registers which we want to keep.

We already have a convenient place to do this: **On the Stack!**.

If we edit our code to save the value of `ecx` on the stack and then retrieve it after we call `printf` and clean the stack then our code looks like this
```
	   mov ecx, 10
floop: push ecx     ; save our loop counter
	   lea eax, msg 
	   push eax     ; push our parameter
	   call printf 
	   pop eax      ; clean the stack
	   pop ecx      ; retreive our loop counter
	   loop floop
```

Now our code will work just as we expect. it doesn't matter that `printf` corrupts our register.
### Call Preserved Registers
Some registers in the CPU are automatically preserved by the C library routines during a call:
- **ESI** - Source index register (Not used in any code on this module)
- **EDI** - Destination index register (Not used in any code on this module)
- **EBX** - Base register
- **EBP** - Stack base pointer
- **ESP** - Stack pointer

We haven't look at **EBP** yet, but we will see what that does later on.

Notably, you can see that 3 of the 4 main registers we use are not preserved so we must store the values stored in `eax`, `ecx`, `edx` in order to ensure our code functions as we want.
## Outputting Values
The `printf` subroutine can take extra parameters, in addition to the string, that store values to be outputted. Each value is inserted into the string in place of a **format specifier**, and they are inserted in the order that they appear in the parameter list.

So if we want to output someone's name and age, we need the following parameters:
- A string, containing format specifiers - e.g. `"I am %s and I am %d years old\n"`
- Another string containing their name, which will be placed instead of the `%s` specifier - e.g. `"Bob"`
- A number representing their age, which will be placed instead of the `%d` specifier - e.g. `21`.

So if we pushed those example parameters onto the stack in the correct order, this would output:
```
I am Bob and I am 21 years old

```
### Format Specifiers
There are a lot of format specifiers and options, but the common ones (and the ones we'll use on this course) are:
- `%d` - display as a decimal integer
- `%d` - display as a string
- `%c` - display as a single character
- `%f` - display as a floating point number
You can look to [here](cplusplus.com/reference/cstdio/printf/) for a complete list.

It's very important that the extra parameters we pass to `printf` match the **specifiers** we use in the string. Specifically:
- The **types** must match;
- The **number of parameters** must match;
- The **order of the parameters** must match.

There are no error checks or type checks in assembly code, so it will simply crash or behave in an unexpected way if you get this wrong.
### Example
Now lets try and output an numeric value as part of a string.

First we (cheat) and declare the string and value in the C part of our code
```C
char msg[] = "The number is %d\n";
int num = 7; 
```

The string is our first parameter, any extra parameters (in this case just `num`) come after and represent the data to be formatted into the string.

We must push our parameters in **reverse** order, follow the **cdecl** calling convention, and then clean up the stack afterwards.

So our full assembly code looks like this:
```assembly
push num     ; push the value of num onto the stack
lea eax, msg ; load the address of msg into eax
push eax     ; push the address of msg into the 
call printf  ; calls our external subroutine
add esp, 8   ; clean the stack
```

Notice we can use `add esp, 8` to quickly clean the stack of multiple parameters. We are working in 32-bit so our parameters are each 4-bytes, so we add 8 bytes to the stack pointer to clear it of our two parameters.
## Program Input
To input data we use the external `scanf` subroutine from the `C` standard library.

`scanf` takes two parameters:
- A format specifier to indicate the type of the data
- The memory address where the data should be stored

Following the **cdecl** calling convention we must:
- Push parameters to the stack in reverse order
- Pass by reference
- Clean up the stack afterwards

We can use `scanf` to input strings from the user but we must be careful to reserve enough memory. We do this by:
- Using the `%s` format specifier.
- Declaring a `char` array that is big enough to store what they will enter. It is very easy to overflow doing it this way.
### Example
Say we want to input a integer value and store it in the accumulator.

First we need to declare the format specifier as a string, and declare a variable for us to store the input in.
```C
char fmt[] = "%d";
int num;
```

We must then push these parameters to the stack in **reverse** order, following the **cdecl** calling convention, and afterwards we must clean up the stack.

So our full assembly code looks like this:
```
lea eax, num ; load the address allocated to num into eax
push eax     ; push the destination for the input onto the stack
lea eax, fmt ; load the address of our format specifier into eax
push eax     ; push the address of format specifier onto the stack
call scanf   ; take our input
add esp 8    ; clean the stack
mov eax, num ; move the inputted value into eax
```
## Stacking Local Variables
In high level languages, subroutines can declare their own internal (local) variables. 

For example:
```C
int prodcedure (int n) {
	int x;
	int y;
	int z;
	...
}
```

These variables can only exist while the subroutine is running, and can't be accessed anywhere else. So it makes sense to store them on the stack.

When high level code is compiled, it generates machine code instructions to reserve enough memory the stack for each variable.
## Stack Frames
Every time a subroutine is called, a new stack frame is created on the stack. This holds the data that is needed by the subroutine:
- Parameters
- Return address
- Local variables

With nested calls, several stack frames will be present on the stack at any given time.

We know the **stack pointer (ESP)** register, which always points to the top of the stack, but we also have the **stack base pointer (EBP)** register, which always points to the start of the current stack frame.

You can also use the **EBP** to access the parameters and local variables by using an offset:
- **EBP** would be address of the first parameter that was pushed,
- **EBP-4** would be the address of the second parameter that was pushed
- etc.
### Building a Stack Frame
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

Finally the caller is responsible for cleaning any parameters from the stack (dependent on calling convention).
### Nested Stack Frames
When a subroutine calls another subroutine another stack frame is built on top of the last stack frame.

Each stack frame is made up of:
- The parameters
- The return address
- The old **EBP** address
- Local variables

The values of **ESP** and **EBP** change as the calls happen:
- **ESP** always points to the top of the stack
- **EBP** changes with each subroutine call

When subroutines are called the stack shrinks, as the stack frames are cleaned off of it.

You can see a model of how the stack frames are built below.
![[nested_stack_frames.png]]