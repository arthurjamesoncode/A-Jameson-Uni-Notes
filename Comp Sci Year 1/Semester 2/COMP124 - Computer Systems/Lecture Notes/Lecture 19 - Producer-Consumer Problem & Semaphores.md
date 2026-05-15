## Semaphore Notation
The semaphore mechanism provides two operations:
- `wait()`
- `signal()`

These two functions go by many different names including:
- `P` and `V`
- `test` and `inc`
- `up` and `down`

Java has its own words for these functions and this will be covered below.

In this note we will implement a simple boolean semaphore over the course of the lecture.

A thread must call `wait()` before it enters a critical region. This blocks the thread is the region/semaphore is in use be another thread. Otherwise the thread obtains the lock and can enter the critical region.

The thread must call `signal()` just before it exits the critical region. This releases (unlocks) the semaphore and notifies any other blocked thread that the region is now safe to enter. If multiple threads are waiting, only one will successfully enter and the rest must wait for another `signal()` call.
## Producer Consumer Problem
The producer-consumer problem is a good way to illustrate how semaphores work.

The problem is as follows:
- The producer and consumer are separate threads with different roles.
- Both the producer and the consumer require access to a shared resource.
- There could be multiple producers and/or multiple consumers accessing the same resources.

For example in a bakery:
- The baker makes a cupcake (producer)
- They put the cupcake in a box (shared resource)
- A diner takes the cupcake from the box and eats it (consumer)

Threads are usually producers or consumers of some resource. The resource would be a shared variable or object represented (in Java) by a class.
## Buffer - Attempt 1
Let's model this problem as two threads trying to access a buffer. 

Importantly:
- The producer cannot insert if the buffer is full
- The consumer cannot remove if the buffer is empty
- The buffer cannot be accessed by multiple producers or consumers at the same time

Consider the following code for the `Buffer` object, the `Producer` object and the `Consumer` object
```java
class Buffer {
	private int store;
	
	public void insert(int item) {
		store = item;
	}
	
	public int remove() {
		return store;
	}
}

class Producer extends Thread {
	private Buffer buff;
	
	public Producer (Buffer b) {
		buff = b;
	}
	
	public void run() {
		int m = 0; 
		... //m is possibly redefined
		buff.insert(m);
		...
	}
}

class Consumer extends Thread {
	private Buffer buff;
	
	public Producer (Buffer b) {
		buff = b;
	}
	
	public void run() {
		...
		n = buff.remove();
		...
	}
}
```

The code for the main program creates instances of the buffer, producer and consumer

```java
public class ProdCon {
	public static void main(String[] args) {
		Buffer b = new Buffer();
		Producer p = new Producer(b);
		Consumer c = new Consumer(b);
		p.start();
		c.start();
	}
}
```

All of this code is bad. This is because none of it has protection for the constraints mentioned earlier:
- The producer doesn't check to see if the buffer is full;
- The consumer doesn't check to see if the buffer is empty;
- The buffer is not protected from being used by both threads at the same time.

Surely we can do a bit better.
## Buffer - Attempt 2
If we edit the buffer code a bit we can add some of the protections that we need.
```java
class Buffer {
	private int store;
	private volatile boolean empty = true;
	
	public void insert(int item) {
		while(!empty);
		store = item;
		empty = false;
	}
	
	public int remove() {
		while(empty);
		int item = store; //this line is necessary because the method isn't protected against object lock
		empty = true; 
		return item;
	}
}
```

The `volatile` keyword prevents variables from being cached. This means that the latest value will always be used.

The `while(empty);` and `while(!empty);` statements are an example of **spinlock**, or **busy waiting**.

Essentially an empty loop is run while the buffer is empty or is not empty. These loops only terminate when a separate thread edits the value of `empty`.

**Spinlock** works well at preventing threads from accessing the same resource, but is inefficient since it wastes CPU cycles performing empty instructions. It should only be used if the expected wait time is very short.

An alternative, which may be more efficient, is for the waiting thread to give up control of the CPU. For example the `insert` method could look like
```java
public void insert(int item) {
	while(!empty) {
		Thread.yield();
	}
	store = item;
	empty = false;
} 
```

The `yield()` method tells the JVM that the thread is willing to block, freeing up the CPU. The exact behaviour of `yield()` depends on the installation of JVM on the machine, making this request non-deterministic.

The JVM can ignore the request to block so we still need to put this in a spinlock to ensure the code won't run. Including the `yield()` should at least decrease the amount of wasted cycles.

This is a nice homebrew solution for implementing a simple semaphore, but surely there is something better defined and widely used within Java?
## Buffer - Attempt 3
Java has a special keyword for indicating critical regions. We can use the `synchronized` keyword (American spelling), to indicate a critical region.

```java
class Buffer {
	private int store;
	private volatile boolean empty = true;
	
	public synchronized void insert(int item) {
		while(!empty) Thread.yield;
		store = item;
		empty = false;
	}
	
	public synchronized int remove() {
		while(empty) Thread.yield();
		empty = true; 
		return item; //value now protected by object lock
	}
} 
```

Each Java object has a `lock` associated with it. Locks are **not** shared across multiple instances of the same class. Every object instance has its own lock that works independently.

The `synchronized` keyword declares methods that contain **critical regions**. When a thread calls a synchronized method it get's exclusive control of the lock. Other calls to the object's synchronized methods must block in an **entry set** (set of threads which want to **enter** the critical region).

Non-synchronized methods can still be called without any issues.

When the thread with the lock exits the synchronized method, the lock is released and the JVM will select an arbitrary thread from the entry set which will then perform its call to the synchronized method.

Java provides methods to help with semaphores:
- `wait()` 
- `notify()` (renamed `signal()`)

These methods provide a way to give up the CPU which works regardless of the platform it is run on or the installation of the JVM.

We could implement them in our `insert` method like so
```java
public synchronized void insert (int item) {
	while(!empty) {
		try {
			wait();
		} catch (InterruptedException e) {
			System.out.println(e);
		}
	}
	store = item;
	empty = false;
	norify();
}
```

Note that `wait()` can throw an `InterruptedException` so we must use a try-catch statement to handle this case.

>Exception handling is outside the scope of this module but we have covered in [[Lecture 16 - Exception Handling]] of the COMP122 module.

The call to `wait()` suspends the current thread and moves it to the **wait set**. 

The call to `notify()` moves an arbitrary thread from the wait set to the **entry set**.

You can also call `notifyAll()` to allow all threads in the wait set to compete for the chance to resume. The winner is the one which calls a synchronized method first.

## Java Semaphores
The previous examples show us implementing our own semaphores. However Java provides a `Semaphore` class that we can use instead.

```java
import Java.util.concurrent.Semaphore
```

>You can read in depth about the Java `Semaphore` class [here](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Semaphore.html).

When creating a semaphore you pass an integer `i` to the constructor which specifies how many **permits** the semaphore allows. This is because Java `Semaphore` objects are counting semaphores, meaning that they allow `i` objects to access the resource at once.

Since we want to make sure that our critical regions are only accessed by a single thread at a time, we will pass `1` into the constructor like so
```java
Semaphore sem = new Semaphore(1);
```

When the `acquire()` method is called:
- If the counter is 0 the thread will block (added to a **wait queue**)
- If the counter is greater than 0, the counter is decreased and the thread can continue

When the `release()` method is called:
- The counter is increased
- The first blocked thread in the wait queue can acquire the permit

Testing and setting the counter must be **atomic** (single/non-compound) operations to avoid race conditions.
