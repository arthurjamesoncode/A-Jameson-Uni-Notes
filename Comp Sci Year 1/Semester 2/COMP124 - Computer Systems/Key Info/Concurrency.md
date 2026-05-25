---
cssclasses:
  - flashcards
---

## Threads
### What is a thread?
A thread is like a lightweight process inside of a normal process. Threads can be executed independently from, and in parallel to, other threads.
### Who handles the context switching of individual threads?
It's handled within the process that the threads belong to.
### What do threads within the same process share?
They share:
- The address space/process image
- Static data
- The heap
- The code
- File descriptors
- Global variables
- Child processes
- PCB
### What is unique to each thread?
- The instruction pointer
- The register values
- The stack
### What are the benefits of using threads?
- **Modularity** - It's easier to create a single thread for each activity then one linear piece of code
- **Responsiveness** - Your program can continue to run even if a single thread is blocked
- **Resource Sharing** - Threads can share memory and resources of the process they belong to. When sharing resources it is important to handle concurrency properly (see below)
- **Economy** - Threads are easy to create and switch between because they are allocated and managed within a running process
- **Parallel execution** - Each thread can be physically running at the same if the CPU has multiple cores, although concurrent programming can cause some issues
### How do you calculate how much time a concurrent program will take to execute?
You can calculate the time by identifying which operations are independent and which operations are dependent.

The independent operations can run in parallel, but the dependent operations must wait for their precursor to have been performed before they can be.
### How do you write threads in java?
Threads in java are objects which extend `Thread`. They must include a `run()` method which includes the code they will run.
### What is the signature of the java `Thread` class?
```java
public class Thread extends Object implements Runnable
```
The runnable interface is what forces any thread we make to have a `run()` method.
### How do we start a new thread in java?
Construct it using the `new` keyword and then call its `start()` method.
### What states can java threads be in?
- new - start of life
- runnable - after `start()` is called
- blocked - `sleep()` is called or it is waiting for I/O
- dead - terminated
### What is a race condition?
A race condition is when a piece of code has a different effect depending on which order independent threads run a piece of code, or what time they run the piece of code.
### What is a critical region?
A critical region is a segment of code which accesses shared resources.
## Semaphores
### What is a semaphore?
A semaphore (or token) is a way to manage who has access to shared resource. They give access to a resource to only one (or a set number) of processes at a time.
### What functions does a semaphore have, and what names could they have?
The semaphore mechanism provides two operations:
- `wait()`
- `signal()`

These two functions go by many different names including:
- `P` and `V`
- `test` and `inc`
- `up` and `down`
### What does `wait()` do?
When a thread calls `wait()` they either:
- Obtain the lock to the semaphore and execute
- Block if the semaphore is already being used by something else
### What does `signal()` do?
When a thread calls signal (just before it leaves a critical region) it releases the semaphore and tells any other blocked thread that the region is now safe to enter
### What is the producer consumer problem?
The problem is as follows:
- The producer and consumer are separate threads with different roles.
- Both the producer and the consumer require access to a shared resource.
- There could be multiple producers and/or multiple consumers accessing the same resources.
### What does the `volatile` keyword do in Java?
It stops a variable being cached, meaning that the latest value will always be used.
### What is busy waiting or spinlock and its pros/cons?
Spinlock is when a process runs a bit of code which does nothing repeatedly until some condition is met.

**Spinlock** works well at preventing threads from accessing the same resource, but is inefficient since it wastes CPU cycles performing empty instructions. It should only be used if the expected wait time is very short.
### What does `Thread.yield()` do?
**Spinlock** works well at preventing threads from accessing the same resource, but is inefficient since it wastes CPU cycles performing empty instructions. It should only be used if the expected wait time is very short.

The JVM can ignore the request to block so we still need to put this in a spinlock to ensure the code won't run. Including the `yield()` should at least decrease the amount of wasted cycles.
### What does the `synchronized` keyword do?
`synchronized` indicates that a method contains critical regions. When a thread calls a `synchronized` method it gets exclusive control to the lock.

Other calls to the objects critical methods block and go into an entry set.
### What is an entry set?
A set of threads which want to **enter** a critical region.
### What methods does java provide for semaphores?
Java provides the methods:
- `wait()` 
- `notify()` (renamed `signal()`)

A call to `wait()` suspends the current thread and moves it to the **wait set**. 

