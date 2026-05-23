## Von Neumann Model
Prompting Questions: 
- What does the Von Neumann model consist of?
- What concept is it associated with?
- Has this model changed over time?
- What does the architecture of a modern system look like?
### Answers:
Von Neumann model consists of:
- Input Device ->
- CPU & Memory ->
- Output Device 

(See below)
![[von_neumann_model.png]]

It is associated with the **stored program concept**.

This model has not changed over time but the specifics (type of input device/memory etc.) have changed.

![[modern_system.png]]
## CPU Overview
Prompting Questions:
- What is the role of the CPU?
- What is an instruction?
- What is an instruction set?
- What common types of CPU instruction sets exist? 
- Where is each type of instruction set used, and how do they differ?
- How do you measure CPU speed?
- What does 1Ghz mean?
- What is the advantage of multiple CPU cores?
### Answers:
The role of the CPU is to fetch instructions from memory and execute them.

An instruction is a very basic command the CPU can perform such as:
- Add two values
- Save a value at $x$ point in memory
- etc.

An instruction set is all the instructions a CPU can perform. These differ based on make (AMD, Intel, etc.)

The two common types of instruction set are:
- Complex Instruction Set (CISC) - Desktops/Servers etc. - For example Intel x86
- Reduced Instruction Set (RISC) - Smartphones etc. - For example ARM

They differ as:
- RISC instruction sets use a small set of simple, fixed-length, fast instructions which can execute in a single clock cycle.
- CISC instruction sets use a larger set of variable length instructions which may take multiple clock cycles to execute.
- RISC code isn't slower than CISC code, but will be longer.

CPU speed is measured in hertz (Hz) by the speed of its clock:
- 1Hz = 1 cycle/second
- 1MHz = 1,000,000 cycles/second
- 1GHz = 1,000,000,000 cycles/second

Multiple CPU cores allow for some programs to execute faster provided they are written in a way to take advantage of concurrency.
## System Bus
Prompting Questions:
- What is a system bus?
- Why do we use busses?
- How does data transfer work?
- What kinds of lines does the bus have, and what are their purposes?
- What are common busses in modern systems?
- What is bus contention?
### Answers
A system bus is a collection of wires which all connected motherboard components to communicate.

Using a bus allows us to avoid directly connecting each component (a point-to-point system) which is prohibitively expensive/complicated. In a $n$ device point to point system there would need to be
$$
\frac{n(n-1)}2=O(n^2)
$$
connections.

Data transfer works by **senders** placing items (data) on the bus and **receivers** taking it off.

The bus has:
- Address lines - These specify a memory address/device to be accessed
- Data lines - Carry the data/item to be transferred
- Control lines - Carry instructions for the receiver to perform

Modern systems include busses such as:
- SATA
- PCIe
- USB

**Bus contention** is the problem of deciding what uses a bus at any given time, since only 1 thing can be on each bus at once.
## I/O Devices & Interrupts
Prompting Questions:
- How does the CPU know when a device is ready to receive/transmit?
- What is polling?
- What are the downsides of polling?
- What are interrupts?
### Answers:
The CPU knows when devices are ready by using:
- Polling (Older systems)
- Interrupts (Modern systems)

Polling is when the CPU periodically checks the status of each device by sending out a clock signal.

The disadvantages of polling are:
- Needs the CPU to stop what it's doing
- Wastes clock cycles

An interrupt is a signal sent to the CPU by a device when:
- It is ready
- It is finished with a task
They are intercepted by an interrupt handler within the OS which then decides how/when the CPU will access respond to the interrupt.
## Internal Memory
Prompting Questions:
- How are programs and data stored?
- What do we need to do before processing programs/data?
- What types of internal memory are there?
- How are they used?
- What are their properties?
### Answers
Programs/Data are **stored in binary** and must be **loaded into internal/main memory** before they can be processed.

The types of internal memory are:
- Random Access Memory (RAM)
- Read Only Memory (ROM)

