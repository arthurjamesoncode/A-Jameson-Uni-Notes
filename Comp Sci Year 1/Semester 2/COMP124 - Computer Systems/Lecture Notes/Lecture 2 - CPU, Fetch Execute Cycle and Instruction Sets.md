## I/O Devices & Interrupts
Devices include expansion cards (for example, graphics, WIFI, etc.), built in I/O devices on the motherboard, and peripheral devices, (for example keyboard, mouse etc.).

When performing input/output (I/O), the CPU needs to know when a device is ready to receive or transmit, and when it has completed each request.

One option to do this is to use **polling**, which:
- Periodically checks the device status by sending out a clock signal;
- Required the CPU to stop what it's currently doing;
- Wastes CPU cycles.

Polling obviously has problems, laid out above. Instead of this, modern computers now use **interrupts**. 

When interrupts are used, each device sends a signal to the CPU when it is ready, or when it's finished with a task.

This invokes an interrupt handler within the operating system, which intercepts the interrupt and decides when the CPU will handle it.
## Internal Memory
All programs and data must be converted to binary format and loaded into internal memory before they can be processed. This is called the stored program concept.

There are multiple types of memory, which include:
- **RAM** - Random Access Memory - This is read and write, volatile (meaning it is not persistent, and will be lost when turned off or power is lost) and is the main type of memory the computer uses when performing tasks. It is called random access memory because it can be accessed from any random location, rather than needing to be accessed from the beginning.
- **ROM** - Read Only Memory - This is non-volatile, and cannot be change. It is usually burned into a chip on the motherboard. This is how the system boot code would be stored.
- The memory in HDDs and SSDs is different from the above 2 types, it is non-volatile and read and write. Programs stored in HDDs and SSDs must be loaded into ram before they are used.

The **bit length** of a system determines how much memory can be moved and manipulated by the CPU in a single operation.

Most modern systems (desktops, laptops, phones etc.) are 64 bit.

Embedded microprocessors (inside appliances) are often 8-bit or 16-bit. Nowadays, 8-bit are fairly uncommon.

You can run a 32-bit operating system on a 64-bit system. Some Windows installations use the 32 bit version even if the CPU is 64-bit.

Software compiled for a 32-bit CPU can usually run on a 64-bit CPU, but not vice versa.
### Bit Length & Word Size
The bit length of a system is related to the word size of variables in our code. "Word size" refers to the size of data that can be stored in a single variable.

This is because the width of the system bus and the size of CPU registers, both of which are directly related to the bit length of a system, limit the size of information that can be altered. This means the word size of our variables cannot exceed the bit length of our system.

The maximum unsigned integer also relates to the max random access memory size, since RAM is byte addressable. So:
- A 16-Bit system can only address $2^{16}$ bytes or 64 kilobytes
- A 32-Bit system can only address $2^{32}$ bytes or 4 gigabytes
- A 64-Bit system can only address $2^{64}$ bytes or 16 exabytes (This is likely more RAM than anyone will ever need. I believe the most RAM any single machine has has so far is 160TB, which is about 1 billion times less than 16 exabytes)

Within a single "word" bits are 0 indexed from right to left. We call bit zero (the rightmost bit) the lest significant bit, and we call the left-most bit (31 in a 32-bit system etc.) the most significant bit. 

In the same manner we can also have the least and most significant byte. In a 32-Bit system, the least significant byte would contain bits 0-7 and the most significant byte would contain bits 23-31.
## CPU Structure
Below you can see an image of the structure of the CPU.
![[inside_cpu.png]]

The **control unit** is a complex piece of logical hardware that governs the activity of the CPU. 

The **arithmetic logic unit** (ALU) performs bit manipulations and numeric operations, such as logical operations (bitwise ORs, ANDs etc.) and arithmetic operations (plus, minus, divide, etc.). The control unit supplies the ALU with operands (data) and tells it what to do. 

The CPU has internal data stores called **registers**. These are physically on the silicon of the CPU and therefore are much faster to access than RAM. They all have individual names, and can be general purpose or have a specific use. They can hold data temporarily while the ALU acts on it. On the diagram, registers are shown by the green boxes.

