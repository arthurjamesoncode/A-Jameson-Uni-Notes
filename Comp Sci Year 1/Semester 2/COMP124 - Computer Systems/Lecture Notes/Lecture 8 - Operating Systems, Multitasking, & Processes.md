## Operating Systems
Operating systems (OS) serve two main purposes:
- Turn hardware components into a usable device;
- Make efficient use of resources

The common general purpose operating systems you may know are:
- Windows
- Unix
- Linux
- MacOS
- iOS
- Android

The last 4 of that list are all based on, or at least heavily influenced by, Unix.

There are also embedded operating systems inside home appliances, tv boxes, game consoles, etc.

You can see the abstract view of an OS below:
![[abstract_os_view.png]]
## OS Managers
The blue nodes of that diagram show us the four essential managers of every operating system:
- **Processor Manger**
- **File Manager**
- **Device Manager**
- **Memory Manager**

Each manager must perform certain tasks:
- Continuous monitoring of resources
- Enforcement of policies (who gets resources, when, and how much)
- Allocation of resources when appropriate
- Deallocation of resources when no longer needed

Managers have different jobs, but must work in harmony with each other to complete tasks.
## Processes vs Programs
What's the difference between processes and programs?

A **program** is a the code that performs some task. It could be:
- Source code (Java, C++, etc.)
- Object code (compiled executable) stored on a disk somewhere

A program is static, meaning it doesn't change, after compilation.

A **process** is the activity that the CPU performs when it executes a program.
The code is loaded from disk into memory, the instruction pointer starts at the first instruction in memory.

A process is dynamic, execution branches depending on input.

There isn't exactly a 1-1 correspondence between programs and processes, but you can (somewhat simplistically) think of processes as programs while they are running.
## OS Structure
The operating system consists of various key parts. I am going to go over them briefly here, and mention a lot of things we are yet to come to. These, unless specified otherwise, will be covered slightly further down in the lecture note.

The key parts of an OS include:
- A central **kernel**, which: 
	- Resides permanently in memory;
	- Performs low-level, frequently needed activities (such as context switching);
	- Operates in **kernel mode** also called **privileged mode**.
- A **shell**, which:
	- Provides the user interface for the operating system;
	- Allows the user to run and interact with programs (processes);
	- Operates in **user mode**, which has no special privileges and offers restricted access.
- A set of **processes**, which:
	- May be created by the **kernel** to carry out its activities;
	- May be executed when the user runs software;
	- Can be privileged or non-privileged depending on how they were started.
## System Boot (Initialisation)
When the device is first turned on:
- An interrupt is sent to the CPU;
- The instruction pointer is set to the first address in **ROM** (read-only-memory)
- Fetch-execute cycle begins from this address

The ROM contains a small **bootstrap** program, which:
- Performs basic system checks
- Sets up the system bus and I/O channels
- Loads the OS kernel from the disk and passes control to it by using the instruction pointer

The kernel then performs further setup and system checks. It starts various processes to perform background tasks of the OS and also starts the main shell process, which allows the user to trigger further processes.
## Command Interpreter (Shell)
The shell itself is just a series of processes that are spawn by the kernel. 

It's main function is to allow the user to interact with the operating system. Users can run more processes by typing a command or clicking an app icon. Any processes started by the shell run in **user mode**, meaning they have restricted access compared to processes started by the **kernel**.

In the early days of computers, they were big (the size of your room) and expensive. A university or other organisation would usually only have 1 (if they had one at all) and users would connect to this central mainframe via text based terminals. A lot of ASCII notation dates back to this era.

Nowadays, Linux, MacOS, and Windows all provide both a text based terminal (think command prompt) and a graphical shell (desktop).
## Protection Levels
There has been some mention above about **user mode** and **kernel mode**. What does this mean?

The OS has various different protection levels for processes. 

The **kernel** has access to everything:
- All parts of the CPU
- All hardware components
- All I/O devices
It's incredibly important to protect these things against unauthorised access by users (hackers, malware, etc.) and so we have a separate **kernel** mode.

Kernel mode is enforced via a **protection ring**. This is a physical part of the CPU. Intel x86 processors have four rings. You can see below a visualisation of the 4 protection rings on an Intel x86 CPU.
![[protection_ring.png]]

The CPU flags register stores the **privilege level** of each process. Certain registers, instructions and memory addresses are protected, meaning they can only be used by processes with the correct **privilege** level.

