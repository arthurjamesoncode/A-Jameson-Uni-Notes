## Device Manager
The device manager monitors every device within the system. It ensures that every process gets fair access to the devices it needs.

The device manager:
- Keeps track of all devices connected to the system
- Creates virtual files that map onto physical devices
- Schedules read write access to each device
- Deals with multiple requests for the same device
- Communicates with devices during operation
- Provides system calls that let other software use devices
- Deallocates system resources when a device is no longer needed

The system calls defined by the device manager provide a level of abstraction to any programmer who wishes to interact with a device. You can see these levels of abstraction below:
![[device_abstraction.png]]

Each device may behave differently. They may:
- Write different amounts of data at a time. Usually this would be single-bytes (called characters) or blocks, like the disks we have looked at so far.
- Read or write in different orders. This could mean sequential, meaning read/write happens in a specific order and we can't move around (for example a keyboard always sends it's keypresses sequentially), or random meaning that read/write could happen in any order (for example how we could read/write from/to any part of a disk).
- Be shared between multiple computers or dedicated to only one machine
- Have different speeds of operation
- Allow only writing, or only reading, or both.

The kernel of the OS never knows about these differences. The **device driver** hides all of this, and provides standardised ways for the kernel and device manager to interact with it.

The **device driver** is (usually) designed by the people who made the device and is the only part that understands what the hardware needs to do. The system calls are then able to interact with the device driver in standardised ways (e.g. accessing a file in the `/dev` directory). 

The **device driver** converts the action the system calls want to do into instructions the **device controller** can understand, and this then performs whatever physical manipulations need to be done to the hardware by sending electrical signals.

This whole system of **abstraction** is essentially just multiple layers of **translation** from a higher level to a lower level.
## Device Buses
Devices aren't just the things you plug into the outside of your computer, those are called **peripherals** and are only 1 kind of device.

Other devices could be soldered onto the motherboard themselves, or may plug into slots on the motherboard, via a **daughterboard**. These could be things like disks, graphics cards, wi-fi cards etc.

There are multiple buses that are designed for different purposes:
- **PCIe** - Peripheral Component Interconnect Express - general purpose
- **USB** - Universal Serial Bus - general purpose
- **NVMe** - Non-Volatile Memory Express (also called **M.2**) - flash disks (SSDs)
- **SATA** - Serial AT Attachment - mechanical disks (HDDs)

>Note that most SSDs can still use SATA cables. This is just slightly slower than NVMe cables.

Each bus uses a different protocol and format for sending and receiving data, as well as a different speed.

Each **device bus** communicates with the CPU through the **system bus** and interrupts.
![[device_system_buses.png]]
## Device and Disk Scheduling
The device manager schedules I/O activities in a way to maximise system performance. What we mean when talking about this is scheduling the amount of time each device, including disks, spends on each request/process.

It wants to:
- Minimise time wasted by moving the HDD read/write head
- Prioritise I/O requests depending on process
- Ensure each process has fair access to disks
- Guarantee that important requests are met before their deadline (in real time systems)
- Minimise the overall wait time for processes in the **blocked** state

Each disk has an I/O queue, and the scheduler can reorder these based on policy. There are a number of different policies such as:
- First Come First Served
- Shortest Seek First
- Elevator Algorithm
- Completely Fair Queueing
- Anticipatory Scheduling

How first come first served works is in the name, so I will skip that one but quickly go over all of the other options.
### Shortest Seek First
This is a scheduling policy that always schedules I/O so that the operation closest to the current position of the HDD read/write head is performed.

This minimises the amount of time that the read/write head has to move but has no benefit on non-HDD devices.

This policy can also cause problems since, if many operations are requested close to the current position of the read/write head, then an operation that was requested a while ago may stall or never execute.
### Elevator Algorithm
The elevator algorithm is a version of the "Shortest Seek First" policy which functions similar to the way an elevator in a building works.

In this algorithm, the next operation which will be performed is chosen based on both the **distance** from the current position, as well as the current direction that the head is moving in. 

So if the head is moving to the other side of the disk to perform, and an I/O operation is requested that is closer, but still in the same direction, it will stop on the way. If an operation was requested which is closer than the current requested operation, but in the other direction, then it will continue to the further one first before changing direction.

This algorithm stops the read/write head "wiggling" inside, and ensures that every operation will be seen too without losing many of the benefits of the "shortest seek first" policy.
### Completely Fair Queueing
Completely fair Queueing works similarly to the [[Lecture 10 - Priority Scheduling & Round Robin|round robin]] method of process scheduling.

Each process places it's IO requests into a queue. Every process has it's own unique queue.

The system them services each queue for a specific time-slice, before cycling to a queue for a different process. Processes may have different **priorities** which will be taken into account.

In HDD drives, this can cause a lot of extra movement of the read/write head since it will jump between the different physical locations that different processes want to perform their I/O. For SSDs this is not an issue.

This policy ensures that every process gets equal access to each device, and ensures that no process gets completely blocked/stuck for long.
### Anticipatory Scheduling
A single process usually deals with locations on disk which are close to each other. 

