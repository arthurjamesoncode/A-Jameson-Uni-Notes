## Linux
Linux is an **open source** operating system. It's code is publicly available to download, and anyone can contribute changes/improvements.

Linux is usually packaged into distributions that all use the same Kernel but add other open source system software and libraries.

It was created in 1991 and is based on the "Minix" OS, which was made in 1987 based on the "Unix" OS, which was made in 1971.

>Unix is actually what MacOS is based on.

Linux itself is uncommon on desktops and laptops but makes up the vast majority of Web & Cloud Services (96% market share), and Android, which is pretty much just Linux, makes up the majority of mobiles and tablets.

If you look below, you can see a overview of Linux's system architecture
![[linux_architecture.png]]
## System Calls
User programs need to access I/O devices. Otherwise, they have no way of interacting with the user, or sending and receiving data from disk or network. However, the **protection ring** prevents direct access.

To allow users to access I/O devices, operating systems provide a collection of **system calls**. These are often implemented as interrupts. These (along with some other useful functions), form the **application programmer interface** (API) of the OS.

Library code is included or imported at the top of source code. This provides a wrapper which make system calls look like normal subroutine calls. These libraries, which operating in user mode, use system calls, which operate in kernel mode, to carry out privileged tasks.
## Kernel Modules
The kernel is privileged in any OS, meaning it can do anything without any restrictions. It can access any device memory location etc.

Device drivers also need privileged access to hardware. Because of this, Linux has trusted device drivers  built into the kernel itself.

There are two types of kernel which load drivers in different ways:
- A **monolithic kernel** has all drivers included when the kernel is compiled.
- A **modular kernel** only has specific drivers loaded when the system boots up.

The disadvantages of a **monolithic kernel** are:
- The kernel image is very big on disk and in memory
- Need to recompile the kernel every time we want to add a new driver or functionality

The disadvantages of a **modular kernel** are:
- Fragmentation of kernel memory as file systems and modules are loaded.
- Security and stability risk from loading bad modules. 

Generally a **modular kernel** offers much more flexibility and would probably be preferable for a general purpose desktop/laptop but a **monolithic** kernel offers better security and is better suited to specific important systems, for which security is important and new functionality is unlikely to be needed.
## Graphical and Terminal Shells
The original Unix/Linux shell was purely text based. You just type a command, hit enter, and then see the result as text in a single scrolling terminal.

Modern Linux distributions include various graphical shells:
- **WIMP** - Windows, icons, menu, pointer
- **GUI** - Graphical user interface
The user can install and boot into their preferred desktop shell, and this shell and window manager run as **user level** processes.

On this module, we will use a terminal shell by connecting to our remote Linux farm. Here we will navigate the Linux file system to see how files are stored and then investigate how processes are created and managed.
### School Linux Farm
There is a uni-owned Linux farm in the School of Computer Science and Informatics.