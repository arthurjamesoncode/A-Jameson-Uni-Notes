## Process Creation
Processes are created (or spawned) by other processes. We consider the original process the **parent** of the new process, and the new process the **child** of the original process.

This means that all running processes form a tree structure. You can see this tree if you look at the output from the Linux `pstree` command (Look below).

![[pstree.png]]

The `systemd` process is the first process created, as therefore forms the root of this tree.

There are a number of system calls which Linux provides that allow a process to spawn a child:
- `exec()` allows the process to **execute** another process. The child overwrites the parent in memory and the PCB.
- `fork()` spawns a new clone of the process. Both the parent and child continue to run.
- `wait()` called by parent process, and causes the parent to block until the child process terminates.

Below you can see an example of some possible process execution flows

![[process_execution_flow.png]]

### `fork()` - Return Value
The fork system call returns one of three possible values:
- A **negative number** means that the child could not be created
- **Zero** means the child was created and this is running from **inside the child process**
- A **positive number** means that the child was created and this is running from **inside the parent process**. In this case, the number returned is the ID of the child process.

It is important to note that `fork()` clones the current process, and returns in **both** the child and parent process.

A typical example of how this would be used is shown below
```
int pid = fork(); // Call returns in each of the two processes 

if(pid == 0) { 
	printf(“I’m the child process”); 
	// Will usually call exec() to load its own code 
} else { 
	printf(“I’m the parent and my child’s ID is %d”, pid); 
}
```
### The First Process
ROM stores a small program that runs a bootloader when a system is first turned on.

Linux systems use GRUB (GNU Grand Unified Bootloader) which loads the kernel image from disk and starts fetch-execute cycle from first instruction.

The first process to run is called `systemmd` and has a process id (PID) of 1. This process can be configured for various environments (server, desktop, etc) and spawns all other processes the kernel needs.

`systemd` then continues to run as a background process, also called a daemon, which:
- Offers on-demand spawning of other services
- Maintains logfiles to record system activity
- Keeps track of other processes and kernel settings
## Shell (Terminal) Login
The `sshd` daemon runs in the background, waiting for incoming connections. It is spawned by `systemmd` when the system first boots up.

We can use an `ssh` client to connect to a Linux server. When we do this:
- The `sshd` daemon uses `fork()` to spawn a child process,
- The child uses `exec()` to run a login process,
- The login process checks that our credentials are correct,
- If credentials are correct it uses `exec()` to run our preferred shell process.

Processes are being created all the time to handle whatever the system needs to do, and whatever users are trying to do. All of this is done through the `fork()` and `exec()` system calls.

We have been talking about this in terms of Linux, but this is the same concept for any other major OS.

When we run a shell command, the shell uses `fork()` to create a child process, that child then uses `exec()` to run the command we typed in.

You can see this with the `ps` command
![[ps.png]]

Notice that both processes are running at the same time:
- The parent process is the shell (bash)
- The child process is the `ps` command

A desktop GUI does the exact same thing but uses clicks to spawn processes instead of text commands.
## Zombies and Orphans
Parent processes usually wait for their children to die.
- The processor manager will tell the parent that the child terminated
- A `SIGCHILD` signal is then sent to the parent (you can read about signals later in this note)
- Clean up is only done **after** the parent acknowledges it no longer needs its child

If the death (termination) of a child process is not acknowledged by the parent process then the child becomes a **zombie**, meaning that it has finished but is still present in the process table.

If a parent terminates before it's children (e.g. an unexpected crash) then the children become **orphans** and are adopted by the `systemd` process.

It is the job of the `systemd` process to periodically clean up zombies and orphans in the process table.
## Daemon Processes
We have already mentioned some daemon processes such as `systemd` and `sshd`, but there are a ton of these.

These processes are not associated with any shell or any user, they run permanently in the background, and their names usually end with `d` to signify daemon.

These processes perform the background operations of the operating system. Each subsystem manager is a daemon process. 

These processes need time on the CPU and must be accounted for when scheduling. They usually run with a higher priority since they are more important to the running of the system.

