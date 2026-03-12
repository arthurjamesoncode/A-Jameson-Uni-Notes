## Loops
We can loop over instructions by jumping backwards in the code. A jump instruction moves the instruction pointer back to an earlier point.

It's important to not end up in an infinite loop, so we need to ensure our loops have terminating conditions like they would in high level code. We use conditional jumps to write loops that:
- Iterate **while** a certain condition is true
- Iterate **until** a certain condition is true
## While-Do Loop
Lets look at an example while loop to generate all the Fibonacci numbers until the numbers reach or exceed 1000 in a high level language.
```
//assume all variables are defined
while (fib2 < 1000) {
	fib0 = fib1;
	fib1 = fib2;
	fib 2 = fib1 + fib0;
}
```

So we can see here that the smaller number is stored in `fib0`, a temporary store. Then we set the value of `fib1`, which held the smaller number, to the value of `fib2`, the larger number.

We then get our new larger number by summing `fib1` and `fib0`. 

To do this is assembly, we need to continuously check whether the value of `fib2` is greater than 1000, and if true, we jump after the code which generates a new value for `fib2`. At the end of our code to generate new values for `fib1` and `fib2`, we must jump back to where we test this condition.

So our assembly code would look like this
```
begin: mov eax, fib2
	   cmp eax, 1000
	   jge endwh
	   mov eax, fib1
	   mov fib0, eax
	   mov eax, fib2
	   mov fib1, eax
	   add eax, fib0
	   mov fib2, eax
	   jmp begin
endwh: nop
```

>`nop` simply means "no operation". It tells the CPU to do nothing for a clock cycle.
### Do-While Loop
A do-while loop always runs for at least a single iteration and then tests at the end of the loop.

In a high level language it could look like
```
do {
	fib0 = fib1;
	fib1 = fib2;
	fib 2 = fib1 + fib0;
} while (fib2 < 1000);
```

This can be more efficient that a while loop when working with assembly code as we can remove the second jump command.

```
begin: mov eax, fib1
	   mov fib0, eax
	   mov eax, fib2
	   mov fib1, eax
	   add eax, fib0
	   mov fib2, eax
	   cmp eax, 1000	   
	   jl begin
endwh: nop
```

You can see how this code is shorter than the code before. In assembly, shorter code always means less instructions and so this makes the code more efficient.

It's worth noting that in this program the `endwh` address label is not used. It is simply there to show the end.
### For Loop
We can use a for loop when we know in advance how many iterations we need.

For example, consider a program to sum all the integers from 1 to 10 inclusive.

In a high level language this will look like:
```
int sum = 0;
for (int i = 1; i <= 10; i++) {
	sum = sum + i
}
```

One way to implement this is like so:
```
	   mov ecx, 1   ; use count register to count iterations 
floop: add sum, ecx ; update sum 
	   inc ecx      ; increase loop counter 
	   cmp ecx, 10  ; have we reached the end? 
	   jle floop    ; if not, go round again
```

Here we use the count register to to store the loop counter, increase our sum, increment our loop counter and then compare our loop counter with the total number of loops we want to do. If we still haven't completed enough loops we jump back to the `floop` address. Which is short for `for-loop`.

There is actually a more efficient way to do this, by using the `jnz` command. This jumps if the last operation resulted in a 0. Since summing from 1 to 10 is the same as summing from 10 to 1 we can use this to forgo the `cmp` command and therefore increase efficiency.

So our code now looks like:
```
	   mov ecx, 10  ; use count register to count iterations 
floop: add sum, ecx ; update sum 
	   dec ecx      ; decrease loop counter  
	   jnz floop    ; if the loop counter is not 0, go round again
```

There is a way to make this even more efficient by using the `loop` instruction. `loop` functions exactly like a `jnz`, but in addition to this it also decrements the value in `ecx` by 1. Again this allows us to forgo another command and increase efficiency.

So our final code looks like this:
```
	   mov ecx, 10  ; use count register to count iterations 
floop: add sum, ecx ; update sum  
	   loop floop   ; if the loop counter is not 0, decrease it and go round again
```

There is a often a trade-off between readability and efficiency, which is why we prefer to write code in the more readable high level languages. Good, modern, compilers will usually generate optimised low level code for us.
## Labels and Memory Addresses
Remember that our labels just point to memory addresses. In our C++ code, we declare a variable name and optionally give it a value
```
int age = 21
```
and in our assembly code we can use the label to refer to the variable in memory
```
mov eax, age
```

Sometimes we want to get the memory address of the variable, not its value. To do this we can use the `lea` command which stands for "load effective address". So to load the address of age into our base register we can do
```
lea ebx, age
```

If we then wanted to get the value stored at the address that we have saved we can use **register indirect** mode to get the values stored in that location. We do this by placing the name of the register in square brackets. So
```
mov eax, [ebx]
```
places the value stored in the address of `ebx` into the accumulator. In this case, the accumulator would be storing 21.
## Arrays
Arrays are just items stored in consecutive memory locations. The amount of memory depends on the data being stored in the array. In a 32-bit system, each integer takes up four bytes of memory. So
```
int grades[4] = { 64, 78, 60, 55 }
```
Would take up 32 bytes. If the array was stored at address 3 in memory, the first item would be stored at 3, the second at 7, and so on.

In assembly, we use this to access the values of the array. First we load the address of the array, and then to access subsequent items we increment the address by 4.

We can use this all to write a loop which can sum the values of the array.

```
	   lea ebx, grades ; load the address of the grades array into the ebx
	   mov ecx, 4      ; set the counter registers value to 4 (length of array)
	   mov eax, 0      ; initialise our sum to 0 in the accumulator
floop: add eax, [ebx]  ; add the value of an item in the array to our accumulator
	   add ebx, 4      ; move to the next element of the array
	   loop floop      ; loops 
```

After this loop, the sum of all the elements is stored in `eax`.
## Subroutines
High level languages provide a way to call certain lines of code with parameters. This saves effort in programming, reduces the size of programs, and in general allows us to make modular code which is easier to maintain and add to.

These can be called procedures, methods, subroutines, or functions. Depending on which language and or text book you are using.

We can define subroutines in assembly code, but this has a couple challenges:
- Parameter passing is difficult.
- If a subroutine call changes the instruction pointer how do we get back to where we were before the call?
We will look at these challenges in more detail next lecture.

There is no special syntax or meaning around subroutines in assembly code. 
- There isn't a fancy way to specify parameters and their types.
- There are no local registers.

Subroutines are simply sequences of instructions like the rest of assembly code. We use the `call` instruction will the label of the first instruction of the subroutine to jump to it, and then we use the `ret` instruction to return from the subroutine.

A subroutine that doesn't end with a `ret` instruction isn't really a subroutine. It will just continue on to the next instruction.

**The following is speculation on the questions asked at the end of the lecture and may be removed or repackaged. Even if I forget to change it, it may be inaccurate**

My assumption is that there is a register that stores the address after the function call, and that `ret` simply jumps to that address whatever it may be.

The lack of local registers causes a problem. Since we only have 4 general purpose ones to use, when we call a subroutine we have to be sure it will not overwrite any values that we need. A workaround for this could be to store the values we need in memory, and then retrieve it after running the subroutine.

There also isn't really a concept of "return values" as it just jumps back to the where it was before, but if a subroutine computes a value and always leaves it in the same register we can use that value after calling the subroutine.
