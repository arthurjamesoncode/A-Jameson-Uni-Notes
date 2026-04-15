## Linux & Files
The fundamental concept that Unix (and therefore Linux) is built on is that **everything is a file**.

This applies to things you wouldn't expect:
- Pipes
- Sockets
- Processes
- USB ports
- Printers
- Hard drives
- Kernel data structures

This is convenient, as it allows the same system calls and commands to access everything, presenting a clean system call API to applications and developers.

Users and programs see a unified **logical** view of the file system as a tree structure of nested directories and files.

This is an abstraction because in reality:
- Some parts of the tree might be stored on separate disks
- Some might be stored on a network (remote files)
- Some might be stored in main memory (virtual file systems)
Each place that can store files can be formatted with a different physical disk layout

The phrase **file system** can be used in two ways:
- To mean the overall tree structure of the entire **logical representation**
- The **physical format** of each disk
## Logical System Tree
The Linux file system tree is a logical structure separate from the physical layout of the files on disk.

Part of the Linux file system tree are some special directories:
- `/dev` is a virtual file system (meaning it is stored in main memory). Every subdirectory maps onto a physical device, and stores relevant information about that device.
- `/home` is a top level directory that would store, for instance, specific user directories. In network systems this would usually be located on a server. This directory is not available until the system has fully booted
- `/proc` is a virtual file system which stores dynamic data about all current processes.

Each part of the logical file system could use a different physical disk or different disk format.

There are two directories that need to be available while the system is booting and the kernel is forking its initial processes:
- `/root` is the home directory of the super user. The root user is needed to spawn new processes during start up so must be stored separately from the home, which may not be accessible yet.
- `/boot` is used store the kernel image and other required boot files. The bootloader knows where this is and how to read it's files.

Other parts of the logical file system are **mounted** (created/made accessible) in correct place by the kernel after it has finished loading.

The `df` command can be used to see mount points and physical disks.
## EXT4 File System
The EXT4 file system is one of the most common Linux file systems. It is an updated version of EXT2 which dates back to 1993.

It has many strengths including proven stability, reliability, and performance and is the default file system on a lot of Linux installations.

EXT4 can support very large disks and file sizes:
- Disks up to 1 exabyte (1 billion GB)
- Individual file up to 16 terabytes (16,000 GB)
- Standard disk block size is 4KB (but can go up to 64KB)

It also provide many features that improve performance, stability, and security.

Every file (and directory) has an **inode** associated with it. Again this are stored in the **inodes table** and which inodes are free/used are stored in the **inodes bitmap** (the free list).

Each file inode stores:
- Size of the actual file on disk;
- Owner, group, octal permissions value;
- Type of inode (normal file, directory, link etc.);
- Timestamps (created modified accessed);
- Start and end block numbers of actual data on disk (fragmented files store a list of start end fragments);
And much more.
## Directory Data Structure
A file inode does not store the name of the file itself.

Instead the content of each directory is stored as a normal file in a block somewhere on disk. This contains the filename of each file in the directory and its corresponding inode number.

Permissions and other metadata about each directory are stored in the inode that points to that directory data block.

Since directories are nested some of the inodes listed in the directory block could point to other directory blocks, and so on.

The Kernel has to follow a trail of inode numbers and block indexes before it can finally read the actual data blocks for a file. You can see a figure illustrating this below:
![[read_trail.png]]
## Deleting Files
When a file is deleted, its data blocks are not actually removed. Writing over the data with 0s would waste a lot of time. 

Instead, only the inode is deleted to remove the link to the data and the free list updated to mark the data blocks as free.

Because of this, it is actually possible to recover deleted files with specialist software. This may be done for many reasons:
- Recovering mistakenly deleted files
- Recovering evidence for criminal investigations (computer forensics)
This is only possible if the block has not already been overwritten.

Many OSs provide **secure delete** and **secure format** facilities which completely erase a file or an entire disk. This works by repeatedly writing random data to the relevant blocks.
## EXT4 Optimisation Features
EXT4 has many optimisation features which we will go over now.
### Journaling
Part of the disk is used to store a journal of changes made to inodes and data blocks. Changes are only applied to disk after they are recorded in the journal.

Writing data is slightly slower, since you need to write everything twice, but this allows for quick recovery when system crash since it only needs to check and apply the journal entries.
### Scattering
New files are spread evenly across the disk, leaving large gaps between each file. This allows files to grow contiguously and decreases their chance of getting fragmented.
### Delayed Allocation
Creates virtual blocks in memory while file is written. Only commits this to disk when the final size is known. This allows the system to find contiguous blocks of free space.

This can lose data if the memory is not written to disk, and isn't always suitable for some users or situations. Linux allows you to turn this off for specific disks.
### Persistent Pre-Allocation
A system call (`fallocate`) can be used to reserve space for a file. All the needed blocks and data are allocated and filled with zeroes before the real data arrives.

This can be used to guarantee a contiguous set of blocks for the file, and improves read/write speed for media streaming and database applications.
## Symbolic Links
We can give a file a second filename using the `ln` command

For example:
```
ln file1 file2 
```

This creates a **hard link** to `file1` called `file2`. A hard link can be in a different directory but not in a different data partition.

Since the names of files are stored in the **data file** for the directory which stores it, `file2`'s name is added to this file along with the **inode reference** for `file1`.

This means that a single **inode** can be referenced from multiple entries in one directory, or multiple entries in two directories. You can see a figure depicting this below:

![[hard_link.png]]

If an inode is referenced by multiple file names, deleting a single file name will not delete the inode. The inode is only deleted when it's **final reference** is deleted.

If we want to store a link to a file on a different disk partition we can create a **soft link** to the file. We do this by using the `-s` option.

For example
```
ln -s file1 file2
```

This creates a **soft link** to `file1` called `file2`. This creates a new file, with a new inode, called `file2` and stores `file1`'s name in it. `file2` and it's inode reference are then added to the relevant directory data file.

This allows us have links which refer to files across different disk partitions, but adds a layer of indirection.

If `file1` is deleted, the link from `file2` will be broken. This means that soft links may point to an invalid location.
## File Descriptors and Standard Streams 
Every open file has a numeric file descriptor (a positive integer which acts as a label)

This is used by system calls instead of file names and is NOT the same as the inode number.

The file manager maps file descriptors onto physical files or streams (see below). The descriptor is recorded in the PCB of processes using the file.

Every Linux system has three standard streams (linked to shell terminal/keyboard):
- `stdin` – **FD 0** – Standard input 
- `stdout` – **FD 1** – Standard output
- `stderr` – **FD 2** – Standard error (where error messages are sent)
Note that **FD** stands for File Descriptor.

The C `printf` and `scanf` subroutines are just wrappers around system calls that use file descriptors 1 and 0 internally. 
## Device and Process Soft Links 
Linux maintains various soft links within its **virtual file system**
- Link at `/proc/self` always points to the current process
- The `/proc/self/fd` directory contains links to every open file descriptor 
- Links at `/dev/stdin`, `/dev/stdout`, `/dev/stderr` point to current process streams 
These links are updated in the background as part of every context switch

We can see how these soft links work with a simple terminal command 
```
$ echo “Hello” > /proc/self/fd/1 Hello
``` 

Remember that Linux treats everything as a file (using the same system calls)
- Can perform terminal I/O by reading and writing standard streams
- Can access virtual files associated with processes and devices
- Can read and write network sockets as if they were local files




