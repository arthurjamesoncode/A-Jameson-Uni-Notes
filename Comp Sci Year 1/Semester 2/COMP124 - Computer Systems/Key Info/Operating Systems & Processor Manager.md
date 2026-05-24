---
cssclasses:
  - flashcards
---
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
## Linux Overview
### What is Linux?
Linux is an open source operating system created in 1991. You can see its architecture below:
![[linux_architecture.png]]
### What are System Calls?
System calls are an interface provided by the OS. They allow users to access I/O devices and perform certain actions which would otherwise be prevented by the protection ring.

System calls can be made by processes in user mode, but system calls themselves use kernel mode.
### What is the difference between modular and monolithic kernels?
A monolithic kernel has all drivers included when the kernel is compiled.

The disadvantages of a **monolithic kernel** are:
- The kernel image is very big on disk and in memory
- Need to recompile the kernel every time we want to add a new driver or functionality

A modular kernel only has specific drivers loaded when the system boots up

The disadvantages of a **modular kernel** are:
- Fragmentation of kernel memory as file systems and modules are loaded.
- Security and stability risk from loading bad modules
### What do WIMP and GUI stand for?
WIMP stands for:
- Windows
- Icons
- Menus
- Pointers

GUI stands for "Graphical User Interface"
## Navigating Linux & Other Commands
### What is a directory?
A directory is a location in which files or other directories are stored.
### What special directories do we use to navigate file systems?
We use 4 special directories to navigate file systems:
- `~` - Home Directory
- `.` - Current Directory
- `..` - Parent of current directory
- `/` - Root Directory
### What is the root directory?
The root directory is the top of the directory hierarchy and holds all other directories.

### What commands can we use to navigate through and manipulate directories?
We can use the commands:
- `cd` - change directory
- `pwd` - print working directory (current directory)
- `ls` - list all files and directory in current directory
- `mkdir` - create a new directory
- `rmdir` - remove an empty directory
- `rm` - remove a file
### How can we pass options to commands?
We can pass options to commands as a string of single letters following a dash.

For example:
```
ls -a
```
or
```
ls -la
```
### What do `ls -a` and `ls -l` do?
`ls -a` lists all directories in a folder including special/hidden ones.

`ls -l` uses a longer format which shows more information
### How are file permissions shown in the terminal?
In the terminal, after performing `ls -l` a string will be shown next to each file which looks something like this:
```
drwx--x--x
```
### What does each character of the permission string mean?
There are 10 characters in the permission string

The first character indicates the type of file:
- `-` for normal file
- `d` for directory
- other characters for other special files

The next 9 characters split into 3 groups (in order):
- User
- Group
- Others

Each 3 character section indicates permissions:
- The first character is either `r` (for read) or `-` 
- The second character is either `w` (for write) or `-`
- The third character is either `x` (for execute) or `-`
### How do you change permissions?
You can change permissions using the `chmod` (change mode) command.

You either use the format `chmod [ugo][+-][rwx] filename` where:
- `u`, `g`, or `o` represents who you are changing permissions for
- `+` or `-` represents whether you are adding or removing permissions
- `r`, `w`, `w` represents which permission you are changing

Or you can change the whole string at once by passing in a 3 digit octal value. Each digit represents the new permissions for one set of users (`u`, `g`, `o`). 

You can either get the correct octal value by thinking of the binary string which matches the permissions, or by using the table below.

| (add up) | Value |
| -------- | ----- |
| Read     | 4     |
| Write    | 2     |
| Execute  | 1     |
>Importantly, the filename is the second argument to the command. There was a practice question on this I got wrong.
### What is the Root User?
The root user is a special user in Linux which has full access to everything. It owns many background processes and system files. 

Human users can not login to the root user in most modern systems. Users can temporarily request root permissions using the `sudo` command.
### How do I compile and run assembly code in Linux?
You must compile a file using the command
```
nasm -f elf32 filename.asm
```

And then link it to an executable with
```
ld -m elf_1386 filename.o -o filename
```

You can then run it with 
```
./hello
```

