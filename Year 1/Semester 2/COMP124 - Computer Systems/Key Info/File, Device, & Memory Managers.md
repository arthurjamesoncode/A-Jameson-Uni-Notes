---
cssclasses: flashcards
---

## File Manager Overview & Disk Drives
### What does the file manager do?
The file manager's job is to keep track of all the files in the OS and map the logical file system onto the physical organisation of data on disks.

Generally it:
- Organises files into directories
- Maps the logical structure onto disk
- Enforces file permissions
- Deals with file operations
### What is a disk drive?
A disk drive is where programs/data are stored before being loaded into main memory. They are non-volatile so programs must also save any data they wish to persist to the disk.
### What types of disk drive are there?
There are two common types of disk drive:
- Hard disk drive (HDD)
- Solid state drive (SSD)
### What is a HDD and what are its properties compared to SSDs?
HDDs are mechanical devices with moving parts. They contain a magnetic disk and a read/write head which moves across it. 

Compared to SSDs they:
- Have slower access speeds, since the disk need to spin and the head needs to move
- Have shorter lifespan from wear and tear
- Use more power (around 8 watts)
- Risk being damaged by vibrations and knocks
- Are much cheaper for the same amount of space
### What is an SSD and what are its properties compared to HDDs?
SSDs have no moving parts. They use NAND flash chips to store data via electronic circuits. 

Compared to HDDS they:
- Have faster access speed
- Have a longer lifespan
- Are more energy efficient (around 2 watts)
- Impervious to knocks and vibrations
- Are much more expensive for the same amount of space
### What is a disk block?
A block is a unit of memory that disk drives are split into.

Each block can only hold information from one file. Files can be larger than a block and therefore take up many blocks.
### How big is a disk block?
This depends on the OS but typically are around 4KB or 4096 bytes.
### What is a partition?
Partitions are a section of a disk drive which has been formatted with a particular disk format. 

Formatting a partition is what splits it into blocks of equal size.
### What is metadata?
Metadata in a disk partition is information about the disk and its files. Some space is reserved on each disk partition for metadata?
### What is the free list?
The free list is an ordered bit vector which records which blocks are not in use. 

The index of a bit matches the index of the block. 1 means in use, 0 means free.
### What are some downsides of the free list?
- If stored in main memory, can become out of sync. Needs to be saved regularly to avoid this.
- Can get pretty big. In even a small 160GB hard drive 5MB would be needed to store the free list.
## File Systems
### What 4 parts make up a file system?
File systems are made of:
- Physical storage on disk - Formatted as one of disk formats.
- Logical naming scheme - File and directory names, along with the way they are nested
- Permissions model - Some way to control access to files
- System calls - Standardised programmatic access to files via the kernel
### What file handling system calls do we need for this module?
We need to know 6 file system calls for this module:
- `fopen` - Open a file
- `fclose` - Close a file
- `fread` - Read from a file
- `fwrite` - Write to a file
- `fseek` - Change the current file position pointer
- `fflush` - Forces unwritten buffered data to be written to its destination

>I don't think you need to know this but eh
### What is an inode?
An inode stores metadata for a specific file. It points to the physical blocks on disk which hold that file.
### Where are inodes stored?
Inodes are stored in the inode table. This is stored somewhere on a given disk partition and is created during formatting.
### What methods are used to access files?
Files are accessed by one of two methods:
- **Sequential file access** - Starting with the first block of a file, read each block in turn until the required data is found
- **Direct file access** - Skips the earlier blocks of a file to go directly to the block that contains the required data
### What file allocation methods are there?
There are 3 file allocation methods for this course:
- Contiguous
- Linked
- Indexed
### What is contiguous allocation and how does the inode table look?
Contiguous allocation is when each file is allocated across contiguous blocks on disk. All blocks for a given file are stored next to each other.

The inode for a given file stores the start block number and then the amount of blocks.
### What are the pros/cons of contiguous allocation?
The advantage of contiguous allocation is it is fast for both methods of access, sequential and direct.

There are some significant problems with contiguous allocation:
- Fragmentation of free blocks, requiring regular defragmentation
- Needs some way/policy for choosing which free blocks to allocate to a new file
- Files don't necessarily have room to grow after initial allocation
### What is linked allocation and how does the inode table look?
Linked allocation is when each block contains a pointer to the next block at its end.

The inode table stores only the index of the start block.
### What are the pros/cons of linked allocation?
Advantages of linked allocation are:
- It's easy to grow and shrink files
- No danger of fragmentation of free blocks