Specific registers include:
- **Instruction Pointer** - This always holds the address of the *next* instruction in memory. This can also be called the program counter or PC.
- **Instruction Register** - Holds the instruction currently being executed.

There are also registers contained in the **memory management unit** or MMU. These registers are used to interface with main memory, and are not directly accessible to the programmer.
- **Memory Address Register** - This stores the address of data to be accessed in main memory.
- **Memory Buffer Register** - Once data has been retrieved from main memory it is stored in the memory buffer register.
### Fetch Execute Cycle
A compiled program is just a sequence of instructions in successive memory locations. Before it is run, it will be loaded from a hard drive, such as HDD or SSD, and stored in a contiguous chunk of RAM. 

To execute the program, the instruction pointer is set to point to the memory address of the first instruction. Once this is done the full cycle can be seen below.

The cycle:
- Step 1: Copy the address in the **instruction pointer** (IP) into the memory address register. 
- Step 2: Increment IP to point to the next instruction. It does this now as accessing memory is slow compared to accessing registers.
- Step 3: Current Instruction arrives from memory into the **memory buffer register** (MBR), and the instruction is then copied to the **instruction register** (IR).
- Step 4: Decode IR to find out what the instruction is
- Step 5: Fetch any operands (extra data needed)
- Step 6: Execute the instruction (via the ALU, etc.)
- Step 7: Repeat from step 1.

Note that steps 5 and 6 may cause extra memory access but don't need to. This all depends on the specific instruction.
## Instruction Sets
The CPU instruction set provides various operations the CPU can execute. Instruction sets can be very large. IA-32/x86, the intel 32-bit instruction set, contains more than 1,500 instructions.

These instructions generally fall into 6 broad categories:
- **Transfer** - Moving data to and from memory and registers.
- **Arithmetic** - Simple maths operations such as add, subtract, multiply, divide.
- **Logic** - Bit manipulations such as AND, OR, NOT, shift, rotate
- **Test** - Comparing data values and setting status flags
- **Control** - jumps and subroutine calls
- **Miscellaneous** - Any helper operations that don't fit into another category.

Code written in high level languages, such as Java or C++, needs to be compiled into a sequence of ow level instructions that the CPU can understand.

The fetch execute cycle works it's way through that low level sequence as it executes the program.

We will write low level assembly code during this module in order to understand what is happening inside the CPU.
## Instruction Format
Each instruction has an **opcode** that the CPU understands. For example, the number 5 might mean add, and whenever the CPU sees a 5 stored in the instruction register it knows to perform an addition.

The CPU gets further data, which we call operands, directly from registers or from main memory via MMU requests. For example, the numbers which it has been instructed to add.

Many instructions have several opcodes as the operands can be encoded in different ways. For example:
- Adding the content of two registers;
- Adding a number and the content of a register;
- Adding the content of a register and a number stored in main memory;
- etc.

How the CPU should get the operands is encoded into the opcode itself. This means that the CPU can differentiate when it is asked to add 1 to number from when it is asked to add the number stored in the 1st location in memory to a number.

In this module we will use IA-32/x86, or Intel x86, which is intel's 32-bit instruction set. The 64-bit version is called Intel x64.

>Note that if you have issues with the labs, you should check that you are compiling for x86 and not x64.

A single x86 instruction can be anywhere from 1 to 15 bytes long. You can see below for the structure of an instruction.
![[x86_instruction.png]]
You may have realised that, since Intel x86 is a 32-bit system, that it can only access 4 bytes at once. What this means is that some of these longer, more complex instructions cannot be accessed all at once. 

This means that, depending on the opcode, the CPU may need to read more data from main memory in order to fully complete the instruction. The fetch execute cycle we looked at is a simplification of this in order to remove these extra steps.

For the purposes of this module, we will assume every instruction takes up 4 bytes of memory, in order to make the concepts simpler to understand and explain.

The mode part of the instruction tells the CPU where the operands are located.
- **Immediate** - The operand value is encoded directly into the instruction (for example, a number).
- **Register** - The operand value is stored in a register.
- **Direct** - The operand value is stored in main memory, so the instruction encodes it's address.
- **Register Indirect** - The instruction specifies a register which contains the address of the operand in main memory.

There is a fifth mode, called **implicit**, which is used when the instruction does not require an operand.