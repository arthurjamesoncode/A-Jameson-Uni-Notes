## File Manager
The file manager keeps track of every file in the operating system. It provides an **abstracted view** of files to the user, and maps this onto the **real organisation** of data on the disk.

This abstracted view is called the **logical file system**. This is the organisation you see though applications like finder on mac, or system explorer on windows.

The real organisation is called the **physical file system**. The end user of the operating system never sees this. It refers to the actual locations of each file on disk.

The file manager performs a number of tasks for the operating system:
- Organises all files into folders/directories
- Manages the real locations of files on disk
- Maps the logical structure on to the physical locations
- Enforces restrictions on who can access files (via the **permission system**)
- Deals with standard file operations (open, close, read, write etc.)
- Provides standard system calls so other software can use files
- Liaises with the device manager to access physical disks within the system

This lecture will be spent going over the ways it does all of this.
## Disk Drives
Disk drives are where programs and files are stored before being loaded into main memory.

There are a few types of disk drive, but we focus on two common ones:
- Hard Disk Drive (HDD)/Mechanical Drive
- Solid State Drive (SSD)

>Note that we can use the word "disk" to refer to either type of drive, not just HDDs. "Disk" is typically used to just differentiate the memory in drives from main memory (RAM)

You can see an image of them below.
![[disk_drives.png]]

Whichever type of drive the system uses, the operating system provides a level of abstraction over the physical hardware. Read and write speeds may be different, along with some other properties, but, as far as interacting with the data on the drive, there is no difference to the user.

HDDs are mechanical devices with moving parts. They contain a magnetic disk and a read/write head which moves across it. Compared to SSDs they:
- Have slower access speeds, since the disk need to spin and the head needs to move
- Have shorter lifespan from wear and tear
- Use more power (around 8 watts)
- Risk being damaged by vibrations and knocks
- Are much cheaper for the same amount of space

SSDs have no moving parts. They use NAND flash chips to store data via electronic circuits. Compared to HDDS they:
- Have faster access speed
- Have a longer lifespan
- Are more energy efficient (around 2 watts)
- Impervious to knocks and vibrations
- Are much more expensive for the same amount of space

Note as well that fragmented physical storage of files causes slowdown when using a HDD, as the mechanical head needs to move more in order to read a program or file from disk. SSDs do not suffer from the same problem as there are no moving parts.

SSD's are obviously superior in pretty much every way except for price.
## Disk Blocks & Partitions
Disks are based around the idea of blocks. 

Every disk is split into blocks of certain size. How big the blocks are depends on the OS. Typically they would be about 4KB or 4096 bytes.

Each block can only hold information from one file, but files can be larger than a block and therefore fill multiple blocks. If a file doesn't fully fill a block, the remaining space is wasted.

Each physical disk can be divided into separate partitions. Each partition is formatted with a particular disk format, for example FAT (File Allocation Table) which will be covered later in this note. Formatting each partition splits it into blocks of equal size. The disk format and block usage is determined by the file allocation method.
## Free List & Metadata
Some part of each disk is reserved to store the data about the disk and the files on it (metadata). Since not all blocks are used for data, so the total storage size is less than the total disk size.

Some blocks store something called the **free list**. This is a simple bit vector that records which blocks are not in use. 1 means in use, 0 means free and eight blocks can be represented by one byte.

The free list lets the file manager easily see which blocks are available for new files to be stored in, although modern disk formats use a much more complex set of metadata which takes more room to store.

There are some disadvantages of the free list:
- If stored in main memory, can become out of sync. Needs to be saved regularly to avoid this.
- Can get pretty big. In even a small 160GB hard drive 5MB would be needed to store the free list.
## File Systems and System Calls
Every file system is made of four parts:
- Physical storage on disk - Formatted as one of disk formats.
- Logical naming scheme - File and directory names, along with the way they are nested
- Permissions model - Some way to control access to files
- System calls - Standardised programmatic access to files via the kernel

System calls include:
- `fopen`
- `fclose`
- `fread`
- `fwrite`
- `fseek`
- `fflush`

These standard system calls let any program manipulate data in files. The same calls are used regardless of the type of drive or disk format. They provide an abstraction of the underlying disk hardware.

The user, along with user programs and code, can see the **logical view** of the file system through these system calls.
## Logical & Physical Views
Operating systems provide plenty of conveniences to make life easier for us, such as:
- Filenames with extensions (e.g. `.txt`, `.pdf`)
- Directory hierarchies with nested folders and files
- Graphical shell with drag and drop control to move/copy files
These conveniences and abstractions form the **logical view** of the file system.

The operating system itself doesn't follow these conveniences. They are only needed for humans. 

For an OS, directories and files are just bit patterns stored in blocks of the disk. The OS needs to know which blocks belong to which files and so metadata about block usage and files is also stored on the disk.

The exact arrangement and usage of blocks depends on the **file allocation method**. All of this together forms the **physical view** of the file system.
## Inodes & Metadata
We need some way to map the logical view to the physical locations on the disk. We do this by using **inodes**.