The disadvantages are:
- Blocks are widely dispersed (only really affects HDDs, since the mechanical head has to move to each block)
- Sequential access is slightly less efficient
- Direct access is even worse, since you have to read the end of the first $n-1$ blocks to get to block $n$. This means you have to read $n$ things to get data from the $n$th block.
- Danger of pointer corruption. If a block stores the wrong number at the end of it, then the file becomes unreadable.
### What is indexed allocation and how does the inode table look?
Indexed allocation is when the first block of a file holds the index to all other blocks in the file.

The inode table stores just the index of first block.
### What are the pros/cons of indexed allocation?
The advantages of indexed allocation are:
- Each file's block information is held in one place
- Very efficient for both sequential and direct access

The disadvantages are:
- Blocks can still be widely dispersed
- Wastes a block for very small files
- Can run out of pointers for very large files, requiring us to chain index blocks
- If the index block gets corrupted, the file becomes unreadable
### What windows disk formats do we need to know for this course?
We need to know 2 disk formats:
- File Allocation Table (FAT)
- New Technology File System (NTFS)
### What is FAT and how is a FAT disk formatted?
File Allocation Table is a disk format which uses indexed allocation.

A fat disk is formatted into 4 sections:
- Boot sector - Contains bootstrap code (if on primary disk) and housekeeping data
- FAT - Master copy of the index blocks for each file (the inode table)
- FAT (copy) - A backup copy of FAT used to help recover from corrupted disks
- Data region - Contains the blocks storing the actual content of files
### What are the pros/cons of FAT?
The advantages of FAT are:
- Can be understood by all major OSs
- All pointer information is stored in the same place
- Easier to protect from corruption
- No need for a separate free list
- Direct access is way more efficient

Disadvantages:
- Slow in HDDs as the head must move constantly between the FAT area and file area
- Space for FAT must be reserved when the disk is formatted
- FAT will become huge for large disks
### What is NTFS and what optimisations does it offer?
New Technology File System is a more modern version of FAT. It is the default installation for modern windows systems.

It offers
- Access Control List (similar to Linux permissions)
- Encryption
- Journaling
- Hard Links
- File Compression
- System Compression
- Sparse Files
- Shallow Copies
- Disk Quotas
### What are popular file systems by OS?
Windows installations typically use either FAT32 or NTFS.

MacOS installations use APFS (Apple File System), but can also read and write to FAT disks. MacOS can read NTFS but can't write to them without significant system changes.

Most Linux installations use EXT4 (EXT2 and EXT3 are earlier versions of the same system). EXT4 disks can't be read by MacOS or Windows so, when using Linux, for portable disks you should use FAT.
## Linux & Files
### What is the fundamental concept that Unix/Linux is built on?
Everything in the OS is a file.
### What two things can file system mean?
- The overall tree structure of the logical representation
- The physical format of each disk
### What special directories exist for in Linux file system tree?
- `/dev` is a virtual file system where each subdirectory maps onto a physical device
- `/home` is a top level directory which stores specific user directories. The system must be fully loaded to access
- `/proc` is a virtual file system which stores information about all current processes
- `/root` is the home directory of the root user
- `/boot` is used to store the kernel image and other required boot files
### What does mount mean?
To mount a part of the file system (device, disk, etc) means to make it accessible to the OS.
### What does the `df` command do?
The `df` command can be used to see mount points and physical disks.
### What is EXT4?
EXT4 is the file system used in most installations of Linux.

Every file (and directory) has an **inode** associated with it. Again these are stored in the **inodes table** and which inodes are free/used are stored in the **inodes bitmap** (the free list).

Each file inode stores:
- Size of the actual file on disk;
- Owner, group, octal permissions value;
- Type of inode (normal file, directory, link etc.);
- Timestamps (created modified accessed);
- Start and end block numbers of actual data on disk (fragmented files store a list of start end fragments);
And much more.
### What are the strengths of EXT4?
EXT4 can support very large disks and file sizes:
- Disks up to 1 exabyte (1 billion GB)
- Individual file up to 16 terabytes (16,000 GB)
- Standard disk block size is 4KB (but can go up to 64KB)

It also provides many features that improve performance, stability, and security.
### How are filenames stored in EXT4?
Filenames are not stored alongside the inode in EXT4.

