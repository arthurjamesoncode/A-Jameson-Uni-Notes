## Paging Memory Model
The paging memory model splits the physical memory into equal sized blocks. The address space for each block is then spread across as many pages as necessary. This functions similar to how files are stored in blocks on a disk.

The **process memory addresses** will appear to be one contiguous range, with **logical addresses** numbered from 0 to $N$ where $N$ is the process limit. In reality they are spread over multiple different **pages**.

Pages can be anywhere in memory, they do not need to be consecutive. The physical memory used by a page is called the **page frame**.

Each process has a page table that maps **logical pages** onto **physical memory frames**. This is stored in memory as part of the process image. The address of the page table for the current process is stored in the page table base register in the CPU.

Below you can see a figure illustrating how the **virtual addresses** could map to the physical memory.

![[page_mapping.png]]

### Page Table Lookups
Consider the figure below. It shows the **logical address space** of a process split into 4 pages.

![[logical_pages.png]]

Now using a **virtual address** and the **page table** for this process we can find the physical memory location for the corresponding instruction/data.

The virtual address is split into 2 parts, which may or may not be of equal size. 
- The high/most significant part (leftmost part) stores an index to the page table (zero-indexed). The corresponding memory location indicates the index of the physical page frame. 
- The small/least significant part (rightmost part) indicates the offset into the **page frame**. Adding this to the start of the page gives us the required **physical location**.

So for a virtual address of `00010011` where 4 bits are used for both halves, we can see that
- `0001=1` is the index of the page. This means it would be the second page since the pages/page table are zero-indexed. The corresponding value in the page table is the index of the physical page frame
- `0011=3` is the offset into the page frame.

Below you can a figure illustrating this.

![[page_table_mapping.png]]

>Stuart started to talk about what an exam question on this would look like. 
>
>He said that you would not be given a diagram, but would be given virtual address, a breakdown of which part shows page and which part shows the page offset. You would then be asked to show which memory address is pointed to.
## Segmentation VS Paging
Segmentation and paging are two ways to reduce the size of a process in working memory. While similar ideas with similar goals they do have some pretty big differences.

For segmentation:
- It is a logical division of the address space
- Segments can be different sizes
- The segments match the structure of the program

For paging:
- It is a physical division of the address space
- Each page is always the same size
- Pages have no relation to the program structure

In modern systems, paging is used much more often than segmentation this is because of two main reasons:
- Memory allocation is much easier since all the pages have the same size.
- Fragmentation is eliminated, although there is some wasted space in the final page of a process.