Processes often want to deal with data (perform some calculations etc.) read from the disk before issuing another request. If, while they are dealing with this data, a different process requests some I/O at a point far away from the head's current position, the read write head will be moved away before having to return to perform the follow up request.

This leads to moving the read/write head more than necessary. Anticipatory scheduling freezes for a short time (milliseconds) after completing a request. This can decrease the amount of movement required for the read/write head, increasing efficiency.
## Buffering
Consider a program that reads a file stored on disk character by character. Accessing the disk each time you want to read another character is very slow. Every time the **device manager** would need to communicate with the **file manager** to access the file on the disk, and (if a HDD disk) the read/write head needs to physically move for each request.

To get around these inefficiencies, most operating systems use a **buffer**, an area of main memory where a whole chunk of data from disk is read to.

The chunk would be read on the program's first read request, and subsequent read requests would then read from the buffer instead of the disk. Once the buffer is empty, another chunk would be read. This lets us use fewer, large requests instead of many small ones, which is much more efficient.

Buffers can also be used to **write** data to a file. When this is done, each character (or just unit of data) is written to the buffer first and then, when the buffer is full, the whole buffer is written to disk in a single operation.

When using buffer's to write data there is danger of losing data (since RAM is volatile). A program can use the system call `fflush` to immediately write the buffer disk.

Some systems use **double buffering**. This is when one buffer is being read to/written from by disk while another is being filled or emptied by a program. Having two buffers increases efficiency, since we can swap between them minimising downtime.

Buffering can happen at many levels of abstraction:
- Software programs
- Library Subroutines
- Operating Systems
- Hardware (for example, a memory buffer built into the drive itself)

Buffering can cause some inconsistency issues. The data on disk may not match exactly what the system thinks it wrote. Because of this, it's important to flush buffers regularly via `fflush` or a timer in the device controller.
### Spooling
Spooling is a specific type of **buffer** used for devices which are **non-shareable**. For example, a printer is **non-sharable** since it can only print one document at a time, despite (usually) being available to multiple systems.

Non-sharable devices use a **daemon process** called a **spooler** name after the idea of spooling tape from a reel.

>Spool has a since been made an acronym "Simultaneous Peripheral Operations On Line", which you may find useful to remember but is a bit silly.

When processes send their requests to the printer (or other non-shareable device), they actually send it to this **spooler daemon** which creates a temporary file for each process. The request data is written into the file.

This means we never have to worry about if the device is available, since the daemon (and it's files) are always available. When the device becomes available, the spooler sends the data for a request to the device.

Spooler daemon's can have their own policy about how they choose which files to send the data from. Usually some kind of priority queue.
## Direct Memory Access
Some hardware devices can access main memory without the CPU. This is know as **direct memory access** (DMA).

In DMA the CPU initiates the read or write operation, before the **DMA Controller** (see below) completes it. The CPU will continue to run other processes while the transfer is happening, and receives an interrupt after the transfer is complete. This obviously increases performance by allowing the CPU more time to work.

It's worth noting that the system bus is still tied up during this transfer, but the CPU can still get on with things that don't involve accessing the bus.

 A **DMA Controller** is required for DMA. This is a hardware component of the system which liaises with both the CPU and the device controller. 

It has it's own registers:
- Memory Address Register (MAR)
- Byte Counter
- Control Register
- etc.

The CPU loads these registers with the device address, and transfer details, before the DMA controller carries out the data transfer in the background.

Transfers happen via the system bus in **burst**, **cycle stealing** or **transparent** mode.

In **burst mode** the system bus does the whole transfer in a single burst. Since the system bus is tied up during the transfer, this can cause problems. When using burst mode, large transfers prevent the CPU from being able to access the system bus for a long time.

In **cycle-stealing mode**, every few clock cycles the CPU will wait and allow the system bus to be used for the transfer. This is better than **burst mode** since it prevents total locking, but we can still do better since we don't want to hold up the CPU.

In **transparent mode**, the DMA controller monitors the system bus and only lets the transfer happen while the system bus is not in use by the CPU. If the CPU suddenly needs the bus for something while the transfer is taking place, then the DMA controller will pause the transfer. This is the best option since it doesn't lock the CPU and doesn't steal cycles from it.

Below you can see a diagram of how these different components interact for DMA
![[dma.png]]
## Devices in Linux
Remember that Linux treats everything like a file.

Linux creates a virtual file in the `/dev` directory for every device in the system. These devices (to processes and programs) appear to be simple files or steams.

This lets us use these devices in programming through standard file handling system calls.

When a device is enabled, the device driver requests an entry in the file system.

Linux uses the `devtmpfs` virtual disk format with the `udev` device manager.

Some pseudo-devices are also created with specific purposes. You can see the table below for more information.
![[pseudo-devices.png]]

The files which represent devices in Linux start with specific letters depending on which device it is. For example:
- `lp` - printer
- `sd` - disk
- `pp` - parallel port
- `tty` - terminal
- `pty` - pseudo-terminal (pipes between processes)
- etc.

Below you can see how some of these show up when using the `ls` command in a terminal. 
![[device_files_ls.png]]