Instead the content of each directory is stored as a normal file in a block somewhere on disk. This file maps all the inodes of files/directories inside this directory to their name.
### How are files deleted?
Files are deleted by removing the inode. The actual data is not overwritten.
### What are secure delete/format options doing?
They are ensuring that deleted data cannot be recovered by repeatedly writing random data to the blocks.
### How many EXT4 optimisation features are there and what are they?
There are 4 we need to know for this module and they are:
- Journaling - Part of the disk stores a list of changes allowing for quick recovery but slightly slower write times
- Scattering - New files are spread evenly across the disk leaving room for contiguous growth
- Delayed allocation - Creates virtual blocks in memory while file is written only writing to disk when the final size is known. Allows for contiguous space in memory to be found.
- Persistent Pre-allocation - Can use `fallocate` to reserve space for a file.
### What is a symbolic link?
A symbolic link is a new filename for an already existing file. The data is not stored twice, just has two references to it.
### What is a hard link and how do I create one?
A hard link is when the new name has the same inode as the original name. Hard links must be in the same disk partition.

```
ln file1 file2 
```
### What happens if I delete a hard link?
If I delete any hard link to a file, it does not delete the file unless I am deleting the last hard link.
### What is a soft link and how do I create one?
A soft link is a new file which contains the original files name in it. This allows us to create links across partitions.

```
ln -s file1 file2
```
### What happens if I delete a soft link?
If I delete a soft link nothing changes in the file. If I delete the file, however, the soft link will be broken and now point to an invalid location.
### What is a file descriptor?
This is a positive integer number that acts as a label for any **open file**. 

This is distinct from filenames and inode numbers and is what is passed to system calls that act on open files.

The file manager maps these descriptors onto physical files or streams.
### What standard streams does every Linux system have?
- `stdin` - File Descriptor 0 - Standard input (keyboard)
- `stdout` - File Descriptor 1 - Standard output (shell terminal)
- `stderr` = File Descriptor 2 - Standard error
### What soft links does Linux maintain in its virtual file system?
- `/proc/self` always points to the current process
- `/proc/self/fd` is a directory which contains links to every open file descriptor
- `/dev/stdin`, `/dev/stdout`, `/dev/stderr` point to the current process streams
## Device Manager
### What does the device manager do?
The device manager monitors/tracks every device in the system and ensures that each process gets fair access to the devices they need.

Generally it:
- Tracks all connected devices
- Creates virtual files in the `/dev` directory
- Schedules read/write access to devices
- Handles multiple requests for the same device
- Provides system calls for interfacing with devices
- Deallocates resources when a device is no longer needed
### How can devices be categorised?
They can be categorised by:
- Quantity of Data: Character/Block
- Order of access: Sequential/Random
- Who has access: Shared/Dedicated
- Speed of operation
- Data direction: read-write/read-only/write-only
### What does a device driver do?
The device driver of a device converts the action that a system call from the OS wants to perform into instructions the physical device controller can understand.

The devices simply look like normal files/streams to the kernel.
### What device busses do we need to know about and what are they used for?
There are 4 device buses we need to know about which are:
- **PCIe** - Peripheral Component Interconnect Express - general purpose
- **USB** - Universal Serial Bus - general purpose
- **NVMe** - Non-Volatile Memory Express (also called **M.2**) - flash disks (SSDs)
- **SATA** - Serial AT Attachment - mechanical disks (HDDs)
### How do device buses communicate with the CPU?
Through the system bus and interrupts.
### What are the goals of a device/disk scheduling algorithm?
It wants to:
- Minimise time wasted by moving the HDD read/write head
- Prioritise I/O requests depending on process
- Ensure each process has fair access to disks
- Guarantee that important requests are met before their deadline (in real time systems)
- Minimise the overall wait time for processes in the **blocked** state
### What device/disk scheduling algorithms do we cover?
We cover 5 device/disk scheduling algorithms. 

They are:
- First Come First Served - Self explanatory
- Shortest Seek First
- Elevator Algorithm
- Completely Fair Queueing
- Anticipatory Scheduling
### What is Shortest Seek First and its pros/cons?
This is a scheduling policy that always schedules I/O so that the operation closest to the current position of the HDD read/write head is performed.

Pros:
- This minimises the amount of time that the read/write head has to move in HDDs

Cons:
- No benefit to non HDD drives
- If many operations are requested close to the current position of the read/write head, then an operation that was requested a while ago may stall or never execute.
### What is the Elevator Algorithm and what issue does it fix?
The elevator algorithm functions the same as shortest seek first but the head won't change direction to fulfil a request until it finishes all requests in the current direction.

