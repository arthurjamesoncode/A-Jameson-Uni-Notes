## Memory Manager
The memory manager of an OS manages the main memory (RAM) of the system. It's main job is to ensure that each process gets access to the memory it needs.

It performs many tasks for the system including:
- Preserves and protects the space in memory occupied by the OS itself
- Checks validity of each request for memory space
- Allocates free areas of memory for valid requests
- Keeps track of which areas of memory are being used and by which user/process
- Deallocates memory when no longer needed
- Implements segmentation and paging models via virtual addressing
- Manages swap space according to page swapping policy

This lecture will be spent going over how memory works, and how the memory manager manages it.
## Memory Addressing
The RAM inside a system can be viewed as a linear sequence of bytes. This idea is called the **linear model** or **flat model**.

In this model, memory is byte addressable and addresses can range from 0 up to the number of bytes available.

Since memory addresses need to be stored in the registers of a CPU during process execution, the **bit length** of the CPU determines the maximum size of addressable memory:
- In a 32-bit CPU, **4,294,967,296** bytes of memory can be addressed. This caps the size of memory to 4GB of RAM.
- In a 64-bit CPU, **16 Exabytes** (16 Billion Gigabytes) of memory can be addressed. We are unlikely to ever need more than this.

Some addresses will need to be used for the **kernel image** of the OS itself, while other bits are needed for any memory mapped devices. This makes the total **available memory** for other processes less than the system memory itself.
## Process Memory
A program exists first on disk as a binary executable file. This is usually gotten by compiling some high-level code to target the specific OS and CPU architecture.

When a program is run, this binary file is loaded into main memory along with some extra space for variables and the stack, allowing room to grow. This memory footprint is the **process image**. The CPU's instruction pointer is then set to the first byte address of this image, which starts the execution of the process.

Jumps to labels are then replaced by real memory addresses. These addresses point to a physical location within the process image and can be **fixed** or **relative** addresses. When these jumps occur, the IP is to these real addresses.

Below you can see an example representation of what a **process image** is.
![[process_image.png]]

Think of the bottom of this image as it's **start**. The image contains multiple different sections:
- **Text** - This is the actual code that the process needs to execute.
- **Data** - This is the memory allocated for variables and objects declared in the high-level code.
- **Heap** - This is memory available for the programmer to reserve. It is dynamically resized and grows upwards
- **Stack** - This has been covered before [[Lecture 5 - Stacks, Parameters, & Calling Conventions#The Stack|here]], and is used for calling subroutines, holding local variables etc.

When **stack overflow** occurs it is because the heap and stack have grown to the point that they overlap.
## Address Binding
When programs are compiled into machine code, the addresses of loops, jumps, variables etc. must be bound to real physical addresses in memory.

There are two main ways to do this:
- At **compile time**
- At **load time**
- At **run time**
We will cover all of these approaches now
### Compile Time Address Binding
With compile time address binding, jumps and loop locations are turned into **fixed** memory addresses when compiled.

This approach assumes that the program will always occupy the same physical space in memory every time it is executed.

For example consider the program below:
```assembly
floop: mov eax, 2
	   mul ebx
	   jmp floop
```

The start of the program and the jump location (`floop` label) is turned into a memory address when compiled. Every time the program is loaded, it must be loaded into this start address or the jump will just not work (send the program to the wrong place).

Lets say the start is loaded into address 1000. This means the program will only work when loaded into address 1000. If we even loaded it into 1001 it would break.

This has a number of clear disadvantages:
- Can't move the program to another location in memory
- The OS can't make the most efficient use of memory
- If another program is also compiled the use the same memory address, these programs can not run at the same time.
These problems are mitigated by **load time** address binding.
### Load Time Address Binding
With load time time address binding, jumps and loop locations are turned into **relative** memory addresses when compiled.

Now, a program can be loaded at any free space in memory and it won't affect execution.

Take the example from before
```assembly
floop: mov eax, 2
	   mul ebx
	   jmp floop
```

Now the jump location (`floop` label) is encoded with a relative address such as `JUMP -8`. `-8` indicates that we want to jump 8 bytes backwards, assuming 4 bytes per instruction this means go back 2 lines. The actual address would be inserted into the code when the process is loaded into memory.

>Note that the assumed 4 bytes per instruction is an oversimplification.

This lets the memory manager load a process anywhere in the address space, and ensures that 2 programs, as long as they are loaded into different addresses, will not want to jump to the same address.
### Dynamic/Run-Time Address Binding
With run-time address binding, jumps and loop locations are turned into **relative** memory addresses when compiled.

The difference here is that each process has its own address space which starts at location 0. So if a process takes up $n$ bytes of memory when loaded, then the address space will always be the numbers from 0 to $n$ no matter where it was loaded.

Essentially, this sets up a **logical address space**, and each address in it is a **logical address**. They can also be called **virtual addresses**.

These logical addresses are mapped to the **physical** addresses by the memory management unit (MMU):
- The CPU has a **relocation register** that holds the real address of the start of the process
- The logical addresses are then mapped relative to this base value

The MMU only needs to do this address mapping when doing **dynamic/run-time** address binding since in both compile and load time address binding, the **logical and physical addresses are the same**.

Separating the logical and physical addresses has some pretty big advantages:
- The memory locations of programs can be changed **after they are loaded**.
- It is **not necessary** for all of a running program to be stored **contiguously**.

Both of these advantages allow for things such as:
- Virtual Memory (using disk as memory to store background/less important processes when too much is running at once)
- Paging and Segmentation (covered later)
- etc.

**This is the type of address binding most modern OSs use.**