These processes also perform tasks requested by other processes, For example, they act as servers in a client server relationship.
## Processes in the Linux File System
The kernel stores a lot of housekeeping information about the currently running processes. It stores this in the `/proc` directory. This gives:
- Dynamic details about the current state of the kernel
- Virtual file system called `procfs`, meaning that they are not all real files on disk.
- A subdirectory for each running process.

Below you can see an example of some directories and there purpose
![[proc_dir.png]]

If we use the `top` command, we can see a dynamic, real-time display of all process details.

![[top_shell.png]]
## Linux Signals
A process running in the terminal can usually be terminated by typing `^C` (CTRL + C). This works by sending an **interrupt signal** to the process. The process intercepts the signal and responds by terminating.

Signals can be sent between processes using the **signal()** system call. You can send signals with the `kill` command from a terminal shell.

For example if we wanted to terminate process 438 we could use
```
kill -s SIGKILL 438
```

>Note that kill can be used to send any signal, but by convention you should only use it to terminate a process.

The process that receives a signal can respond in one of three ways:
- **Perform** the action requested
- **Ignore** the signal completely
- **Catch** the signal and run some other arbitrary code
The only signal which can't be ignored or caught is SIGKILL (9)

You can see a few examples of common signals in the table below

| Code     | Number | Meaning                                             |
| -------- | ------ | --------------------------------------------------- |
| SIGINT   | 2      | Interrupted from keyboard (via CTRL+C)              |
| SIGKILL  | 9      | Request to terminate process (**can't be ignored**) |
| SIGTERM  | 15     | Request to terminate process (can be ignored)       |
| SIGCHILD | 17     | Indicates that a child process has terminated       |
| SIGIO    | 29     | Indicates that input or output is ready             |
### Terminating Zombie Processes
Imagine that a parent process is badly coded. This process spawns a child via `fork()` but does not acknowledge when that child terminates (via `wait()` or SIGCHILD).

We have seen that when this happens the child becomes a zombie, and hangs around in the process table doing nothing. This takes up some (minimal) system resources unnecessarily so we want some way of trying to kill it.

We could try and resend the SIGCHILD signal to the parent, but if it has been badly coded this probably won't work.

So to eliminate this process we have to send the SIGKILL signal to the parent to kill it. Once the parent is dead `systemd` will adopt the zombie and clean it up during the next periodic check.
## Inter Process Communication (IPC)
Processes very often need to communicate with each other. This can be to share send and receive data or to provide services (such as severs) to other processes (such as clients).

There are many types of IPC:
- Shared memory
- Shared files
- Pipes
- Sockets

Shared memory and shared files allow  two processes to access the same memory location or file at the same time. This introduces synchronisation issues, and so this type of IPC needs to be coordinated via **semaphores** and **locks**, which will be covered in later lectures ([[Lecture 19 - Producer-Consumer Problem & Semaphores|here]]).
### Pipes
A pipe is a form of IPC between two children of the **same** parent, and is usually triggered by typing a command in the terminal.

Two processes can be joined with the pipe symbol `|`, the output from the first process becomes input to the second process.

For example, we can both: 
- List all the kernel modules with `cat /proc/modules`
- And count the lines in a file with `wc --lines filename` (if we don't include a filename it counts lines of input)

We could use a pipe to combine these two commands and therefore get the current number of kernel modules with
```
cat /proc/modules | wc --lines
```
### Sockets
A socket is a form of OPC that can span multiple systems.
- One process is the server (a daemon) listening for clients
- One process is the client which connects to the server
- Both sides can send and receive (communication is bidirectional)
- Implemented as special files in the file system

These processes don't need to be on the same machine. This means they can have totally different parent processes (unlike pipes).

Typically these are used to provide internet services to the rest of the world.
- The server (e.g. `httpd`, `maild`, `sshd`) is running as a daemon
- Clients connect when they need to get/send data

The server process uses the `listen()` system call to wait for clients. When a client connects, the server spawns a child, which we call a **handler**, via `fork()`. The handler handles the communication and then terminates. The parent process puts the `accept()` system call in a loop to handle multiple incoming clients.

To the client process's `fread()` and `fwrite()` system calls, the socket just looks like a local file.

You can see an example diagram of this below
![[socket_example.png]]