This keeps the benefit of "Shortest Seek First" but ensures that every process gets access to any HDD eventually.
### What is Completely Fair Queueing and its pros/cons?
Completely fair queueing is a round robin approach to device scheduling.

Each process has a queue of IO requests. The system processes each process' IO requests during fixed time slice. Processes may have different priorities.

Pros:
- Ensures that every process gets fair access to each device
- No process gets completely blocked for long

Cons:
- Causes a lot of extra movement in HDDs
### What is Anticipatory Scheduling and its pros/cons?
Anticipatory scheduling is when the read write head pauses for a beat (few milliseconds) after serving a request in order to *anticipate* a new request for a nearby location.

Pros:
- Decrease movement of a read/write head since processes tend perform IO on localised areas of memory

Cons:
- Stops I/O requests from being executed for a brief time
### What if a buffer?
A buffer is an area of main memory that either:
- A whole chunk of data from disk is written to
- A whole chunk of data to go to disk is written to
### Why are buffers used?
It can be expensive to repeatedly read/write small things from/to disk. Writing everything to a buffer and then reading/writing from that increases efficiency.

Buffers are emptied when they are full, or if they transfer to the buffer has finished.
### What happens if power is cut while writing to a buffer?
Since RAM is volatile the data will be lost. Buffers must be flushed using the `fflush` system call to ensure that their contents has been written to disk.
### What is double buffering and what are its benefits?
Double buffering is when one buffer is being read to/written from by disk while another is being filled or emptied by a program?

Having two buffers increases efficiency, since we can swap between them minimising downtime.
### At what level of abstraction can buffering occur?
Buffering can happen at many levels of abstraction:
- Software programs
- Library Subroutines
- Operating Systems
- Hardware (for example, a memory buffer built into the drive itself)
### What issues can buffering cause?
Buffering can cause inconsistency issues since the data on disk might not match what the system thinks it wrote. Flushing buffers regularly is important to maintain consistency.
### What is spooling?
Spooling is a type of buffer used for non-shareable devices. 

Non-shareable devices have a daemon process called a spooler which executes spooling.
### What does a spooler do?
When a process sends its request to a non-shareable device it is caught by the spooler daemon.

The spooler then creates a temporary file for each process and the data for the request is written into the file. The file remains available while the device is busy.

When the device is free the spooler sends the request to the device which is called de-spooling.
### What is direct memory access?
Direct memory access DMA is when a device can access main memory without the CPU.
### How does DMA work?
DMA works by the CPU initiating the read/write operation before the DMA controller completes it.
### What is the benefit of DMA?
DMA allows devices to perform read/write operations without tying up the CPU.
### What can't the CPU access during DMA?
It can't access the system bus since that is tied up during the transfer.
### What is DMA controller?
The DMA controller is a hardware component of the system which communicates with both the CPU and the device controller.
### What registers does the DMA controller have?
The DMA contains:
- Memory Address Register (MAR)
- Byte Counter
- Control Register
### What transfer modes are there?
- Burst - Whole transfer done in a single burst
- Cycle Stealing - The CPU waits every few clock cycles to free up the system bus for the transfer
- Transparent - The DMA controller waits until the CPU is not using the bus to do the transfer
### Where is the device virtual file system?
In the `/dev` directory
### What virtual disk format and device manager does Linux use?
- The `devtmpfs` virtual disk format
- The `udev` device manager
### What pseudo devices are created and for what purposes?
![[pseudo-devices.png]]
### What letters do printers start with in the Linux terminal?
`lp`
### What letters do disks start with in the Linux terminal?
`sd`
### What letters do parallel ports start with in the Linux terminal?
`pp`
### What letters do terminals start with in the Linux terminal?
`tty`
### What letters do pseudo-terminals start with in the Linux terminal?
`pty`
## Memory Manager
### What does the memory manager do?
The memory manager of an OS manages the main memory (RAM) of the system. It's main job is to ensure that each process gets access to the memory it needs.

