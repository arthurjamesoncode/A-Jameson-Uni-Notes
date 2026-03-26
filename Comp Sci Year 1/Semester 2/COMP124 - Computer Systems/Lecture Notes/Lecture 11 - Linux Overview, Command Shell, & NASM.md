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
There is a uni-owned Linux farm in the School of Computer Science and Informatics. It has sixteen servers called `lxfarm01`, `lxfarm02`, and so on until `lxfarm16`. 

You can connect to it with via `lxfarmXX.csc.liv.ac.uk`. Your MWS login details should already work. You do need to be on campus or using the VPN service, and you might be asked to confirm a duo 2FA request.

When logged in you will see the command line prompt, you can type commands and send them with enter. You can type `logout` or `exit` to close your connection to the server.
### Directories/Folders
In GUI desktop environments, we use the word **folder** to refer to the locations that we can store files, or even other folders.

In command line environments, it's common to call them directories. These two words are virtually interchangeable when it comes to file management systems.

There are a number of special directories we can use when navigating a file system from the command line:
- `~` - Home Directory
- `.` - Current Directory
- `..` - Parent of current directory
- `/` - Root Directory

You can move to a directory by typing `cd` followed by that directory. You can either pass an absolute (from the root directory) or relative path. 
- Paths that start with `/` are absolute
- Paths that start with `.` or `..` are relative to your current location or its parent respectively
- Paths that start with `~` are relative to your home directory

You can use `pwd` to display the **absolute path** of the current directory.

For example:
- `cd /users/arthur` uses an absolute path to change to the `arthur` directory inside of `users`.
- `cd ..` uses a relative path to change to the parent of the current directory

You can use the `mkdir` command followed by a name to create a new directory (with the specified name, inside the current directory.

You can use the `rmdir` command followed by a directory to remove that directory. Similarly you can use `rm` to remove a file.
## Command Options
Pretty much all Linux commands can be augmented with options. We're going to go over what these are using the `ls` command, which lists all files and directories in the current file.

These usually start with a minus sign followed by a letter. These options can do different things depending on whether a lower case or upper case letter is used. 
For example:
- `ls -a` means list **all** entries. It does not ignore hidden entries.
- `ls -A` means list **almost all** entries, and does the same as `ls -a` except it doesn't list the implied `.` and `..` that exist in almost all directories.
In this case the difference is fairly minimal, but can be more extreme.

You can use more than one option at the same time. For example the `-l` option tells `ls` to use a long listing format. So if you use `ls -la` then it knows to list all files in a long listing format.

You can see an example call of `ls -la` below 
![[ls-la.png]]

You can type `man <command>` to view the manual for a command, this will detail the options available for that command.
## File Permissions
In the example `ls -la` call above you can see on the left strings that look like
- `drwx--x--x`
- `-rw-r--r--`

These 10 character strings show the **permissions** for these files. It is split into four parts:
- The first character indicates directories and other special files
- The next three characters indicate user permissions (the current user)
- The next three characters indicate group permissions (the groups the current user is in)
- The last three characters indicate other permissions (everyone on the system)

Each 3 character section which indicates permissions follows the same structure:
- The first character is either `r` (for read) or `-` 
- The second character is either `w` (for write) or `-`
- The third character is either `x` (for execute) or `-`
If a letter is not present, it indicates that permission doesn't exist, for that user/group/everyone depending on which section it is in.

On Linux systems every user belongs to a group, and can be in multiple groups. Every process is owned by a user and a group, even system processes.
### Root User
Linux has a special user called **root**. Anyone logged in as root has **full access to everything**. Permissions do not apply to them.

Many system files and background processes are owned by the root user, which is shown when you visit their permissions.

The root login is disabled in most modern Linux systems. It still exists but just can't login to the system. A user can temporarily request root permissions to perform privileged actions by using the `sudo` command.

>Root user and root directory are completely different concepts. Root just means 1st/original.
### Changing Permissions
You can use the `chmod` (change mode) command to change the permissions of a file.

The command follows the format `chmod [ugo][+-][rxw] filename` where `[abc]` represents a choice of one of the characters in the square brackets
- Your choice of `u`, `g`, or `o` represents who you are changing the permissions for (user, group, or others)
- Your choice of `+`, or `-` represents if you are adding or removing a permission
- Your choice of `r`, `x`, `w` represents which permission you are changing

For example:
- `chmod g+w filename` adds write permission for the users group(s)
- `chmod o-r filname` removes read permission for everyone else (others)

You can also use 3 digit octal values to change permissions quickly. The way to do so uses the table below. You add up the permissions to get a digit. The first digit represents the user permissions, the second permission represents the group permissions and the last digit represents the other permissions.

| (add up) | Value |
| -------- | ----- |
| Read     | 4     |
| Write    | 2     |
| Execute  | 1     |
So if we had a file and we want the user to be able to read write and execute, the group to be able to read and execute and for everyone else to be able to read, we can do the following:
- Add 4 + 2 + 1 for our user, giving us a first digit of 7
- Add 4 + 1 for our group, giving us a second digit of 5
- Add 4 for the others, giving us a last digit of 4
This gives us the octal number **745** which corresponds to the strings
- `-rwxr-xr--`
- `drwxr-xr--`
(Note that the first character is decided by the type of the file, and so isn't a part of our octal value)
## Linux Assembly Coding
We can write and compile assembly code in Linux by using NASM.

You need to:
- Put pure assembly code into a text file
- Use interrupts to trigger system calls to read, write, exit, etc.
- Compile with command line options
- Link to an executable with further options.

To compile and run some assembly code stored in `hello.asm`
```
nasm -f elf32 hello.asm
ld -m elf_i386 hello.o -o hello 
./hello
```

This is much more complicated than writing code in Visual Studio with the C wrapper.

You will get a chance to play with this in the labs later in the semester. You can look at the man pages for `nasm` and `ld` if you want to see what these options do.

For example to display some text we can do
```
global _start ; Tell linker where to start 
section .data ; Constants go in .data section 
	msg db ‘Hello World!’, 10, 0 ; db = define bytes (10 = \n) 
	len dd 13 ; dd = define dword (32 bits) 

section .text ; Code goes in .text section 
	_start: 
		mov eax, 4 ; 4 = sys_write 
		mov ebx, 1 ; 1 = file handle for STDOUT 
		mov ecx, msg ; Address of string 
		mov edx, [len] ; Length of string 
		int 0x80 ; Trigger interrupt 
		mov eax, 1 ; 1 = sys_exit 
		int 0x80 ; 0x80 is 128 decimal
```

The assembly instructions are familiar but there are a lot of new concepts. I recommend going through the labs to fully grasp these concepts.