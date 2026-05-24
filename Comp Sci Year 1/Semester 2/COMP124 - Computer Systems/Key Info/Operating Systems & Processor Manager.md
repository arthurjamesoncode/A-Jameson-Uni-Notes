## Operating Systems Overview
### What is the purpose of an OS?
Operating systems (OSs) serve two main purposes:
- Turn hardware components into a usable device;
- Make efficient use of resources
### What makes up the abstract of an operating system?
Operating systems have 5 key parts:
- User Interface or shell (can be terminal or graphical)
- Processor Manager
- Memory Manager
- Device Manager
- File Manager
### What must the four OS managers do?
Each manager must perform certain tasks relating to the things it manages:
- Continuous monitoring of resources
- Enforcement of policies (who gets resources, when, and how much)
- Allocation of resources when appropriate
- Deallocation of resources when no longer needed

Managers have different jobs, but must work in harmony with each other to complete tasks.
### What is the kernel?
The **kernel**, is the base of the OS. It: 
- Resides permanently in memory;	
- Performs low-level, frequently needed activities (such as context switching);	
- Operates in **kernel mode** also called **privileged mode**.

The four OS managers, and the shell are all processes which the kernel spawns.
### What happens when the system boots?
When the device is first turned on:
- An interrupt is sent to the CPU;
- The instruction pointer is set to the first address in **ROM** (read-only-memory)

The ROM contains a small **bootstrap** program, which:
- Performs basic system checks
- Sets up the system bus and I/O channels
- Loads the OS kernel from the disk and passes control to it by using the instruction pointer
### What are the different protection levels for an Intel x86 CPU?
There are 4 protection levels for an intel x86 CPU:
- 0 - Kernel Mode (Privileged Mode)
- 1 - Trusted Device Drivers
- 2 - Other Device Drivers
- 3 - User Mode

Higher numbers are granted less access. The kernel has access to everything.
### How are protection levels enforced?
Protection levels are enforced via a **protection ring**. This is a physical part of the CPU. Intel x86 processors have four rings. You can see below a visualisation of the 4 protection rings on an Intel x86 CPU.

![[protection_ring.png]]

The CPU flags register stores the privilege level of each process. Certain physical locations (memory/registers/devices) and instructions are protected and can only be accessed by processes with the correct privilege level.
### What happens if a process attempts to access something it can't?
If a process attempts to use something it does not have the correct privilege level for, it generates an interrupt called a **general protection fault**.
## Processor Manager Overview
### What is a process and how is it different to a program?
A program is the code that performs some task and can be either source code or object code.

A process is the activity the CPU is performing when it executes a program.

Programs are static, while processes are dynamic.
### What does the processor manager do?
The processor manager decides how to allocate the CPU to waiting processes, and what should be done with currently running processes.

Its goal is to maximise throughput, meaning maximise the amount of processes which can do what they need to do.

Generally it:
- Creates new processes, initialising their memory and stack
- Keeps track of the state of processes
- Handles termination of processes
- Handles inter-process communication
- Schedules processes
### What is multiprogramming?
Multiprogramming is an early process management system which ensured that a process was always running by:
1. Loading multiple processes into memory
2. Executing 1 process until it terminates or blocks for I/O
3. Switching to another process
4. Repeat from 2
### What are the problems with multiprogramming?
Multiprogramming leads to starvation of processes because:
- If a process takes a long time to compute no other process can run
- Processes become unresponsive as soon as they block for I/O if there is another process waiting
### What is multitasking?
Multitasking is a process management system which rapidly switches between processes to give the illusion of uninterrupted execution in parallel.

Each running process is given a fixed time-slice or quantum on the CPU. At the end of the quantum an interrupt is sent to the CPU, and the OS scheduler decides which process should run for the next time slice.

The OS scheduler requires time on the CPU itself to make the decision
### How are interrupts handled?
An interrupt request (IRQ) is a hardware signal that is sent to the CPU. It tells the CPU to stop what it is doing an load an interrupt handler. The handler will be different depending on which interrupt is sent.
### How does the CPU know where to find interrupt handlers?
The CPU has an interrupt vector, which stores the memory addresses of the handlers for each type of interrupt.