Generally it:
- Preserves & Protects space in memory for the OS
- Validates requests to access memory
- Allocates memory
- Tracks who is using each area of memory
- Deallocates memory
- Manages a swap space
- Implements segmentation or paging
### What is the linear model of memory?
Viewing the RAM in a system as a linear sequence of bytes. Also called the flat model.
### What is a process image?
The space in memory the process takes up and the data which fills that space.
### What areas make up the process image?
The process image is made up of:
- **Text** - This is the actual code that the process needs to execute.
- **Data** - This is the memory allocated for variables and objects declared in the high-level code.
- **Heap** - This is memory available for the programmer to reserve. It is dynamically resized and grows upwards
- **Stack** - grow downwards and used for calling subroutines, holding local variables etc.
### What is compile time address binding?
Compile time address binding is when jumps and loop locations are turned into fixed memory addresses when compiled.
### What are the problems of compile time binding?
When using compile time address binding:
- The MMU cannot load the program into any other space in memory
- Cannot run multiple programs compiled to run in the same space
- MMU cannot make the most efficient use of memory
### What is load time address binding?
Load time address binding is when jumps and loop locations are turned into relative memory addresses when compiled. So each jump address is encoded as a difference such as `-8`, `+50` etc instead of a fixed number.
### What is dynamic/run-time address binding?
Dynamic address binding is when a process that takes up $N$ bytes is given its own logical address space from $0\to N$ at compile time. Each address is **relative** to the start of the process.
### How is dynamic address binding different?
Dynamic address binding is separated from the others as it binds jumps to a logical address space instead of a physical one.
### How does the MMU map logical addresses to physical ones with dynamic binding?
The CPU has a relocation register which holds the real address of the start of the process. The logical addresses are mapped relative to this base value.
### What are the advantages of dynamic binding?
- The memory locations of programs can be changed **after they are loaded**.
- It is **not necessary** for all of a running program to be stored **contiguously**.
### What is a processes base/datum and its limit?
Each process has:
- A **base** or **datum** - The start location of the process in memory
- A **limit** - The length of the process (in bytes)
### What is fragmentation?
Fragmentation is when there is gaps in memory between memory allocated to processes.
### What problems can fragmentation cause?
Fragmentation can mean there isn't enough contiguous space to load new processes and the read/write head must move more?
### What memory allocation policies do we need to know?
- **First fit** - choose the first free space that is big enough
- **Best fit** - choose the smallest free space that is big enough
- **Worst fit** - choose the largest free space if big enough
### What is the 50% rule?
The 50% rule is that if $n$ blocks are currently allocated then the number of unoccupied blocks will be about $n/2$.
### How can the memory manager defragment memory?
By moving processes around. Requires dynamic binding.
### What must the MMU do when moving processes?
It must:
- Update the relocation register so logical addresses map correctly
- Pause the execution of the processes while the move takes place
### What are the limitations of the linear memory model?
- Processes cannot share subroutines with each other
- Memory allocation doesn't map onto high level program structures
### What is swapping?
Swapping is when process images are saved on disk before they are taken out of memory and replaced with a different process. The process images are save in a swap space.
### How can library routines be included in compiled programs?
Library routines must be linked to by the program by either:
- Static linking
- Dynamic linking
### What is static linking and its downsides?
Static linking is when copies of the library code are added to the final program image.

Downsides:
- Wastes a lot of space on disk and in memory
- Program images can become huge if they use a lot of libraries
### What is dynamic linking and its benefits?
Dynamic linking is when a small stub is included in the final program image which tells the memory manager where to find the library code. If not already in memory, then it will be loaded into memory.

Benefits:
- allows library code to be shared between processes
- helps keep the disk image small while using less main memory

It does require the operating system to support it. Windows supports it through `.DLL` files.
### What is dynamic loading?
Dynamic loading is when the programmer makes it so the program can start without all required libraries being loading into memory.

When these libraries are needed they are attached to the process image while it is running.

When no longer needed the library can be detached to free up space in memory.
### What is the difference between dynamic loading and dynamic linking?
- Dynamic loading is controlled by the programmer.
- Dynamic linking is controlled by the OS's memory manager.
### What must support dynamic loading for it to be possible?
- The library
- The programming language
- The operating system
### What is segmentation?
Segmentation is when each process is split into multiple segments which don't need to be loaded contiguously.
### How does segmentation work?
Each process has a segment table which stores:
- An index for the segment
- The length of each segment (limit)
- where it starts (datum)

