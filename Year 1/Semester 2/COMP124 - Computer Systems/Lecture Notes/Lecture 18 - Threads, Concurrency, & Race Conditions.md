## Threads
A thread is like a process inside of a process. A process can have many threads which can executed independently from, and **in parallel to**, the other threads which make up the process.

In most systems, the kernel isn't involved in the context switching of individual threads. This is handled at a higher level within the process that the threads belong to.

For example, threads in a Java program are handled by the Java Virtual Machine whenever its process is running. Threads like these are called **user-level threads**. 

Threads are very important for even driven programs, especially programs with a GUI.

Within a process all threads share:
- The address space/process image
- Any static data
- The heap
- Instructions (code)
- File descriptors (file handles)
- Global variables
- Child processes
- Statistics in the process control block

Although each thread has it's own:
- Instruction pointer
- Register values
- Stack

You can see an figure depicting this in memory below
![[multi-thread-memory.png]]

Threads usually serve a specific purpose which helps the main process perform its task.

For example a web browser
- Uses one thread for retrieving data from the internet
- Uses another thread to render the website
- Uses another thread to watch for user driven events like keypresses
- etc.

Or a text editor:
- Uses one thread to render the text of the screen
- Uses another thread to handle user input
- Uses another thread to perform spellchecking
- etc.

There are some significant benefits to using threads:
- **Modularity** - It's easier to create a single thread for each activity then one linear piece of code
- **Responsiveness** - Your program can continue to run even if a single thread is blocked
- **Resource Sharing** - Threads can share memory and resources of the process they belong to. When sharing resources it is important to handle concurrency properly (see below)
- **Economy** - Threads are easy to create and switch between because they are allocated and managed within a running process
- **Parallel execution** - Each thread can be physically running at the same if the CPU has multiple cores, although concurrent programming can cause some issues
## Concurrent Programming
Take the quadratic formula below
$$
x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$
If we asked a programming language to calculate this in a single thread it would do so by calculating each step one after the other following the standard BIDMAS rules.

If we used a multi-threaded program to evaluate this we can split the the equation into two types of operation:
- **Concurrent operations** - They do not rely on any other operations and therefore can be run in parallel
- **Serial operation** - These do rely on other operations, and therefore must wait for them to happen before they can be executed.

If split up like this we can reduce the total amount of time required to run a program by running all the concurrent operations at the same time before following with the serial operations.

Below you can see a figure illustrating which operations are concurrent and which are serial for the quadratic formula.

![[concurrent_vs_serial.png]]

We can see that this has 4 concurrent operations, and 5 serial operations.

In a single threaded program, this would take 9 units of time total to run all the operations in sequence.

In a multithreaded program with at least 4 cores the four concurrent operations can all be performed in the same unit of time, before the serial operations are run in 5 units of time afterwards.

This means that, by using multithreaded programs, we can decrease the time taken to do this from **9 units** to **6 units**.

>Stuart was talking about the type of exam questions we could get on this, and he said that we could be asked to determine how many units of time we can get a program down to by executing instructions concurrently. 
>
>This mainly just requires determining which operations are independent and which operations depend on other operations. If $x$ is the number of independent operations and $y$ is the number of dependant operations (and the first of these depends on an independent operation), the minimal time for these are $x+y$ units of time.

A good compiler will try to identify concurrent instructions and assign them to different CPU cores.
## Threads in Java
Each Java program runs in its own heavyweight process. The `main` method runs in one lightweight thread and the JVM starts other threads for garbage collection, event handling, rendering etc.

The programmer can spawn new threads in a java program by extending the `Thread` class which has the signature
```java
public class Thread extends Object implements Runnable
```

The `Runnable` interface defines a `run()` method which the programmer must implement. This code does not start executing until the main program requests it by **creating an instance** of the thread and calling its `start()` method.

Threads are handled internally the JVM. Everything the JVM process gets access to the CPU it decides which thread to run, including its own. It has its own internal thread scheduling algorithm which is similar to round robin.

For example take the code below
```java
class MyWorker extends Thread { 
	public void run() { 
		System.out.println(“I am a worker thread”); 
	} 
} 

public class MyMain { 
	public static void main (String[] args) { 
		MyWorker runner = new MyWorker();
		runner.start(); 
		System.out.println(“I am the main thread”); 
	} 
}
```

Consider the order in which the statements will print to the terminal. Which statement prints first?

The answer here is that it depends. You would expect the worker thread to output first because it is called first but, since the threads run concurrently, if the worker thread is slow to start then the main thread could run first.

