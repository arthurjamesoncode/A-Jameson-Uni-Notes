## Low Level SQL Operations
When discussing SQL operations in terms of schedules and transactions we need some easy way to denote this.

Take the following two SQL statements:
```
SELECT salary // READ
FROM Employees 
WHERE e_id = 1234; 

UPDATE Employees // WRITE
SET salary = salary*1.1
WHERE e_id = 1234
```

This can be translated into 3 transaction operations:
- `read(e_id=1234, salary)`
- `salary=salary*1.1`
- `write(e_id=1234, salary)`

The above is a simple abstracted notation that uses tuples to denote database operations, and programming notation to denote non-database mutations to that data.

We can go even further to simplify this notation:
- `read(X)`
- `X=X*1.1`
- `write(X)`

We don't care about what we are reading/writing when analysing transactions and schedules, we simply care about whether the things we are reading and writing are distinct.

There are some basic operations of transactions:
- `BEGIN`
- `END`
- `read(X)`
- `write(X)`
- and other non-database operations such as maths operations.

At the program and hardware level a DBMS performs various operations to do the two abstracted database operations.

When **reading** a DBMS:
- Finds the address of the disk block that contains item X
- Copies that disk block into a buffer in main memory (if not already in a buffer)
- Copies that item from the buffer to the program variable X

When **writing** a DBMS:
- Finds the address of the disk block that contains item X
- Copies that disk block into a buffer in main memory (if not already in a buffer)
- Copies item X from the program variable into the correct location in the buffer
- Stores the updated block in the buffer back to disk (may be instant, may be done later)
## Schedules
Schedules hold many transactions for execution. The operations making up the transaction are then executed by the schedule in some order, preserving the order of operations in the right order.

There are two types of schedule:
- **Serial Schedules** - Executes the transactions one after the other
- **Concurrent Schedules** - Can interweave operations from the transactions, while preserving the order of operations in each transaction

>Since concurrent schedules **CAN** interweave operations but don't have to, all **serial schedules** are concurrent but not all **concurrent schedules** are **serial**. Formally speaking.

We can denote schedules with a shorthand notation, using subscripts to denote which transaction each operation belongs to. Since all that we need for scheduling is to consider database operations such as:
- `read`
- `write`
- `commit`
- `rollback`

We can use the notation
- `r_t(X)`
- `w_t(X)`
- `c_t`
- `r_t`

To denote all relevant operations for a transaction, ignoring non-database transactions.

Say we have two transactions
```
Begin (T1) 
	read(X); 
	X := X + 100; 
	write(X); 
	read(Y); 
	Y := Y + 50; 
	write(Y); 
	commit; 
End (T1)

Begin (T2) 
	read(X); 
	read(Y); 
	X := X + Y; 
	write(X); 
	commit; 
End (T2)
```

We could describe a **serial schedule** that performs `T1` and then `T2` like so:
```
S_a: r_1(X);w_1(X);r_1(Y);w_1(Y);c_1;r_2(X),r_2(Y);w_2(X);c_2
```

We could also describe an example concurrent (but not serial) schedule like so
```
S_b: r_1(X);w_1(X);r_2(X)r_1(Y);w_1(Y);c_1;,r_2(Y);w_2(X);c_2
```

>The slides use colour to denote this more clearly. I do not have that luxury in obsidian without sorting out some plugins or some shit.

If we were to write something that didn't preserve the order of operations in `T1` or `T2`, that would NOT be a schedule. For example no valid schedule for these transactions would put `r_1(Y)` before `r_1(X)`.
## Serialisable Schedules
All good schedules will satisfy ACID, although this can be difficult to achieve. 

>This part will not look at atomicity and durability.

Serial schedules can guarantee both consistency and isolation however concurrent schedules do not guarantee either of these things.

The problem is that serial schedules are massively inefficient and not practical for most real world applications. The result is that we need to have concurrent schedules which act like serial schedules. In other words we need a **serialisable** schedule.

Formally:
	A schedule $S$ is serializable if there is a serial schedule $S'$ that has the same effect on every initial database state.

Below you can see an example serialisable schedule
![[serialisable_schedule.png]]

Below is a schedule which is not serialisable
![[non_serialisable_schedule.png]]

These schedules are what we want. Since they have an equivalent serialisable schedule we know that will satisfy:
- Isolation
- Consistency

The problem with these schedules is that it's very hard to show that a schedule is serialisable. This is because a schedule being serialisable doesn't only depend on the database operations but also the non-database operations which can be massively complex. As a result we use **conflict-serializable schedules**.
## Conflict Serializable Schedules
Conflict-Serializability is a form of serializability that is used and enforced by most commercial DBMS.

It is based on the idea of a **conflict** which is a pair of operations from different transactions that cannot be swapped without changing the behaviour of at least one of the transactions.

For example in the following schedule:
```
r_1(X);w_1(X);r_2(X);w_2(X);r_1(Y);w_1(Y);
```

The second and third operations represent a conflict since if `T2` reads before `T1` writes that will give a different result to if `T2` reads after `T1` writes.

Two operations can are in conflict if, and only if, the following is true:
- They are from different transactions
- One of them is a write operation
- They both access the same item

We call a schedule **conflict-serialisable** if it is **conflict-equivalent** to a serial schedule.

Two schedules $S$ and $S'$ are conflict equivalent if $S'$ can be obtained from $S$ by swapping any number of **consecutive**, **non-conflicting** operations from **different transactions**.

![[conflict_equivalent_schedules.png]]

This is much easier to check because if we simply have to see if it is possible to get all the `r_1` operations before the `r_2` operations.

**All conflict-serializable schedules are serialisable, but not all serializable schedules are conflict serializable.**

For example if a schedule is only write operations, it is serialisable since as long as the last write operation is executed last in the serial schedule it will be equivalent.

However by our definition of conflict it would be very easy to arrange these in a way that conflicts could prevent swapping to a serial schedule.
## Recognising Conflict-Serializable Schedules
To show that a schedule S is not conflict serializable, we need to:
- Identify the transactions in S
- Identify the conflicts in S
- Identify what constraints those conflicts impose on the order of transactions in every conflict-equivalent schedule

If the constraints imposed do not allow us to find a serial, conflict equivalent schedule then we know that our schedule is not conflict-serializable.

We can do this formally using a precedence graph. The precedence graph for schedule $S$ is defined as follows:
- It is a directed graph
- Its nodes are the transactions that occur in $S$
- It has a edge from $T_i$ to $T_j$ if there is a conflicting pair of operations $op_1$ and $op_2$ such that
	- $op_1$ appears before $op_2$ in $S$
	- $op_1$ belongs to transaction $T_i$
	- $op_2$ belongs to transaction $T_j$

![[precedence_graph.png]]

To check if a schedule is conflict serialisable you simply have to:
- Construct the precedence graph for $S$
- Check if the graph has cycles
	- No cycles mean $S$ is conflict serialisable
	- Any cycles mean $S$ is not conflict serialisable

