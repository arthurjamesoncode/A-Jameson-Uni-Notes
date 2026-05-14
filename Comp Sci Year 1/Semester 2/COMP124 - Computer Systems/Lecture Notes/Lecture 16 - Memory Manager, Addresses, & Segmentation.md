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
### Address Binding
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
With run-time address binding, jumps and loop locations are turned into **relative** memory addresses when compiled. This is a big difference from *load time* or *compile time* address binding.

The difference here is that each process has its own address space which starts at location 0. So if a process takes up $n$ bytes of memory when loaded, then the address space will always be the numbers from 0 to $n$ no matter where it was loaded.

Essentially, this sets up a **logical address space**, where each address in it is a **logical address**. They can also be called **virtual addresses**.

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
### Memory Allocation & Fragmentation
At first, processes are loaded into contiguous memory locations. 

Each process has:
- A **base** or **datum** - The start location of the process in memory
- A **limit** - The length of the process (in bytes)

You can see a figure depicting this below
![[simple_memory_management.png]]

When a process terminates, its memory space is deallocated and becomes free again. Now the memory manager needs to decide where to load any new processes.

![[memory_decision.png]]

This leads to **fragmentation**, meaning that there are gaps in memory between currently running processes. This can cause some pretty big problems, mainly there may not be enough contiguous space to load a new process. If a process cannot be loaded into memory, it will starve (never be provided the resources to execute).

The memory manager is responsible for choosing the free space each process should inhabit. The method it uses to do this has consequences for how fragmented the memory will become.

The main methods are:
- **First fit** - choose the first free space that is big enough
- **Best fit** - choose the smallest free space that is big enough
- **Worst fit** - choose the largest free space if big enough

**First fit** leads to very severe fragmentation. If the amount of memory currently allocated is $n$, then the amount of unusable memory (due to fragmentation) will be approximately $\frac n2$.

This is known as the 50% rule.