This is stored in the segment table base register in the CPU.
### What are the advantages of segmentation?
- Memory allocation reflects the high level program structure (subroutines, data, stack)
- Memory protection is enhanced (can't overwrite subroutines or execute data)
- Segments can be swapped out when not needed
- Segments can be reused by multiple processes
### What registers does the CPU have for dealing with segmentation?
- `CS` - Code segment register
- `DS` - Data segment register
- `SS` - Stack segment register
- `ES` - Extra segment register (often used for string programming, but use is defined by programmer)
- `FS` - additional register (use is defined by programmer)
- `GS` - additional register (use is defined by programmer)
### What are `FS` and `GS` used for now that segmentations is less popular?
Mostly used for support for multi-threaded processes.
## Paging Memory Model
### What is the paging memory model?
The paging memory model splits the physical memory into equal sized blocks. The address space for each process is then spread across as many pages as necessary.

Pages do not need to be consecutive, but the process memory addresses will still appear to be one contiguous range.

The physical memory used by a page is called the page frame.
### How are process pages mapped to their physical frames?
Each process has a page table which is stored in memory as part of the process image.
### Where is the page table address stored?
In page table base register in the CPU.
### What does the page table look like?
The page table is the index of the page in the program matched to the index of the page frame used to store it. For example:

| Page | Frame |
| ---- | ----- |
| 0    | 1     |
| 1    | 4     |
| 2    | 3     |
| 3    | 0     |
### How to find the physical location of an instruction given a virtual address?
The address will be split into 2 parts. 
- The most significant part is the index of the page, which allows us to find the actual page frame index from the page table.
- The least significant part is the offset into the page

The parts may not be equal. You will be told how they are split in any question which asks about this.
### What is the difference between segmentation and paging?
For segmentation:
- It is a logical division of the address space
- Segments can be different sizes
- The segments match the structure of the program

For paging:
- It is a physical division of the address space
- Each page is always the same size
- Pages have no relation to the program structure
### Why is paging used over segmentation in modern systems?
- Memory allocation is much easier since all the pages have the same size.
- Fragmentation is eliminated, although there is some wasted space in the final page of a process
### What is page swapping?
Page swapping is like process swapping except instead of storing process images on disk you store pages.
### What is a page fault?
A page fault is a type of interrupt (not an error) that is generated when a process tries to access a page which is not in memory.
### What is demand paging?
Demand paging is when pages are brought in when needed.
### What is anticipatory paging?
Anticipatory paging is when a system brings in more pages than it needs after a page fault.
### What page replacement policies do we need to know?
We need to know:
- **Least Recently Used** (LRU) - Remove the page that has been unused for the longest time
- **First In First Out** (FIFO) - Remove the page that has been in memory the longest
- **Least Frequently Used** (LFU) - Remove the page which has the fewest references in a recent period
- **Second chance** - Works like FIFO but keeps pages that were recently used.

Honourable mention to Longest Forward Distance, for being optimal except that we can't see the future.
### What is the principle of locality?
The principle of locality states that: "Over any short period of time, a process's memory references tend to be spatially localised"

Generally execution stays within roughly 20% of a process's pages for 80% of the time it runs. We can use this to try and estimate the **working set** of our process.
### What is the working set?
The working set of process $W(T,s)$ is the set of pages used in the time period from $T$ to $T+s$ **INCLUSIVE**.
### How do we predict the working set?
By the principle of locality, the set $W(T, s)$ is likely to be similar to the set $W(T-s-1,s)$
### How does size affect how accurate a working set prediction is?
- If the set is too small it won't cover the entire locality for the current process
- If the set is too big it will cover several localities and result in redundant page swapping
### What happens when a process moves from one locality to another?
The number of pages faults increases. This is expected.
### How much memory is wasted in paging?
On average, a system will lose about 50% of a page due to internal fragmentation. This means that the size of the pages affect how much memory is wasted per process.
### How does page size affect system performance?
- Large pages don't need as large a page table but increase the amount of wasted memory in the last page of each process.
- Smaller pages make better use of memory and have less internal fragmentation, but they increase the chance of **page faults** since it is more likely that the required code/data are in a different page.
### What is the default page size in windows and Linux?
4KB
### What is the CPU cache?
The CPU cache is an area of memory in the CPU itself which is slower than the CPU register but faster than main memory.
### What is a cache hit and cache miss?
When the CPU requests data from memory it first checks the cache:
- If the data is in the cache it is a **cache hit** and the CPU can immediately read the data from the cached copy.
- If the data is not in the cache it is a **cache miss**. When this happens the MMU copies a data block from main memory into the cache.
### Why is a data block copied into the cache and not just the required data?
By the principle of locality, the surrounding addresses are likely to be requested soon as well. Moving them into the cache decreases the chance of a cache miss in future.
### What levels of cache do modern CPUs have?
- L1 Cache - Small and fast cache close to the CPU registers
- L2 Cache - Slightly bigger and slower cache compared to L1
- L3 Cache - Bigger and slower cache compared to L2
### How are these caches structured in multi-core processors?
- Each core has its own L1 cache
- Each pair of cores share an L2 cache
- All cores share an L3 cache