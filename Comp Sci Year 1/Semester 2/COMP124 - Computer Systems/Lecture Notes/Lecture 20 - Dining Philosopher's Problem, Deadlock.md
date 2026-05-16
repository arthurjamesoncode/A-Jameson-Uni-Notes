## Dining Philosophers Problem
In the Producer-Consumer problem each thread has a distinct role (for example: baker and eater) and the synchronisation environment involves a single shared resource (for example: cake box).

In the Dining Philosophers problem however threads have identical roles and the synchronisation environment has multiple shared resources.

This problem (which will be described formally below) is a great way to visualise two common issues with concurrent systems: **deadlock** and **starvation**.

The OS processes and resources are also affected by these issues.

The Dining Philosophers problem goes as follows:

"There are $N$ philosophers sitting around a table. Each philosopher switches between two actions: **eating** and **thinking**.

The philosophers don't require any resources to think, but they need **two** chopsticks to eat.

There are exactly $N$ chopsticks. One between each philosopher. If a philosopher wants to eat they must wait for both neighbours to stop eating."

You can see the figure below for a visualisation of this problem where $N=5$
![[dining-philosophers.png]]
The blue $P$ circles indicate the philosophers and the red $S$ rectangles indicate the chopsticks.
## Modelling the Problem
Let's give each philosopher a unique index value in the set 
$$
\{0,1,2,3,4\}
$$
and each chopstick an index from the same set.

The philosopher with index $K$ must wait for both chopsticks $K$ and $(K+1)\text{ mod } 5$ to be free.

When one philosopher with index $K$ eats, they block two other philosophers (their neighbours with indexes $K-1$ and $K+1$) from eating.

For example when $P0$ is eating, they are using sticks $S0$ and $S1$ which means that $P1$ and $P4$ cannot eat.

In code, we can treat each chopstick as a shared resource with it's own critical region like so
```java
class Chopstick {
	private volatile boolean using = false;
	
	public synchronized void pickUp() {
		while(using) {
			try {
				wait();
			} catch (InterruptedException e) {
				System.out.println(e);
			}
		}
		using = true;
	}
	
	public synchronized void putDown() {
		using = false;
		notify();
	}
}
```

We  can then model each philosopher  as a thread with a `run()` method
```java
public class Philosopher extends Thread {
	public void run() {
		while (alive) {
			think();
			stick[i].pickUp();
			stick[(i+1) % 5].pickUp();
			eat();
			stick[i].putDown();
			stick[(i+1) % 5].putDown();
		}
	}
} 
```

Each chopstick has a semaphore meaning that no two philosophers can pick it up at the same time:
- If a philosopher needs the stick but it's already in use then move to the wait set.
- When a chopstick is put down, waiting threads are notified and it can be picked up.

There are some pretty big problems with the way we have implemented this. Specifically this can lead to either **starvation** or **deadlock**.
### Starvation
We cannot guarantee the order in which threads will be executed, or whether threads will be interrupted during execution. 

This means it is possible for $P0$ and $P2$ to pick up first, meaning that the others ($P1$, $P3$, $P4$) must wait and cannot eat. 

After $P0$ and $P2$ put down their chopsticks it is possible for them to pick them up again immediately meaning that the others cannot eat again. If this repeats the other processes will starve.

Even without $P0$ and $P2$ constantly eating, if $P0$ and $P2$ take turns to eat, then $P1$ will still starve.

Essentially, without proper controls on when threads can run, some threads could starve. 
### Deadlock
Suppose each philosopher immediately picks up the chopstick to their right. This means that nobody can pick up the chopstick to their left, and therefore no one can start eating.

Since no philosopher ever releases their chopstick every philosopher is stuck in the waiting state indefinitely. This is called **deadlock** or **deadly embrace**.

We can add some rules to the code to prevent deadlock such as:
- Only allow $N-1$ philosophers to pick up any chopsticks at the same time
- Introduce asymmetry, so even indices would pick up the right chopstick first while odd indices pick up the left.
- Ensure that both chopsticks are picked up in one atomic (uninterruptable) operation.
All of these solutions add some complexity to the code.

So far, we have been looking at deadlock through the lens of **threads within a process**, but deadlock can also occur if separate **heavyweight processes** access the same shared resource such as:
- CPU
- Devices
- Memory
- Files

Deadlock occurs in the following situation:
- Process 1 is granted resource X and then requests resource Y
- Process 2 is granted resource Y and then requests resource X
- Both resources cannot be shared
- Both resources cannot be taken away from either process (the resources are **non-preemptible**)