The Intel x86 MMU supports segmentation and paging at the same time. This works by splitting process memory into logical segments and then storing these segments inside pages. Everything we learnt about segmentation [[Lecture 16 - Memory Manager, Addresses, & Segmentation#Segmentation|last lecture]] still applies, just within a paged memory layout.

Below you can see a figure about what the CPU must do when given a logical address
![[segmented_paging.png]]
The CPU must do this every time an instruction needs to access memory.
## Page Swapping
A big advantage of pages, like segmentation, is that the OS can allocate more memory than is physically installed in the system. It can do this because only pages which are being used by the current process need to be in memory.

This means we can utilise **page swapping**. This is the same as **process swapping** described [[Lecture 16 - Memory Manager, Addresses, & Segmentation#Swapping|last lecture]], but instead of swapping out whole processes the CPU only swaps out pages.

Pages not being used by the current process are stored on disk, in the **swap space**. This means that the system can have as many processes as it likes in the round-robin queue.

However, the OS doesn't know which pages will be needed at any given time so we need to know:
- What happens if a process tries to access a page which is not in main memory?
- How can the system try and predict which pages it will need?

If a process tries to access a page which is not in memory a **page fault** occurs. A page fault is **NOT** an error since it is intended and does not alter or stop the execution of a program.

Every page fault generates an **interrupt** which is then caught by the interrupt handler. The correct page is loaded/swapped from disk into main memory. 

This is called **demand paging** meaning that pages are brought in when needed. Other systems use **anticipatory paging** meaning that they bring in more pages than currently needed.
### Page Replacement Problem
When we bring a page from disk into memory we may need to remove a page from memory. We now have a problem of "How do we decide which page to remove?".

Each OS has a page replacement policy:
- **Least Recently Used** (LRU) - Remove the page that has been unused for the longest time
- **First In First Out** (FIFO) - Remove the page that has been in memory the longest
- **Least Frequently Used** (LFU) - Remove the page which has the fewest references in a recent period
- **Second chance** - Works like FIFO but keeps pages that were recently used.

The optimal policy would be "Longest Forward Distance (LFD)" which we implemented a version of as part of our COMP108 programming assignment. Essentially it removes the page which will have the longest time before it is requested again.

The problem with LFD is that the memory manager cannot see the future. It can only make a sensible guess based on the history of which pages are requested and what the process history is.

If the MMU is wrong it isn't a huge problem. There is just a slight decrease in speed and leads to some disk thrashing as pages are added and removed. The program will still run as expected. Though obviously we still want to minimise any performance loss with our choice of policy.
### The Principle of Locality
We have a goal of selecting the optimal page-replacement policy. Since LFD is optimal but impossible, we want to try and **approximate LFD**. This means that we need some way to predict which page won't be needed for the longest time.

Since we can't see the future requests, we can use the **principle of locality** as a guide.

The principle of locality states that: "Over any short period of time, a process's memory references tend to be spatially localised"

Essentially, memory addresses that we will want to use soon are likely to be close to the addresses we are currently using.

The principle of locality is an approximation, not a rule, so we never guarantee that all needed pages would be in working memory. This means that page faults are entirely normal part of page-replacement.

Following from this principle we can recognise:
- Instructions don't usually jump all over the place
- Code inside a loop usually works in the same area of memory
- Accessing an array or other data structure will be focused on the same memory area

Generally execution stays within roughly 20% of a process's pages for 80% of the time it runs. We can use this to try and estimate the **working set** of our process.
### The Working Set
The working set of a process is defined as the set of pages $W(T, s)$ used in the time period from $T$ to $T+s$ inclusive. For simplicity, in this module time periods are not specified in units. 

This is a set of between $1$ and $s+1$ pages. If there is only 1 page in the set it is the only one used over the entire time period $T$ to $T+s$. If there are $s+1$ pages in the set it means a unique page is referenced every unit of time from $T$ to $T+s$.

For example $W(12, 4)$ is the working set of pages used by a process in the time period from 12 to 16 inclusive.

The MMU knows which pages have been used in which time periods. You can imagine a table like the one below.

![[pages_by_time.png]]

This lets us see the working set for a given time. For example the working set $W(3,3)$ is $\{a, z\}$ since $a$ is used at times $3, 4,$ and $5$ and $z$ is used at time $7$.

By the principle of locality we know that the working set for the next period of time is likely to be similar to the working set for the current period of time. That means that, for each process, memory manger tries to predict the next working set by using the same set used in the previous period. 

This means that the MMU would predict the working set $W(x, y)$ by looking at $W(x-y-1, y)$.

Taking the same table above, we can see that the MMU would try to predict $W(10, 2)$ by looking at $W(7, 2)$. Since $W(7, 2)$ is $\{a, b\}$ then the **predicted working set** $W(10, 2)$ is also $\{a, b\}$

>Again Stuart has started to talk about the exam questions on this topic. 
>
>He says that there are 2 possible questions: "What is the working set $W(x,y)$" and "What is the predicted working set $W(x, y)$?"

How accurate the working set is depends on its size:
- If the set is too small it won't cover the entire locality for the current process
- If the set is too big it will cover several localities and result in redundant page swapping

The working set of a process also changes as its execution moves from one locality to another (different subroutine, data structures, etc.). When this happens the number of page faults will increase during the transition. This is an expected part of how memory management works.
## Page Size
The page size that a system uses has an effect on how the system will work, and how much space is wasted.

The last page of a process is pretty much never entirely full. On average, a system will lose about 50% of a page due to internal fragmentation. This means that the size of the pages affect how much memory is wasted per process.

Large pages don't need as large a page table but increase the amount of wasted memory.

Smaller pages make better use of memory and have less internal fragmentation, but they increase the chance of **page faults** since it is more likely that the required code/data are in a different page.

In both Windows and Linux the page size is 4KB by default.
## Cache Memory
The further we get from the CPU the slower it is to access different types of storage:
- The fastest parts of the system are the registers inside the CPU itself
- The slowest parts are the disk drives
- RAM/Main memory is slow compared to registers but very quick compared to any disk
The reason we use these slower parts rather than just relying on the faster CPU storage, or main memory is that that the slower forms of storage are also much cheaper.

What this means is that we can increase speed by keeping things as close to the CPU as possible. One way of doing this is using the CPU cache.

The CPU cache:
- Is slower to access than the CPU registers
- Is faster to access than main memory
- Is stored inside the CPU itself
- Contains copies of items in main memory
This lets us access these copies of main memory items much more quickly. This is really useful if we are only using a couple of pages.

>There are many forms of caches at different levels of abstraction, they aren't limited to just a CPU cache. For example you may cache results of a database query from a remote machine on the SSD of a local machine. 
>
>The main concept of a cache is to temporarily store results of a more expensive operation in a less expensive place to access them repeatedly.

When the CPU requests data from memory it first checks the cache. If the data is in the cache it is a **cache hit** and the CPU can immediately read the data from the cached copy. This is extremely fast in this case.

If the data is not in the cache it is a **cache miss**. When this happens the MMU copies a data block from main memory into the cache. This is obviously slower than if there is a cache hit.

The block includes the memory location around the requested address. The CPU can then read the data from this cached version. By the principle of locality, it is likely that future data items were brought into the cache as part of the block, thus increasing the chance of cache hits.

A modern CPU can execute hundreds of instructions in the time it takes to place a single block from main memory into the cache. We call this time **latency**. Larger caches have better hit rates but longer latency.

Modern CPUs have multiple levels of caches:
- L1 Cache - Small and fast cache close to the CPU registers
- L2 Cache - Slightly bigger and slower cache compared to L1
- L3 Cache - Bigger and slower cache compared to L2

In multi-core processors:
- Each core has its own L1 cache
- Each pair of cores share an L2 cache
- All cores share an L3 cache

You can see a figure below which depicts the full storage hierarchy
![[memory_hierarchy.png]]