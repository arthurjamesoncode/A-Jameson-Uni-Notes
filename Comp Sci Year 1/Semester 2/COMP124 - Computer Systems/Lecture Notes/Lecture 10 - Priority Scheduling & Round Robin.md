## Priority Scheduling
Priority scheduling is a **preemptive** scheduling algorithm that gives preferential treatment to important processes.

Each process has a priority assigned to it (0 being the lowest) and the highest priority in the ready queue is placed onto the CPU. 
- If two processes have the same priority, then the one which arrived first is placed onto the CPU.
- If a process with a higher priority than the running process becomes ready, then it interrupts the running process and is placed onto the CPU.

Priorities for processes can be set by the user or assigned by the OS depending on whatever characteristic is most important:
- Memory usage
- I/O throughput
- Total CPU time
- Time already elapsed

For example, imagine we had the following five processes which arrive in this order with the given burst times and priorities:
- P1, with burst of **9ms** and priority **3**
- P2, with burst of **2ms** and priority **2**
- P3, with burst of **1ms** and priority **5**
- P4, with burst of **5ms** and priority **3**
- P5, with burst of **6ms** and priority **4**

Remembering that higher numbers mean higher priorities, and that processes with the same priority are scheduled in arrival order, we know that our processes would be scheduled like so:
![[priority_gantt.png]]

The **advantages** of "Priority Scheduling" are:
- Smaller wait times and latency for higher priority processes
- Important processes get dealt with quickly

The **disadvantages** of "Priority Scheduling" are:
- Bigger wait times and latency for lower priority processes
- Process starvation is still possible as higher priority processes will always be run before lower priority ones.

You can solve the starvation issue by using **process aging**. This means that you increase the priority of processes the longer they remain ready. This means that eventually they will be in the front of the queue.

This scheduling algorithm is commonly used in **real-time operating systems** where the processes must meet deadlines.
## Round Robin Scheduling
Round robin scheduling is a preemptive algorithm that gives a set amount of CPU time to each process.

Each process is allocated for a given quantum (time slice) between 10ms and 100ms (depending on the OS and need).

The ready state is treated as a circular queue:
- New processes arrive at the back of the queue;
- Scheduler takes the next process from the front of the queue;
- The process runs for a fixed amount of time, or until it terminates;
- If it terminates it is removed from the queue;
- If it hasn't terminated it is moved to the back of the queue by the context switch;
- The next process in the ready queue is selected.

For example, assume the following process arrive in this order and have their given burst times:
- P1 with a burst of **14ms**
- P2 with a burst of **2ms**
- P3 with a burst of **5ms**
- P4 with a burst of **4ms**
- P5 with a burst of **9ms**

If our scheduler uses a fixed time slice of **4ms** the scheduling will look like this.
![[round_robin_gantt.png]]
Note that the green P means that the process is passed to the back of the queue and the grey T means that the process terminates.

Also note that the OS moves the next process into the CPU the second it terminates, it does not need to wait for the time slice to end.

In this example:
- P1 needed 14ms and so had 4ms on the CPU before being **preempted**. Now it only needs 10ms.
- P2 needed 2ms and so **terminated** before the quantum was up and so entirely removed from the queue.
- P3 needed 5ms and so had 4ms on the CPU before being **preempted**. Now it only needs 1ms.
- P4 needed 4ms and so **terminated** after using us the full quantum.
- P5 needed 9ms and so had 4ms on the CPU before being **preempted**. Now it only needs 5ms.
The algorithm then starts again at the start of the queue.

For a round robin algorithm:
- We call the time taken for a process to terminate after its arrival onto the queue its **turnaround** time.
- We call its turnaround time minus its burst time its **wait time**.

For simplicities sake, assume all processes in the example arrived at time 0 (in reality processes are always arriving). With this assumption, we can consider P2:
- It arrived at time 0 and terminated at time 6, so it's turnaround time was 6ms;
- Its burst time was 2ms, so its wait time was 4ms.

If we table up all the turnaround times and wait times we can calculate the averages. See the table below for our turnaround and wait times.

![[turnaround_wait_table.png]]

This lets us calculate our average turnaround time like so
$$
t = \frac{34+6+23+14+32}{5} = 21.8\text{ms}
$$
and the average wait time like so
$$
t = \frac{20+4+18+10+23}{5} = 15\text{ms}
$$
The **advantages** of "Round Robin" are:
- Easy to implement as a queue;
- Doesn't depend on guessing or estimating **burst times**;
- Response time based on number of processes instead of process burst times;
- No starvation as every process gets a fair turn on the CPU;
- Balanced throughput

The **disadvantages** of "Round Robin" are:
- Depends on selecting a good **quantum**;
- Extensive overhead if the quantum is too short;

If the quantum is too big, "Round Robin" behaves like "First Come First Served", just with shorter processes executing a bit faster. If it too small it behaves like "Shortest Job First", just with longer processes executing a bit faster.
## Windows Scheduling Algorithm
Windows uses the "Priority Round Robin" algorithm. Which is a combination of priority scheduling and Round Robin.

Priority values range from 0 to 31, and each new process is given one of five base priorities:
- **IDLE** (4)
- **BELOW_NORMAL** (6)
- **NORMAL** (8) - this is the default
- **HIGH** (13)
- **REALTIME** (24)

Processes are given a **priority boost** when they are in the foreground (they are the currently active window). Processes can also be boosted when they receive an input or an event which they have been waiting for.

Boosted processes are reduced in priority by one level at the end of each time slice until their base level is reached.
## Linux Scheduling Algorithm
Linux also assigns a priority to each process
- Kernel processes have a value from 1 to 99
- User processes have a value from 100 to 139

It also assigns a ‘nice’ value to each user which ranges from −20 (highest priority) to +19 (lowest priority)
- Default is 0 for every user
- Users can change priorities with nice and renice commands

Linux uses an algorithm called **Completely Fair Scheduling** (similar to Round Robin) 
- Ready processes are stored in a balanced tree (not a queue)
- Gives credit for time spent in the blocked state 
- Time quantum varies depending on processor demand 
- Process priority and nice values combine to give overall priority