>I doubt this will come up but it might so you should try remember these commands.
## Linux Processes
### How are new processes created?
New processes are created from other processes using the system calls:
- `exec()` - tells a process to execute another process (essentially transforms the old process)
- `fork()` - spawns a new clone of the process which runs alongside the parent
### How can we tell a parent process to wait until its child finishes?
By using the `wait()` system call.
### What does the `fork()` system call return?
It returns either:
- A negative number - error that stopped creation
- 0 - Child is created and this is running from inside the child
- A **positive number** means that the child was created and this is running from **inside the parent process**. In this case, the number returned is the ID of the child process

For example:
```C
int pid = fork(); // Call returns in each of the two processes 

if(pid == 0) { 
	printf(“I’m the child process”); 
	// Will usually call exec() to load its own code 
} else { 
	printf(“I’m the parent and my child’s ID is %d”, pid); 
}
```
### What is the first process called and what is its PID?
The first process is called `systemd`, meaning system daemon. Its PID is 1.
### How is the first process spawned?
The first process is loaded by GRUB (GNU Grand Unified Bootloader) off of disk. This is the kernel image.

GRUB is stored on the ROM of the motherboard.
### How can we connect to a remote shell?
We can connect to a remote shell using an `ssh` client.
### What happens in terms of processes when we connect to a remote shell?
An `sshd` daemon runs in the background of the shell we are connecting to. This waits for incoming connections and is spawned by `systemd`.

When we connect:
- The `sshd` daemon uses `fork()` to spawn a child process,
- The child uses `exec()` to run a login process,
- The login process checks that our credentials are correct,
- If credentials are correct it uses `exec()` to run our preferred shell process.
### What is a zombie?
A zombie is a process which has terminated but it's "death" has not been acknowledged by the parent process, meaning it is still present in the process table.
### What terminates first: Parent Process or Child Process?
Parent processes usually wait for their children to die.
- The processor manager will tell the parent that the child terminated
- A `SIGCHILD` signal is then sent to the parent
- Clean up is only done **after** the parent acknowledges it no longer needs its child
### What is an orphan?
An orphan is a process whose parent has terminated before them.
### How are zombies and orphans dealt with?
It is the job of `systemd` to periodically clean up any zombies/orphans in the process table.
### What is a daemon process?
A daemon is a background process. It is not attached to any user and it runs permanently in the background.

Daemon processes usually have a higher priority than other processes.
### How does the Linux kernel keep track of processes?
The Linux kernel stores information about processes in the `/proc` directory.

It stores:
- Details about state of the kernel
- A subdirectory for each running process

This forms the virtual file system `procfs`. These files are not all real files.
### What are Linux signals?
Linux signals are interrupts.
### How do processes send signals?
Signals can be sent between processes using the `signal()` system call.
### How can we send signals from the terminal?
We can send signals from the terminal by using the `kill` command like so
```
kill -s SIGKILL 438
```
`438` is the PID and `SIGKILL` is the signal.

`-s` lets us specify a signal. `SIGKILL` is sent by default.
### How can processes respond to signals?
Processes can respond by:
- **Performing** the action requested
- **Ignoring** the signal completely
- **Catching** the signal and running some other arbitrary code
### What signals do we need to know for this module?
| Code     | Number | Meaning                                             |
| -------- | ------ | --------------------------------------------------- |
| SIGINT   | 2      | Interrupted from keyboard (via CTRL+C)              |
| SIGKILL  | 9      | Request to terminate process (**can't be ignored**) |
| SIGTERM  | 15     | Request to terminate process (can be ignored)       |
| SIGCHILD | 17     | Indicates that a child process has terminated       |
| SIGIO    | 29     | input or output is ready                            |
### How can we terminate a zombie process?
Often processes become zombies because their parents are poorly coded.

This means that to terminate them we must send the `SIGKILL` signal to the parent and then let `systemd` adopt/clean up the zombie.
### What types of Inter-Process Communication (IPC) exist?
There are 4 types of IPC (for this course):
- Shared memory
- Shared files
- Pipes
- Sockets
### What are pipes?
Pipes a way to send the output from one process to another process in the command line.

For example:
```
cat /proc/modules | wc --lines
```
### What are sockets?
Sockets are a form of multiple system IPC between two processes, a server and a client.
- The server listens for clients with the `listen()` system call
- The client connects to the server and the server uses the `accept()` system call
- The server spawns a handler using the `fork()` and `exec()` system calls
Both sides can send and receive information.

Linux views sockets as special files meaning that data transfer can be done with the `fread` and `fwrite` system calls.