A call to `notify()` moves an arbitrary thread from the wait set to the **entry set**.
### What does `notifyAll()` do?
You can also call `notifyAll()` to allow all threads in the wait set to compete for the chance to resume. The winner is the one which calls a synchronized method first.
### Why are these methods preferred to `Thread.yield()`
These are preferred to `Thread.yield()` since they don't depend on the version of the JVM you are running.
### How do we create a Java `Semaphore` object?
We create a semaphore object by using the `new` keyword and passing in the number of "permits" the semaphore can have. For example
```java
Semaphore sem = new Semaphore(1);
```
Creates a new semaphore with 1 permit.

The number of permits is the number of processes/threads which can access the resource at any one time.
### What methods do java semaphores have, and what do these methods do?
When the `acquire()` method is called:
- If the counter is 0 the thread will block (added to a **wait queue**)
- If the counter is greater than 0, the counter is decreased and the thread can continue

When the `release()` method is called:
- The counter is increased
- The first blocked thread in the wait queue can acquire the permit
### How do we avoid race conditions?
Testing and setting the counter must be **atomic** (single/non-compound) operations to avoid race conditions.
## Deadlock
### What is the dining philosopher's problem?
"There are $N$ philosophers sitting around a table. Each philosopher switches between two actions: **eating** and **thinking**.

The philosophers don't require any resources to think, but they need **two** chopsticks to eat.

There are exactly $N$ chopsticks. One between each philosopher. If a philosopher wants to eat they must wait for both neighbours to stop eating."

In this context, we can view the philosophers as threads/processes and the chopsticks as shared resources.
### What is starvation?
Starvation, in this context, is when a thread/process cannot continue because it requires access to a shared resource which is continually tied up by other processes.
### What is deadlock?
Deadlock is when multiple processes cannot continue because they are all waiting for one of the other process to release a shared resource.
### What resources could deadlock occur over?
- CPU
- Devices
- Memory
- Files

In practice CPU interrupts stop deadlock happening over the CPU.
### What strategies are there to deal with deadlock?
Is it up to the OS to either:
- Prevent deadlock
- Detect deadlock
- Avoid deadlock
- Ignore deadlock
### What ways are there to prevent deadlock and what are their problems?
The methods are:
1. Force processes to claim all resources in one atomic operation
2. Number each resource and force processes to claim then in a specific order
3. Force processes to only use one resource at a time

The problem with 1 are:
- If a specific resource is used a long time after the first required resource it will be underutilised
- It's not always possible for a process to know what resource it will need in the future

The problems with 2 are:
- If Y is needed by a process before X is this leads to X being underutilised.
- Keeping track of and ordering all shared resources is an intensive task.

The problem with 3 is that, in modern systems, it's unrealistic to assume that each process only needs one resource at a time.
### What is a resource allocation graph (RAG)?
A graph that shows which resources are currently used by which processes.
### What does it mean if there is a cycle in the RAG?
It means there is a chance that deadlock could occur. If there is no cycle deadlock is impossible.
### In deadlock detection, how often would you check the RAG?
Monitoring the graph and checking for cycles is expensive to do for every request, so it would only be done every so often or when CPU usage deteriorates.
### What could the OS do if detecting a cycle?
- Take an existing resource away from a process to remove the cycle (**pre-emption**)
- Kill one or more processes
- Roll back to a previous state (this requires the OS to store checkpoints of process states)
### What are the problems with these recovery methods?
All of these recovery methods involve losing efficiency or even data:
- Rollbacks involve running previous instructions again in a different order
- Memory would be required to store data
- Calculations and read/write operations would need to be undone and redone
### What is deadlock avoidance and its problems?
Deadlock avoidance means that the system never grants access to a resource if it would cause deadlock.

Its problems are:
- Processes must declare up front what resources they will be using (they might not know this)
- This can force processes to wait unnecessarily as deadlock is rare
### What is the bankers algorithm?
The bankers algorithm is a theoretical approach to deadlock avoidance created by Dijkstra:
- It needs to know in advance what resources a process will request
- Determines whether a static collection of processes is in a **safe** or **unsafe** state.
- Guarantees that all processes will terminate but does not care about how long this takes.
### Why doesn't the banker's algorithm work in practice?
- New processes arrive all the time
- Processes don't necessarily know which resources they need
- We cannot force processes to wait for an indefinite time on the promise of the other processes eventually terminating
### What is the ostrich algorithm?
To bury your head in the sand and pretend nothing is wrong.
### Why is deadlock ignored by most OSs?
Preventing or detecting deadlock is expensive and adds a lot of complexity. However deadlock is pretty rare and so the most cost-effective solution is to just let it happen, and reboot the system when it happens.