Every file has an inode which stores metadata about it. This **inode** points to physical blocks on the disk, and stores block information (for example the start block) depending on the allocation method.

Inodes are stored in the **inode table**. We need to store the inode table somewhere on disk. It is usually created during formatting.

Every disk will have housekeeping data that needs to be stored. Exactly what this looks like depends on the disk format.

All the metadata that we need to store reduces the actual capacity of the disk.
## File Allocation & Access
The are several ways to allocate files to blocks on a disk:
- Contiguous
- Linked
- Indexed

Different disk formats have different file allocation methods. These dictate how easy it is to access the blocks of a file.

Files are accessed by one of two methods:
- **Sequential file access** - Starting with the first block of a file, read each block in turn until the required data is found
- **Direct file access** - Skips the earlier blocks of a file to go directly to the block that contains the required data

We will now go over the different types of file allocation, and how easy they are to access with either method.
### Contiguous Allocation
In contiguous allocation, each file is allocated across contiguous blocks on the disk. This means that all blocks of a file are stored next to each other.

Below you can see a example **inode table**, with a graphical representation of the blocks it stores.
![[contiguous_allocation.png]]

The **inode** stores the start block number and the number of blocks.

The advantage of contiguous allocation is it is fast for both methods of access, sequential and direct.

There are some significant problems with contiguous allocation:
- Fragmentation of free blocks, requiring regular defragmentation
- Needs some way/policy for choosing which free blocks to allocate to a new file
- Files don't necessarily have room to grow after initial allocation
### Linked Allocation
In linked allocation, each block contains a pointer to the next block. This is similar to how [[Lecture 10 - Linked Lists|linked lists]] work.

Below you can see a example **inode table**, with a graphical representation of the blocks it stores.
![[linked_allocation.png]]

The **inode** stores the start block and each block ends with the number of the next block.

Advantages of linked allocation are:
- It's easy to grow and shrink files
- No danger of fragmentation of free blocks

The disadvantages are:
- Blocks are widely dispersed (only really affects HDDs, since the mechanical head has to move to each block)
- Sequential access is slightly less efficient
- Direct access is even worse, since you have to read the end of the first $n-1$ blocks to get to block $n$. This means you have to read $n$ things to get data from the $n$th block.
- Danger of pointer corruption. If a block stores the wrong number at the end of it, then the file becomes unreadable.
### Indexed Allocation
In indexed allocation, the first block holds the index to all other blocks in the file.

Below you can see a example **inode table**, with a graphical representation of the blocks it stores.
![[indexed_allocation.png]]

The **inode** stores the number of the index block, which contains a list of all blocks for a file.

The advantages of indexed allocation are:
- Each file's block information is held in one place
- Very efficient for both sequential and direct access

The disadvantages are:
- Blocks can still be widely dispersed
- Wastes a block for very small files
- Can run out of pointers for very large files, requiring us to chain index blocks
- If the index block gets corrupted, the file becomes unreadable
## File Allocation Table (FAT)
Many windows installations use the FAT disk format, which stands for **File Allocation Table**.

This splits a physical disk into distinct sections (view figure below).
![[fat_disk.png]]

This uses **indexed allocation** but the index blocks are all stored in one place, the FAT. You can understand the FAT as an inode table which stores the index of each block, not just the index of the first block of the file.

The disk is formatted as follows:
- Boot sector - Contains bootstrap code (if on primary disk) and housekeeping data
- FAT - Master copy of the index blocks for each file (the inode table)
- FAT (copy) - A backup copy of FAT used to help recover from corrupted disks
- Data region - Contains the blocks storing the actual content of files

FAT can be understood by all major operating systems. As a result, it is commonly used in USB sticks.

The advantages of FAT are:
- All pointer information is stored in the same place
- Easier to protect from corruption
- No need for a separate free list
- Direct access is way more efficient

Disadvantages:
- Slow in HDDs as the head must move constantly between the FAT area and file area
- Space for FAT must be reserved when the disk is formatted
- FAT will become huge for large disks
## New Technology File System (NTFS)
NTFS is the default format for new Windows installations since Windows 3.1 (1993). Uses a **master file table** instead of a file allocation table, but the idea is the same. 

Disk's using NTFS are formatted to provide a ton of new useful features. We won't cover these in depth but here are a list of some of the most useful:
- Access Control List (similar to Linux permissions)
- Encryption
- Journaling
- Hard Links
- File Compression
- System Compression
- Sparse Files
- Shallow Copies
- Disk Quotas
## Popular File Systems
Windows installations typically use either FAT32 or NTFS.

MacOS installations use APFS (Apple File System), but can also read and write to FAT disks. MacOS can read NTFS but can't write to them without significant system changes.

Most Linux installations use EXT4 (EXT2 and EXT3 are earlier versions of the same system). EXT4 disks can't be read by MacOS or Windows so Linux, so for portable disks you should use FAT.

Other popular Linux file systems include [btrfs](https://en.wikipedia.org/wiki/Btrfs) and [ZFS](https://en.wikipedia.org/wiki/ZFS).