Note that the OS uses interrupts to make certain important shared resources (like the CPU) preemptible. This means that deadlock over things like the CPU won't occur.

Is it up to the OS to either:
- Prevent deadlock
- Detect deadlock
- Avoid deadlock
- Ignore deadlock

We will go over all of these possible approaches over the rest of the lecture.
## Preventing Deadlock
There are a few ways to prevent deadlock:
1. Force processes to claim all resources in one atomic operation
2. Number each resource and force processes to claim then in a specific order
3. Force processes to only use one resource at a time

If we take approach 1, then we must before the process uses any specific resource claim all the resources that the process will need. Although this has some problems:
- If a specific resource is used a long time after the first required resource it will be underutilised
- It's not always possible for a process to know what resource it will need in the future
These too things make this approach difficult/inefficient.

>Stuart says that it claims all resources at the start of the process. I think he's just simplifying it a bit since there is no reason it couldn't run some code that doesn't require the shared resource before claiming all resources after.

If we take approach 2, then we force processes to always claim resources in the same order. So if two processes both need resources X and Y, then they will both try to get resource X first and when only one succeeds the other will wait until X is available before claiming both X and Y. 

This approach also has some problems:
- If Y is needed by a process before X is this leads to X being underutilised.
- Keeping track of and ordering all shared resources is an intensive task.

If we take approach 3, then we would force each process to finish with and release their first claimed resource before they try to claim another. This prevents any process from needlessly hogging a resource.

The biggest problem with this is that it's unrealistic to assume that each process only needs one resource at a time. Considering the philosophers, they need 2 chopsticks or they cannot eat at all.

### Detecting Deadlock
We could draw/maintain a graph which models the processes and resources in a system. We call this a **resource allocation graph**:
- Processes could be represented as circles
- Resource types can be represented as rectangles containing dots
- The dots within the rectangles represent the instances of the resource
- Directed edges show resource requests/assignments. If a resource is assigned to a process it points to that process, and if a process is requesting a resource then it points to that resource.

For example take the graph below
![[resource_allocation_graph.png]]

We can now identify if there is a chance of deadlock by checking for cycles. If there is no cycle there is no chance of deadlock.

The existence of a cycle does not mean there is/will be deadlock, there simply could be deadlock if a request is granted at the wrong time.

So now the graph can be monitored to see if there is a chance of deadlock, and we can then do something to prevent it. Monitoring the graph and checking for cycles is expensive to do for every request, so it would only be done every so often or when CPU usage deteriorates.

If a cycle is created the operating system could:
- Take an existing resource away from a process to remove the cycle (**pre-emption**)
- Kill one or more processes
- Roll back to a previous state (this requires the OS to store checkpoints of process states)

All of these recovery methods involve losing efficiency or even data:
- Rollbacks involve running previous instructions again in a different order
- Memory would be required to store data
- Calculations and read/write operations would need to be undone and redone
## Deadlock Avoidance
Deadlock avoidance is similar to deadlock prevention. The idea is:
- The system never grants access to a resource if it would cause deadlock
- Processes must declare up front what resources they will be using (they might not know this)
This can also force processes to wait unnecessarily as deadlock is rare.

The **banker's algorithm** is a theoretical approach to deadlock avoidance devised by Dijkstra. It needs to know in advance what resources a process will request and determines whether a static collection of processes is in a **safe** or **unsafe** state. It guarantees that all processes will terminate but does not care about how long this takes. 

>The exact steps of this algorithm are not covered in the lecture slides but you can read about it [here](https://en.wikipedia.org/wiki/Banker%27s_algorithm).

In practice this algorithm doesn't work for a few reasons:
- New processes arrive all the time
- Processes don't necessarily know which resources they need
- We cannot force processes to wait for an indefinite time on the promise of the other processes eventually terminating
### Ignoring Deadlock
We have looked at a number of solutions to dealing with deadlock and evaluated all of them as pretty bad.

However there is a solution which is used by both Windows and Linux called the **ostrich algorithm**.

The **ostrich algorithm** is when you stick your head in the sand and pretend that there are no problems. It's a joke name, we just ignore deadlock.

Preventing or detecting deadlock is expensive and adds a lot of complexity. However deadlock is pretty rare and so the most cost-effective solution is to just let it happen, and reboot the system when it happens.

This trades **correctness** for **convenience** and is the approach used by Windows, Linux, and even the JVM.