>In practice, when I tested this code, the main thread printed first every time. I think that is because of the time taken to allocate the memory for the thread.

Since `MyWorker` extends `Thread` it must implement the `Runnable` interface, meaning they have to define a `run()` method which contains the code for the thread.

In the main program, we need to create a new object of type `MyWorker` and call it's start method.

The `start()` method of a `Thread` object tells the JVM to allocate memory for the new `Thread` object before calling it's `run()` method.

After calling the `start()` method, both the main thread and the worker thread are running in parallel.

Threads in java have a number of states they can be in:
- Each thread begins in the `new` state when its object is first allocated memory. 
- It moves to the `runnable` state when it's `start()` method is called. It still may not run immediately depending on the **JVM thread scheduler**.
- It moves to the `blocked` state when its `sleep()` method is called or when it's waiting for I/O.
- It moves to the `dead` state when it has terminated and is waiting for the JVM to clean up its memory via garbage collection.

You can see the lifecycle of a thread below

![[thread_life.png]]
## Synchronisation Problems
Consider this thread object with a constructor that sets two internal character variables
```java
class TwoChar extends Thread { 
	private char out1, out2; 
	
	public TwoChar(char first, char second) { 
		out1 = first; 
		out2 = second; 
	} 
	
	public void run() { 
		System.out.print(out1); 
		System.out.print(out2); 
	} 
}
```

When this thread runs it will print `ou1` and `out2` in the same order. 

Consider the class below which, in its `main` method, starts two different instances of this thread using different characters.
```java
public class ThreadExample { 
	public static void main(String[] args) { 
		TwoChar tc1 = new TwoChar(‘A’, ‘B’); 
		TwoChar tc2 = new TwoChar(‘1’, ‘2’);
		
		tc1.start(); 
		tc2.start(); 
	} 
}
```

Since the threads run concurrently, we have no clue which one will run first. This means that our output could be any of the following:
- `AB12`
- `A1B2`
- `A12B`
- `1AB2`
- `12AB`
- `1A2B`

`A` will always precede `B` and `1` will always precede `2` but we cannot be sure of the order aside from that.

We would probably see `AB12` the most often because of the order in which the threads are started, but that is not guaranteed. 
### Shared Variables
Suppose we have an object that can be shared by multiple threads
```java
class Something {
	private int num;
	
	public Something() {
		num = 0;
	}
	
	public void increase() {
		num = num + 1;
	}
}
```

This object is then passed into the constructor of two threads
```java
Something thing = new Something();
MyThread t1 = new MyThread(thing);
MyThread t2 = new MyThread(thing);
```

At some point during the program execution both threads access the shared object and perform
```java
thing.increase();
```

The problem is that we can't guarantee that both increases will happen. This is because of thread scheduling.

Since threads can be executed concurrently the line
```java
num = num + 1
```
could be executed at the same time. 

This line does 3 things:
1. Retrieves the current value of `num`
2. Increments the value by 1
3. Stores that new value in the same location

At the assembly level this is what happens
```assembly
mov eax, num
inc eax
mov num, eax
```

If step 1 occurs in both threads at the same time, then they will both increment the same value by one and then save the same value in that location. This means that, despite `thing.increase();` being called twice, `num` is only incremented once.

This is called a **race condition** and is very hard to debug or notice.
### Critical Regions
A race condition can happen whenever a variable is shared between multiple threads. Most of the time it won't happen because the threads are not interrupted but it would be very bad programming to ignore the times when it will happen.

We say any process/thread is accessing a shared resource that its code is in a **critical region** or **critical section**.

We need to ensure that only one thread or process can access the resource at any given time. The programmer must then somehow lock the resource so that the thread currently using it gets exclusive access. Other threads must then wait for the resource to be unlocked before they can use it.

The way we lock threads is through something called **semaphores** or **tokens**. The concept of these originates from single track railways in the 1800s.

Essentially a train can only enter a single track if the driver picks up a physical token. Only one token exists so only one train can be on the track. The driver then leaves the token at the other end when they have passed the single track.

Programming semaphores were proposed by `Dijkstra` in the 1960s. Essentially a critical region of code is like a single track railway. The thread must acquire the semaphore before it can enter the region, causing other threads to block until the semaphore becomes available.

Semaphores require careful programming. A programmer must consider how each shared resource will be used by each thread, and critical regions must be kept as small as possible to stop threads from blocking each other frequently.

More on semaphores will be covered [[Lecture 19 - Producer-Consumer Problem & Semaphores|next lecture]].

