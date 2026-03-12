## Recursion
Recursion is when a subroutine calls itself to perform some task. This can make code very compact, but can be difficult to understand.

>Recursion is something that has been covered extensively in COMP105, and thinking recursively is a skill that needs to be built up. 
>
>You can look to [[Lecture 7 - Recursion]] and it's successors from COMP105 for more info, but I don't think that will be very useful considering that COMP105 uses Haskell and not assembly.

Some code may have **mutual recursion** where multiple subroutines call each other recursively. One powerful use for something like this is a state machine.

Recursive subroutines usually do most of their work as they return up through the tree of nested calls.

There are two parts of a recursive subroutine:
- The general case, this is where the function calls itself
- The terminating case, this is the part that causes it to stop. They're may be more than 1 condition as part of this case.
### Fibonacci Sequence
We can consider the Fibonacci sequence in terms of recursion.

The general case is
```
fib(n) = fib(n-1) + fib(n-2)
```

And the terminating case is when n is 1 or 2.
```
fib(1) = 1
fib(2) = 1
```

>This is actually an inefficient way to implement the Fibonacci sequence as it repeats a lot of computation. `fib(n-3)` is usually needed to compute both `fib(n-1)` and `fib(n-2)` and so defining it this way causes the computer to do more work than necessary.
>
>The solution to this inefficiency is to save the numbers as you generate them, so you don't need to re-generate numbers after computing them once.

You can see below the sort of tree that would form as a result of using a Fibonacci function defined as shown above
![[fib_tree.png]]
### Factorial 
Another function which is often defined recursively is  **$n$ factorial**, or the product of all natural numbers up to $n$.

If we consider this in terms of recursion we can see the general case is
```
factorial(n) = n * factorial(n-1)
```
and the terminating case is
```
factorial(0) = 1
```

>`factorial(0)` being 1 is a matter of definition in maths. Using this as a base case allows our subroutine to take 0 as a parameter without causing errors.

Let's look at how we could program a factorial subroutine in assembly code.

```Assembly
; SUB factorial
factorial:
	cmp eax, 1
	jl termcase
	push eax
	dec eax
	call factorial
	pop ebx
	mul ebx
	ret
termcase:
	mov eax 1
	ret
```

We see that our subroutine uses `eax` to pass the parameter. Let's say that `eax` was initially passed the positive numeric value `n`.

At the start of our code, if `eax` has a value of less than 1, we jump to the terminating case, where we place 1 into `eax` and then return to where we have been called from.

If `eax` has a value of 1 or more it pushes the value of `eax` (`n`) onto the stack, decrements `eax`, and then calls `factorial`. This will continue to loop until the subroutine reaches the base case (`eax` holding a value less than 1).

After the `factorial` subroutine returns, we know that the value stored in `eax` is `n-1` factorial. So now, we just `pop` the value we stored (`n`) into `ebx` and then multiply the value stored in our accumulator by this value before returning.
## Iteration VS Recursion
Any algorithm that can be written recursively can also be written **iteratively**. 

Iterative algorithms are the regular, non-recursive algorithms that rely on loops.

The iterative version of these algorithms can sometimes be a lot simpler, usually when the recursive version can be implemented via **tail recursion**.

>For info on tail recursion, look to [[Lecture 25 - Tail Recursion]] from the COMP105 module.

It is often easier to conceptualise, understand, and solve a problem with recursive algorithms.

Recursion implicitly uses the stack as a data structure to simplify the algorithm. Nested calls create nested stack frames which take up memory. For this reason, recursion can often be wasteful for many algorithms.
## Palindrome Checker
Lets design and implement an assembly code algorithm in order to check if a given string is a **palindrome**.

A palindrome is word (or string) that is equal to it's reversal.

If we think of this in terms of recursion the general case is that the letters at each end of the string are equal, and the letters between are also a palindrome.

The terminating cases are:
- If the first and last letters of the string don't match (false)
- If a string only has letter (true)
- If a string is empty (true)

>Notice that checking whether our first and last characters match happens are part of the general case.

So how can we design this algorithm to work in assembly language?

Well first we need to decide how we will indicate the result. 

Usually, in high level code, we would use a **Boolean.** We don't have Boolean values in assembly code, but we can represent bools as either 1 or 0. So we can use 1 to indicate that that our string is a palindrome and 0 to indicate that it isn't. We can just store this value in `eax` when our subroutine terminates.

First we need to store the memory address of the string we are checking, and we also need to store it's length. We need to use registers for this, so let's use `eax` for the address and `ebx` for the length of the string.

We know we will need to access the memory addresses of the characters at the start and the end of the string. Since we know where it starts and where it ends, we can just do some maths to figure out these addresses.