The OS fills this vector during boot up.
### What is the clock interrupt?
The clock interrupt is IRQ0. It is triggered every quantum tick, and triggers a context switch.
### What is a context switch?
A context switch is when the OS runs a scheduling algorithm and then changes process.

When this happens the current state of the CPU is saved in the process control block (PCB) which is stored in memory. The state of the registers for the new process is then restored from its PCB.

The OS stores a PCB in memory for all current processes.
### What does the PCB store?
The PCB of a process stores:
- Unique process ID
- User id of the process owner
- State
- Memory address of the process
- Accounting stats (time used, etc.)
- Resources allocated to process
- Register values from the last context switch
### What process states are there?
The states a process go through are:
- **Running** - Meaning the process is currently being executed by the CPU.
- **Ready** - Meaning the process is waiting for the CPU to become available.
- **Blocked** - Meaning that the process is waiting for I/O to complete.
- **Terminated** - The process is no longer running. It either completed or was aborted.
### What is involved with creating a process?
**Creation** of a process includes:
- Reserving memory for the process and its stack;
- Setting up the process control block;
- Initialising I/O channels;
- Placing the process into the ready state.
### What is involved with terminating a process?
- Closing any open I/O channels;
- Removing the process control block;
- Deallocating memory.
## Process Scheduling
### What are preemptive and non-preemptive scheduling algorithms?
In **non-preemptive** scheduling the process stays on the CPU until it terminates or blocks for I/O. (Multiprogramming)

In **preemptive** scheduling, processes can be interrupted and replaced with another process. (Multitasking)
### What goals could a scheduling algorithm have?
The **scheduling policy** of the OS will try to:
- **Maximise Throughput** - Complete as many processes as possible in a given period
- **Minimise Turnaround Time** - Execute entire process as quickly as possible
- **Minimise Waiting Time** - Reduce the time that processes spend in the ready state without being executed
- **Maximise CPU Efficiency** - Keep the CPU busy at all times to avoid wasting cycles
- **Minimise Latency** - Reduce time taken between user requests and their responses

Achieving these all at the same time is impossible so there are trade-offs between the different algorithms.
### What scheduling algorithms do we need for this module?
On this module we study 5 algorithms:
- First Come First Served
- Shortest Job First
- Shortest Time Remaining First
- Priority Scheduling
- Round Robin
### How to calculate average wait time?
Given a set of processes which all have an **arrival time** and a **burst time** and a scheduling algorithm, you trace the scheduling algorithm to calculate how long each process waits to be on the CPU before finding the mean.

The wait time is the same as the **time of execution** - **arrival time**.

The **burst time** is how long the process needs to execute.