>The 50% rule, as described in this lecture, is a simplification of a proof found in [this paper](https://seriouscomputerist.atariverse.com/media/pdf/book/Art%20of%20Computer%20Programming%20-%20Volume%201%20(Fundamental%20Algorithms).pdf) which states that if $n$ is the average number of occupied blocks in a system which has reached equilibrium then the average number of unoccupied blocks will **tend towards** $\frac n2$ in a system which uses the first fit policy. 
>
>Equilibrium simply means that running processes are terminating at the same rate that new processes are being allocated.

**Best fit** does a really good job of minimising the total amount of wasted space. It has a slight downside of leaving a lot of small gaps which are too small to hold any process.

**Worst fit** is a bit of a niche policy. It aims to ensure that the leftover pieces are as large as possible, and therefore that the most processes will be able to fit into them. It can be useful for minimising fragmentation but tends to perform worse than best fit.

>Ironically, **first fit** is the most used of all of these policies since searching through all of the free blocks is an expensive operation and is necessary for either **best-fit** or **worst-fit**. 
>
>There are also more complicated allocation policies which you don't need to know about for this module. You can read about a couple of them [here](https://www.memorymanagement.org/mmref/alloc.html).

The memory manager can move processes around to defragment space and make more room, but this **ONLY** works if the processes are compiled to use **dynamic binding**. When moving processes the MMU must:
- Update the relocation register so logical addresses map correctly
- Pause the execution of the processes while the move takes place
This all requires some CPU time to carry out the moves.

The contiguous linear memory model imposes limitations on program structure:
- Processes cannot share subroutines with each other
- Memory allocation doesn't map onto high level program structures
### Swapping
Any system will eventually run out of memory, and therefore not be able to run every process. It is possible to execute more processes than fit in physical memory by utilising **swapping**.

Essentially, the processor manager/scheduler works with the memory manager to swap processes in and out of main memory:
- Process images can be stored on disk when not being executed
- This means a process (for example one in a blocked state) can be swapped out to the disk make more room in main memory to swap in (load) a different process
This adds to the complexity and amount of time needed for a context switch.

To use swapping the OS reserves part of a disk (possibly an entire disk partition) as a **swap space**.

**Swapping** increases the system's stability since it means a new process can always be started.

Accessing the disk is much slower than accessing RAM, which means that a system with a lot of processes in **swap space** will run more slowly. This can also cause **thrashing** in HDD drives and the read/write head will be moving backwards and forwards swapping processes in and out.
## Using Library Routines
Programs often make use of third-party library routines (via `import`, `include`, etc.). The code for these subroutines is stored in library images and these need to be **linked to** by the program.

Programs can either use **static linking** or **dynamic linking**.

With **static linking** copies of the library code are added to the final program image. This can cause a lot of wasted memory/disk space and cause program files to become huge if they use a lot of libraries.

With **dynamic linking** a small stub is included in the final program image which tells the memory manager where to find the library code. If not already in memory, then it will be loaded into memory.

**Dynamic linking** library code to be shared between processes, and helps keep the disk image small while using less main memory. It does require the operating system to support it. Windows supports it through `.DLL` files.

There is an alternative to dynamic linking called **dynamic loading**, although both techniques can be used at the same time. This is because:
- Dynamic linking is controlled by the OS's memory manager
- Dynamic loading is controlled by the programmer

The programmer can make it so:
- The program can start to execute without all the required libraries being in memory at the start;
- Each required library is attached to the process image when needed while the process is running;
- The required subroutines can be called;
- The library can then be detached to free up space in memory
This means the library is only in memory for the time needed to execute its subroutines.

For dynamic loading to be possible it must be supported by all of:
- The library
- The programming language
- The operating system
## Segmentation
Segmentation (not to be confused with **fragmentation**) allows for individual parts of a process to occupy different memory locations. This removes the constraint that processes must be loaded into contiguous addresses.

When using segmentation, each process has a segment table which is also stored in memory. The address of the segment table is stored in the **segment table base register** in the CPU. The table consists of the index of each segment followed by its **limit** (length) and **datum** (start position).

Below you can see a figure which shows how the segments are broken up and a corresponding segment table. Below that you can see another figure which shows how these segments could fit into main memory.

![[segment_table.png]]
![[segmented_memory.png]]

Segmentation has some significant advantages.

Firstly, the memory allocation reflects the high-level program structure meaning there could be a segment for each subroutine, data structure, stack etc. The compiler generates the separate segments within the program image.

Next, memory protection is enhanced in a few ways:
- Array bounds checking can be performed easily
- Code segments can be protected from being overwritten by data segments
- Data segments can be protected from being executed

Previously you could accidentally overwrite instructions with new data, or try to *run* data but with signposted segments that is no longer true. The CPU can perform these checks whenever memory is accessed.

Thirdly, segments can be swapped out to disk when they are not needed. This means that a large program's running process can take up significantly less memory it's corresponding program image.

Finally, segmenting programs allows for certain segments to be reused by multiple processes. 

Imagine two processes run the same program but with different data, or maybe the same text editor is used to open two different documents. If the programs are segmented then both of these processes can refer to the same code segment without having to reload the same code. 

You can see a figure of this below:
![[segment_sharing.png]]

There are 6 registers included in the intel CPU that point to segments used by the current process:
- `CS` - Code segment register
- `DS` - Data segment register
- `SS` - Stack segment register
- `ES` - Extra segment register (often used for string programming, but use is defined by programmer)
- `FS` - additional register (use is defined by programmer)
- `GS` - additional register (use is defined by programmer)

Segmentation is no longer widely used in most modern operating systems, but 64-bit CPUs still have these registers for backwards compatibility. Segmentation has largely been replace by the **paging memory model** ([[Lecture 17 - Paging, Working Sets, & Caches|next lecture]]).

The `FS` and `GS` registers are still used by Windows and Linux. This is mainly related to support for multi-threaded processes.