We can already see how we can implement 2 of our terminating cases here:
- If the length is 0, then we can store 1 in `eax` and return (empty string)
- If the length is 1, then we can store 1 in `eax` and return (string with 1 letter)

If neither of these cases are true, then we know that we are going to need to compare the values of those addresses and then jump depending on the result:
- If they **don't match** store 0 in `eax` and return (terminating case)
- If they **do match** we need to set up a **recursive call** to check if the characters in the middle are a palindrome. This will give us a value of 1 or 0 which we can then return.

How can we set up a recursive call?
- Increment `eax` by 1, so that it points at the next character along
- Decrement `ebx` by 2, as we disregard the first and last characters meaning our length decreases by 2
- Make the recursive call (this will store it's result in the accumulator)
- Return
### String Handling in Assembly
We now know the logic behind how we are going to implement this algorithm, but in order to do that we need to know how we can view and manipulate strings in assembly code.

The first thing we need to know is that each character takes up exactly 1 byte of memory which stores its **ASCII** value. 

>For this module we will only consider ASCII codes, which are 1 byte each. Modern programs use **UNICODE** which takes up 1-4 bytes, allowing for far more characters. This is worth knowing but you don't need to worry about it for the purposes of this module. 
>
>For more information on **ASCII** look [here](https://en.wikipedia.org/wiki/ASCII), and for information on **UNICODE** look [here](https://en.wikipedia.org/wiki/Unicode).

The last byte of a string is used to store the **string terminator** (NUL). This tells the CPU that the string has ended.

Each register in a 32-bit system (which is what we work with on this module) stores exactly 4 bytes of memory.

This means that if tried to move the value of the first character of a string into a register using the address that that string starts at, we would actually move the first 4 characters of the string into the register.

For example take this string declared in C:
```C
char msg[] = "Hello";
```
This string is actually stored something like this in memory
![[hello_bytes.png]]
Where each number is the corresponding **ASCII** value to the letters in "Hello".

If we tried to store the first character of this string in our data register like so
```Assembly
lea eax, msg
mov edx, [eax]
```
What we actually moved into `edx` is this
![[wrong_first_char.png]]
All we want to store in `edx` is the number 72, but because we stored the first 4 bytes of the string we actually stored 1214606444 which is obviously a much bigger (wrong) value.

To get the first **single** byte of the string we actually need to use the following instruction
```Assembly
lea eax, msg
movzx edx, byte ptr [eax]
```
`movzx` stands for "move zero extend" and essentially means to pad the rest of the register with 0s. The `byte ptr` instructions tell the `movzx` instruction that the address passed to it is actually a pointer to a single byte in memory. 

You don't need to understand this instruction in detail, but you need to know that it allows you to choose a single character of a string.

Using this command we now get the result below
![[right_first_char.png]]
### Palindrome Checker Assembly Code
Now that we've laid out the algorithm and talked about how we can access specific characters of a string we can actually write our code.

Remember that our code relies on `ebx` being given the length of the string and `eax` being given the memory address of our string before `palindrome` was called.
```Assembly
; SUB palindrome
palindrome:
	cmp ebx, 1                ; compare the length of the string with 1 
	jle success               ; if the string has a length < 1 then jump to success
	dec ebx                   ; decrease ebx by 1 
	movzx ecx, byte ptr [eax] ; move the first char into ecx
	add eax, ebx              ; add ebx to eax to get the last char address
	movzx edx, byte ptr [eax] ; move the last char into edx 
	cmp ecx, edx              ; compare first and last char
	jne failure               ; jump to failure if not equal
	dec ebx                   ; decrease ebx by 1 again
	sub eax, ebx              ; sub ebx from eax to get address of next first char
	call palindrome           ; recursive call acting on smaller substring
	ret                       ; return found value
success:
	mov eax, 1                ; place the value 1 in eax to indicate success
	ret
failure:
	mov eax, 0                ; place the value 0 in eax to indicate failure
	ret
; END palindrome
```
### Length of String using `strlen`
`strlen` is a C library function which returns the length of a string.

To use `strlen` in our assembly code we need to add this line at the top of our file:
```C
#include <string.h>
```

Then we call the subroutine using the **cdecl** calling convention:
- Push the address of string to the stack
- Call the `strlen` subroutine (result will be in the accumulator)
- Clean up the stack

Most C library subroutines can be called like this provided they are included. 

When debugging assembly code in Visual Studio debugger, make sure you don't **step into** them with **F11**. Instead, you should step over them with **F10**. No first year comp sci student at UOL needs to be debugging C library functions written in 1989.