RAM is:
- Read and Write
- Volatile
- For storing programs as they are running
ROM is
- Read only
- Non-volatile
- For storing static code such as boot code
## Bit Length & Word Size
Prompting Questions:
- What is the bit length of system?
- What are common bit lengths for different types of systems?
- Can modern processors run programs built for older ones?
- What does word size mean?
- How are bit length and word size related?
- How does bit length affect maximum RAM size?
- How do we index bits?
- What is the most/least significant bit?
### Answers:
The bit length of a system is how much memory can be manipulated by the CPU in one operation.

Common bit lengths are:
- 64 Bit - Most modern systems
- 32 Bit - Some modern systems and some older ones
- 16Bit/8Bit - Embedded microprocessors

Newer processors with higher bit lengths are usually built with backwards compatibility in mind. 64-Bit Processors can usually run 32-Bit programs but not vice versa.

Word size is the size of the data that can be stored in a single variable in a piece of code.

Word size cannot exceed bit length as the bit length is linked to the size of CPU registers and the width of the system bus.

In an $n$-bit system, the maximum number of addressable bytes is $2^n$. This is our maximum RAM size:
- 16-Bit System - 64KB of RAM
- 32-Bit System - 4GB of RAM
- 64-Bit System - 16EB of RAM

Within a single "word" we index bits from right to left:
- Bit 0 (right most bit) is the least significant bit
- Bit $n-1$ (left most bit) is the most significant bit
## CPU Structure
- What are the main units of the CPU?
- What do these units do?
- What is a register?
- What specific purpose registers does the CPU have?
- What do these registers do?
- What registers does the MMU contain and what do they do?
- What are the steps of the fetch execute cycle?
### Answers
The main units of the CPU are:
- Control Unit 
- The Arithmetic Logic Unit (ALU)
- The Memory Management Unit (MMU)

The **control unit** governs the activity of the CPU, and provides the ALU with operands and data.

The ALU performs arithmetic operations and bit manipulations.

The MMU is used to interface with main memory.

A register is a small data store within the CPU itself. They are much faster for the CPU to access than RAM.

Specific purpose registers include:
- Instruction pointer `IP`, this hold the address of the **next** instruction in main memory.
- Instruction register `IR`, holds the instruction currently being executed.

The MMU contains:
- Memory address register `MAR` - Stores the address of data to be accessed
- Memory buffer register `MBR` - Stores retrieved data

The steps of the fetch execute cycle are:
1. Copy the address in `IP` into `MAR`
2. Increment `IP`
3. Instruction arrives from memory into the `MBR`
4. Instruction is copied from `MBR` to `IR`
5. Instruction in `IR` is decoded
6. Any operands are fetched
7. Instruction is executed
8. Repeat
## Instructions
Prompting Questions:
- How many categories of instructions are there?
- What are the categories of instructions?
- What do you need to do to high level code to make it run on a CPU?
- What is the structure of an instruction?
- Why do some instructions have multiple opcodes?
- How long can an Intel x86 instruction be?
- How many addressing modes can an Intel x86 instruction have? 
- What are these modes?
### Answers
There are 6 broad categories of instructions:
- Transfer - Moving data around
- Arithmetic - Simple maths operations
- Logic - Bit manipulations
- Test - Comparing values/setting flags
- Control - Jumps/Subroutine calls
- Miscellaneous - Whatever doesn't fit

High level code must be translated into a series of low level instructions before the CPU can run it. The specific instructions the compiler must generate depends on the CPU's instruction set.

Instructions are split into:
- Opcodes - A number the CPU understands which represents that instruction
- Operands - Data which the instruction must act on

Instructions may have multiple opcodes to indicate how the operands are encoded, this is not the case in Intel x86 instructions.

>Note all further comments about the structure of instructions are using the Intel x86 instruction set.

An Intel x86 instruction can between 1 and 15 bytes long. The full structure is shown below:
![[x86_instruction.png]]

The mode specifies the **addressing mode** meaning it tells the CPU where to find the operands.

The 5 addressing modes are:
- Immediate - The operand value is encoded directly into the instruction
- Register - The operand value is stored in a register
- Direct - The operand value is stored at an address in main memory
- Register Indirect - The instruction specifies a register which holds a main memory address for the operand
- Implicit - The instruction does not require an operand