Example available [[Lecture 9 - Process Scheduling & Average Wait Times#First Come First Served|here]].
### What is the "First Come First Served" algorithm and its pros/cons?
"First Come First Served" is a **non-preemptive** scheduling algorithm.

Processes are assigned to the CPU in the order they arrive, and have the CPU until they terminate.

The **advantages** of "First Come First Served" are:
- Very simple to implement;
- Scheduling overhead is minimal during a context switch;
- No **starvation** of processes, as every process will be gotten to eventually.

The **disadvantages** of "First Come First Served" are:
- Throughput can be low due to long processes staying on the CPU;
- Average wait time is not minimal and can vary substantially;
- Turnaround time and latency are hard to predict;
- Impossible to prioritise processes.
### What is the "Shortest Job First" algorithm and its pros/cons?
"Shortest Job First" is a **non-preemptive** scheduling algorithm.

Processes are assigned to the CPU in order of shortest estimated burst time, and have the CPU until they terminate.

The **advantages** of "Shortest Job First" are:
- It reduces overall average wait time
- Provably optimal in giving minimal average wait time for a fixed set of processes

The **disadvantages** of "Shortest Job First" are:
- Can lead to **process starvation** of larger processes if smaller jobs keep getting created.
- Difficult to estimate **burst time** for new processes. It usually relies on prior experience.
### Are non-preemptive process suitable for modern systems and why?
No:
- Processes will spend too long waiting
- Large process reduce overall performance
- The system and UI won't feel responsive
- Important OS processes cannot interrupt other processes
### What is the "Shortest Remaining Time First" algorithm and its pros/cons?
"Shortest Remaining Time First" is a preemptive version of the "Shortest Job First" algorithm:

Processes are allocated in the order of "closest to finishing". If a new process arrives which is shorter than the current one the current process is interrupted.

The **advantages** of "Shortest Time Remaining First" are:
- Short processes are handled very quickly
- Gives maximum throughput in most situations
- Doesn't require much overhead during the context switch

The **disadvantages** of "Shortest Time Remaining First" are:
- Starvation of longer processes is still possible is smaller process keep being created
- Introduces extra context switches
- Waiting time and latency increases for longer processes
- Still hard to estimate burst times
### What is "Priority Scheduling" and its pros/cons?
Priority scheduling is a preemptive scheduling algorithm which assigns processes based on a priority queue.

Each process is assigned a priority and the highest priority process is assigned the CPU. If a new process with a higher priority is created, the current process is interrupted.

The **advantages** of "Priority Scheduling" are:
- Smaller wait times and latency for higher priority processes
- Important processes get dealt with quickly

The **disadvantages** of "Priority Scheduling" are:
- Bigger wait times and latency for lower priority processes
- Process starvation is still possible as higher priority processes will always be run before lower priority ones.
### How can you solved the problem of starvation in "Priority scheduling"?
You can solve process starvation in "Priority Scheduling" by using process aging. This means that you increase the priority of a process the longer it remains in the ready state.

This ensures it will eventually make its way to the front of the queue.
### Where is priority scheduling most commonly used?
This scheduling algorithm is commonly used in **real-time operating systems** where the processes must meet deadlines.
### What is "Round Robin Scheduling" and its pros/cons?
"Round Robin Scheduling" is a preemptive algorithm that gives a set amount of CPU time to each process.

The ready state is treated as a circular queue:
- New processes arrive at the back of the queue
- At the end of a time slice the current process moves to the back of the queue and the next starts running
- If a process terminates it is removed from the queue and the next starts running

The **advantages** of "Round Robin" are:
- Easy to implement as a queue;
- Doesn't depend on guessing or estimating **burst times**;
- Response time based on number of processes instead of process burst times;
- No starvation as every process gets a fair turn on the CPU;
- Balanced throughput

The **disadvantages** of "Round Robin" are:
- Depends on selecting a good **quantum**;
- Extensive overhead if the quantum is too short;
### How long is a quantum?
Between 10ms and 100ms depending on the OS and process.
### How does quantum size affect the algorithm?
If the quantum is too big, "Round Robin" behaves like "First Come First Served", just with shorter processes executing a bit faster. 

If it too small it behaves like "Shortest Job First", just with longer processes executing a bit faster.
### What algorithm does Windows use?
Windows uses the "Priority Round Robin" algorithm. Which is a combination of priority scheduling and Round Robin.

Processes are given a **priority boost** when they are in the foreground (they are the currently active window). Processes can also be boosted when they receive an input or an event which they have been waiting for.

Boosted processes are reduced in priority by one level at the end of each time slice until their base level is reached.
### What process priorities does Windows use?
Priority values range from 0 to 31, and each new process is given one of five base priorities:
- **IDLE** (4)
- **BELOW_NORMAL** (6)
- **NORMAL** (8) - this is the default
- **HIGH** (13)
- **REALTIME** (24)
### What algorithm does Linux use?
Linux uses an algorithm called **Completely Fair Scheduling** (similar to Round Robin) 
- Ready processes are stored in a balanced tree (not a queue)
- Gives credit for time spent in the blocked state 
- Time quantum varies depending on processor demand 
- Process priority and nice values combine to give overall priority

>Note that 0 is lowest and 24 is highest in windows
### What process priorities does Linux use?
Linux also assigns a priority to each process
- Kernel processes have a value from 1 to 99
- User processes have a value from 100 to 139

It also assigns a ‘nice’ value to each user which ranges from −20 (highest priority) to +19 (lowest priority)
- Default is 0 for every user
- Users can change priorities with nice and renice commands

>Note that 1 is highest and 139 is lowest in Linux