If a process attempts to use something it does not have the correct privilege level for, it generates an interrupt called a **general protection fault**.
## Processor Manager
The processor manager decides how to allocate the CPU to waiting processes. It's driven by a desire to do something useful when a process can't continue in an attempt to maximise throughput.

The processor manager performs various tasks for the OS, including:
- Creates processes when a program is executed;
- Initialises memory and stack for new processes;
- Keeps track of the status of processes;
- Assigns processes to the CPU when available, called a **context switch**;
- Changes the state of processes as events occur;
- Handles termination of processes on completion or abortion;
- Handles inter-process communication;
- Manages process queues and prioritisation, called **scheduling**.
### Multiprogramming
Early operating systems used a process management system called **multiprogramming**.

This involves:
- Loading several processes into memory simultaneously
- Executing 1 program at a time
- Switching to execute another whenever the current process cannot continue (e.g. waiting for I/O)

This allows I/O and computation to overlap, and ensures that some process is always running avoiding wasted CPU clock cycles.

You can see below a visualisation of how this works
![[multiprogramming.png]]

In practice, this process management system doesn't work very well. This is because of **compute-bound** and **I/O-bound** processes.
- **Compute-bound** means that, if a process takes a lot of time to compute something, the CPU cannot do anything else.
- **I/O-bound** is (kind of) the opposite of compute bound. It means that if a process has a lot of I/O it will be changed away from often which can cause problems for some processes. Lot's of I/O-bound processes can mean that the CPU is often waiting for anything it can run at all.
### Multitasking
A better, modern way of process management is **multitasking**.

Multitasking aims to provide fairer access to the CPU by rapidly switching between processing to give the illusion of uninterrupted execution in parallel.

Each running process is given a fixed time slice (called a **quantum**) on the CPU. This means that the OS itself needs time on the CPU to perform **scheduling** tasks (deciding which processes should run).

You can see a visualisation of this system below:
![[mutitasking.png]]
### Interrupt Handling
Multitasking depends on the ability to interrupt the CPU at regular intervals. To do this the OS uses **interrupts**.

An **interrupt request (IRQ)** is a hardware signal. 
- This usually occurs because something happened outside normal program execution. 
- They can happen at any time, regardless of what the CPU is doing. 
- They tell the CPU to stop the current process execution and load an **interrupt handler**.

The CPU has an **interrupt vector**, which stores the memory address of the handlers for each different type of interrupt and s populated by the OS when it boots up. This makes the OS responsible for handling and managing each interrupt.

Interrupt handlers are also known as **interrupt service routines (ISR)**.

You can view interrupt vector easily in Windows or Linux. IRQ0 is the clock interrupt, triggered every quantum tick.
### Context Switch
The clock interrupt is triggered at the end of each time slice (quantum). When this happens the operating system runs a **scheduling algorithm** to choose the next process. We call this a context switch.

During a context switch, the current state of the CPU (the values stored in its registers) is saved in a special data structure called the **process control block (PCB).** The OS stores a PCB in memory for each process. When a process is placed onto CPU, the state of its registers is restored from its PCB.

The context switch needs some time on the CPU. This wastes a few CPU cycles to perform the switch, but avoids the problems associated with **multiprogramming**.
### Process Control Block & Process States
The kernel maintains a PCB for every process. This is usually stored in memory, but can also be represented as a file (for more info on this look to [[Lecture 11 - Linux Overview, Command Shell, & NASM]] and it's successor lectures).

It contains information like:
- Unique process ID
- User ID of the process owner
- Process state
- Memory address of the process
- Accounting stats (time used, etc.)
- Resources allocated to process (open file, network connections, devices, etc.)
- Register values from the context switch, allowing the state of the CPU to be restored.

Processes go through many possible states during their lifetimes. The operating and system keeps track of these, and updates the PCBs accordingly.

The states a process go through are:
- **Running** - Meaning the process is currently being executed by the CPU.
- **Ready** - Meaning the process is waiting for the CPU to become available.
- **Blocked** - Meaning that the process is waiting for I/O to complete.

There can be many processes in both the ready and blocked states. Blocked processes are unavailable for dispatch to the CPU. Ready processes are selected for despatch according to some kind of scheduling algorithm.

The **process manager** is responsible for creating and terminating processes.

**Creation** of a process includes:
- Reserving memory for the process and its stack;
- Setting up the process control block;
- Initialising I/O channels;
- Placing the process into the ready state.

**Termination** of a process includes:
- Closing any open I/O channels;
- Removing the process control block;
- Deallocating memory.

You can see a visualisation of how processes states can change below:
![[process_state_changes.png]]