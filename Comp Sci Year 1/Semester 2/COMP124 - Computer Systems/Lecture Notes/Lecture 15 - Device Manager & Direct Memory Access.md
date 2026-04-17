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
The device manager schedules I/O activities in a way to maximise system performance. It wants to:
- Minimise time wasted by moving the HDD read/write head
- Prioritise I/O requests depending on process
- Ensure each process has fair access to disks
- Guarantee that important requests are met before their deadline (in real time systems)
- Minimise the overall wait time for processes in the **blocked** state

Each disk has an I/O queue, and the scheduler can reorder these based on policy. There are a number of different policies such as:
- First Come First Served
- Shortest Seek First
- Elevator Algorithm
- Completely Fair Scheduling
- Anticipatory Scheduling

How first come first served works is in the name, so I will skip that one.

