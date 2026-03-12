## Process Scheduling
The **processor manager** uses one or more scheduling algorithms to dispatch processes. The scheduling algorithms:
- Look at all processes in the ready state;
- Decide which ones gets allocated to the CPU;
- If good, gives the impression of speed and responsiveness.

We will look at a variety of scheduling algorithms over this lecture and [[Lecture 10 - Priority Scheduling & Round Robin|next lecture]].

Scheduling algorithms can be **preemptive** or **non-preemptive**.

In **non-preemptive** scheduling the process stays on the CPU until it terminates or blocks for I/O. This implements **multiprogramming**, and we have gone over the problems with this method.

In **preemptive** scheduling, processes can be interrupted and replaced with another process. This is what we need to implement **multitasking**.

### Scheduling Policies
The operating policy will have a **scheduling policy** according to some criteria:
- **Maximise Throughput** - Complete as many processes as possible in a given period
- **Minimise Turnaround Time** - Execute entire process as quickly as possible
- **Minimise Waiting Time** - Reduce the time that processes spend in the ready state without being executed
- **Maximise CPU Efficiency** - Keep the CPU busy at all times to avoid wasting cycles
- **Minimise Latency** - Reduce time taken between user requests and their responses

It's not possible to meet all criteria at the same time, so different algorithms will have trade offs between them.

The processor manager tries to ensure fairness for all processes. This means trying to give each process an equal amount of CPU and I/O time, ensuring that some processes don't hog the CPU.
## First Come First Served
First come first served is is the simplest scheduling algorithm to implement and understand.

It is a **non-preemptive** algorithm that deals with processes according to their arrival time.

This is easy to implement using a queue:
- When a new process is created, its PCB is added to the back of the ready queue
- When the CPU becomes free the process at the front of the ready queue is executed by restoring it's PCB to the CPU
- This process then stays on the CPU until either finishes or is waiting for I/O

There are two key properties of processes that need to talk about this algorithm:
- The **burst time** of a process is the time is takes on the CPU before it blocks or terminates.
- The **arrival time** of a process is the time it is first put into the ready state.

If we have the following three processes (which arrive in order):
- P1, with a burst time of 13ms
- P2, with a burst time of 5ms
- P3, with a burst time of 1ms
We can view the process schedule as **Gantt chart** showing the cumulative execution time.

![[Gantt_chart_example.png]]

No that we have a list of processes, their arrival order, and their burst times, we can calculate the average wait time for the processes.

We know how long the processes waited for:
- P1 waited for **0ms**
- P2 waited for **13ms**
- P3 waited for **18ms**

So we can calculate the average wait time like so:
$$
t = \frac{0+13+18}{3}=10.3\text{ms}
$$
We can see from this that if the processes arrive in a different order their average wait times can be very different. For example if they came in the following order:
- P2
- P3
- P1

Their waits times are now:
- P2 waits **0ms**
- P3 waits **5ms**
- P1 waits **6ms**

Allowing us to calculate our average wait time 
$$
t = \frac{0 + 5 + 6 }{3}=3.7\text{ms}
$$
which we can see is a lot lower than above.

This is so much lower because no process is waiting for our last process to finish, so, when we place our slowest process (P1) last, our system does less waiting.

The **advantages** of "First Come First Served" are:
- Very simple to implement;
- Scheduling overhead is minimal during a context switch;
- No **starvation** of processes, as every process will be gotten to eventually.

The **disadvantages** of "First Come First Served" are:
- Throughput can be low due to long processes staying on the CPU;
- Average wait time is not minimal and can vary substantially;
- Turnaround time and latency are hard to predict;
- Impossible to prioritise processes.

As we saw, we could get better all-round performance if we always scheduled large processes to go last.
## Shortest Job First
Shortest Job First is another **non-preemptive** algorithm that deals with processes according to their burst time.

As the name suggests, the next process chosen is the one with the **shortest** burst time. If two processes have the same burst time, the one with the earlier arrival time is chosen. This happens every time the CPU becomes free, and processes still stay in the CPU until they either terminate or block for I/O.

For example, imagine we have these four processes in the ready state:
- P1, with a burst of **5ms**
- P2, with a burst of **9ms**
- P3, with a burst of **6ms**
- P4, with a burst of **3ms**

The processes would be scheduled in the following order:
- P4
- P1
- P3
- P2

Given by the following **Gantt chart**
![[example_gantt_chart_2.png]]

We know that, since the shortest job is selected first, that the average wait time of this algorithm will be lower than the average wait time of "First Come First Served"

The **advantages** of "Shortest Job First" are:
- It reduces overall average wait time
- Provably optimal in giving minimal average wait time for a fixed set of processes

The **disadvantages** of "Shortest Job First" are:
- Can lead to **process starvation** of larger processes if smaller jobs keep getting created.
- Difficult to estimate **burst time** for new processes. It usually relies on prior experience.

The big issues with "Shortest Job First" come from it being a **non-preemptive** algorithm, which are just not suitable for modern any modern OS. 
- Many processes will get left in the **ready** state and they all need fair access to the CPU.
- Large processes tie up the CPU and reduce the overall system performance.
- The OS itself has processes that it needs to run on the CPU.
## Shortest Remaining Time First
If we remember that processes are being created all the time, we know that the ready state is not a fixed set of processes. New processes will appear and impact the scheduling algorithm.

"Shortest Remaining Time First" is a preemptive version of the "Shortest Job First" algorithm:
- The CPU is allocated to the process which is closest to finishing
- If a new process arrives that is shorter than the current running process, the current process is interrupted and the new process is run.

The **advantages** of "Shortest Time Remaining First" are:
- Short processes are handled very quickly
- Gives maximum throughput in most situations
- Doesn't require much overhead during the context switch

The **disadvantages** of "Shortest Time Remaining First" are:
- Starvation of longer processes is still possible is smaller process keep being created
- Introduces extra context switches
- Waiting time and latency increases for longer processes

A better approach than this is to use a preemptive scheduling algorithm with a fixed time slice. This lets you implement **multitasking** with a fixed quantum and clock interrupts, but still requires us to choose which process to schedule next. You can see an algorithm that works like this [[Lecture 10 - Priority Scheduling & Round Robin|next lecture]].