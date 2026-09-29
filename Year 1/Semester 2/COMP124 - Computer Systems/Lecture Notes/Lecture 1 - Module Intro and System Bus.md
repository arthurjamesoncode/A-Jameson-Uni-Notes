## Module Information
This module aims to introduce how computers function at the instruction operational level. This is a much lower level course than most of the other courses in the degree.

It also aims to teach us about the structure and functionality of modern operating systems, and how the operating system connects low level hardware, and high level programs.

Below you see an image which functions as a summary of what we will be learning about in this module.
![[summary_diagram.png]]

**Module Structure:**
• CPU architecture and machine instructions
• Assembly language programming
• Operating system concepts
• Process management
• File and device management
• Memory management
• Concurrent programming
• Compilers and code generation

**Learning Outcomes:**
• LO1: Describe the structure and operation of computer hardware at the register transfer level
• LO2: Understand and reason about simple assembly language algorithms
• LO3: Describe the overall structure and functionality of a modern operating system and its interactions with computer hardware and user processes
• LO4: Explain how modern operating systems and programming languages implement concurrency and the issues that arise when working with concurrent processes
• LO5: Use the Linux command line and describe how files, devices and processes are managed by the Linux kernel

### Module Delivery
The module delivery will be in person via lectures and lab drop-in sessions. There will be a double lecture every Wednesday from 11-13, and a lab drop in session every Monday from 11-13

Everything used to teach the course will be added to canvas every week
- Lecture slides will be published in advance (every Tuesday for the following week)
- Live lecture recordings will be uploaded a few hours after each delivery
- Lab sheets will be uploaded weekly can be worked through in your own time. Labs are not assessed at all in this module.

### Assessments
The module is assessed with one exam during the exam period. There is no coursework or other assessment.

Practice exams will be released on Canvas throughout the semester.

While the lab tasks aren't assessed, some exam questions will be based on things you do in those lab tasks, the rest will be based on the lecture slides along. Attempting labs is beneficial to passing the exam.

The exam will be multiple choice.
## Von Neumann Model
Von Neumann proposed the basic model of a computer system in the 1940s. You can see this model pictured below.
![[von_neumann_model.png]]
This model hasn't changed over time. The specifics (the kind of input devices, the type of memory etc.) have changed but the model itself remains the same.

The **input device** is used to load programs and data into memory (we call this the **stored program concept**).

The **CPU** (central processing unit) fetches program instructions from memory, processes the data, and generates results. These results are then sent to an **output device**.
## Modern Systems
You can see below an image of how modern computer systems work.
![[modern_system.png]]
We will learn about the specifics of all of these bits, but not in extreme detail today.
### CPU
The CPU fetches instructions from main memory and executes them.

These instructions are very basic, (add two values, save a value in a location, etc.)

Different types of CPU have different instruction sets. AMD will have a different set to Intel, which will have a different set to Apple etc.

One benefit of high level languages is that the code can be written once and then can be compiled to run on different processors. It would need to be compiled to run on each separate processor. A compilation which could run on one machine may not work on another.

There are two common types of CPU instruction set
- **CISC** or Complex Instruction Set - Such as Intel x86 and many other desktop/server CPUs.
- **RISC** or Reduced Instruction Set - Such as ARM (smartphones etc)

Code written for a **RISC** won't necessarily take longer to execute but will be longer.

Internal activity of the CPU is synchronised by a fast clock, which we measure in hertz (megahertz, gigahertz). A 3GHz clock will execute 3 billion cycles (or instructions) per second.

CPUs also have multiple cores. This can make programs run much faster but only if it is written in a way that allows the operating system to schedule in a way that can take advantage of the multiple cores.
### System Bus
The bus is a collection of wires which allows communication between the various components on the motherboard.

Using a bus allows us to connect every component to every other one without directly connecting each component to every other component. The latter strategy is called a point-to-point system and is prohibitively complicated and expensive.

A sender places an item (a piece of data) on the bus and the receiver takes it off. 

The bus can have multiple lines
- **Address lines** - which are used to specify a memory address or a device to be accessed
- **Data lines** - which carry the data which needs to be transferred
- **Control lines** - tell the receiver what to do with the data

Almost all modern computers have multiple interconnected system busses, such as SATA, PCIe, USB.

There is a problem of **bus contention** because only one thing can be on each bus at once.
