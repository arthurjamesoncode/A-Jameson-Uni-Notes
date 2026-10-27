## How Conflict Serializable Schedules are Enforced
So far in this course we have looked at schedules as a finite list of operations. In a DBMS, however, the transaction manager is dealing with a continuous stream of operations. These operations are then passed to a scheduler which then executes or delays requests.

![[transaction_scheduling.png]]

So given this, how is conflict serializability enforced?

The answer is **locks**.
## Simple Locks
In a simple lock system:
- Every transaction must **lock** an item before it accesses it. 
- These locks are requested from and granted by the scheduler.
- Each item can only be locked by one transaction at a time.
- Transactions will wait until a lock is granted.
- Every lock has to eventually be released.

We can extend the notation we have been using so far to show locks by using
```
l_i(X) // transaction i locks X (requests a lock)
u_i(X) // transaction i unlocks X
```

A schedule using this syntax could be
```
S: l_1(X); r_1(X); u_1(X); l_2(X); r_2(X); w_2(X); u_2(X)
```

When writing schedules for locks we must remember:
- For each $r_i(X)$ or $w_i(X)$ there must be an earlier $l_i(x)$ that is not been yet been unlocked by a $u_i(X)$
- For each $l_i(X)$ a $u_i(X)$ must come after
- Between each $l_i(X)$ and $l_j(X)$ there must be a $u_i(X)$

Schedules with locks may not be serialisable.

Consider the schedule below
![[non_serializable_locks.png]]

$T_1$ can execute the first half of it, then $T_2$ can execute the whole thing. Since $T_2$ edits Y in its second half, this changes what would happen in $T_1$'s second half if they were to happen serially.

We can fix this by simply locking $Y$ before we release $X$
![[serializable_locks.png]]

Now, $T_2$ cannot edit $Y$ before $T_1$ is finished (or vice versa depending on which happens first) ensuring serialisability.
### 2PL
2PL, or **Two-Phase Locking** is a modification of the simple locking mechanism that **guarantees conflict serialisability**. An example of it was already shown above.

>There is a proof that 2PL ensures conflict-serialisability in the videos but I think it's kind of intuitive and won't be on the exam so I'm not going to spend the time to put it here.

In 2PL: **All lock operations precede all unlocks**.

It is called 2PL because it has two phases:
- Phase 1: Request locks
- Phase 2: Unlock locks
Both phases can contain other database operations

To check if a schedule satisfies 2PL you simply need to look for the first unlock operation. If there is no lock operations after that point, we know it satisfies 2PL.
## More Flexible Locks
There are some problems with the simple system presented here. Namely:
- Conflicts don't happen on Read/Read yet a transaction still needs to lock an item to read it
- Deadlocks

Deadlock is when two transactions cannot complete because they are both locking a resource that the other needs, and neither will release their lock until the other releases theirs.
![[deadlocks.png]]

This will be covered in more detail later in later lectures.

However to make 2PL more flexible we can introduce **shared** and **exclusive locks**:
- Shared locks are requested when a transaction needs to read an item and are granted to multiple transactions at the same time
- Exclusive locks are requested when a transaction needs to write an item and are granted to at most one transaction at a time

In addition:
- Shared locks are only granted when an exclusive lock on that item does not exist.
- Exclusive locks are only granted when no lock of any kind on an item does exist.

We can use the following notation to denote this
```
sl_i(X): transaction i requests a shared lock for item X
xl_i(X): transaction i requests an exclusive lock for item X
u_i(X): transaction i releases all locks on item X
```

With this system, a single transaction can hold both a shared lock and an exclusive lock for the same item X, essentially upgrading shared locks to exclusive locks.

There is a problem with this system though. Take the following 2 transactions for example:
![[upgrading_deadlock.png]]

If T1 and T2 are both given the shared lock, neither can be given the exclusive lock leading to deadlock. So upgrading causes us problems.

The solution is to grant **update locks** instead of shared locks:
- Requested by transactions to **read** an item
- Can be upgraded later to an exclusive lock
- Granted to at most one transaction at a time

**Update locks** are essentially exclusive locks except:
- They can still be grated if a shared lock exists on the item
- They are for read transactions not write transactions

If we take the same example
![[update_lock_example.png]]

Now T2's request for the u-lock would be denied, meaning that the entirety of T1 would execute first preventing deadlock.

With these more complex and flexible locks the same limitations of 2PL are mostly mitigated.
## Locking with Different Levels of Granularity
DBMS's may lock with various levels of granularity:
- May lock whole tables/relations
- May lock disk blocks
- May lock tuples

For example if we had the statement:
```SQL
SELECT name FROM Student WHERE studentID = 123456;
```
Then we could lock the tuple
```
(studentID=123456, name)
```

Where as if we had the statement
```SQL
SELECT avg(salary) FROM Employee;
```
then we would have to lock the whole relation/table.

There are different trade offs that come with different levels of granularity:
- Too coarse granularity (for example always locking relations) results in low overhead but means that there is less concurrency possible, causing delays.
- Too fine granularity results in very high overhead but leaves you with a very high degree of concurrency.

It's also important to prevent issues like one transaction holding a shared lock for a tuple, while another transaction holds an exclusive lock for the whole relation.
### Intention Locks
Intention locks, or warning locks, signal an intention to request a lock on a sub item. If a transaction wants to lock an item X, then they must first put an intention lock on the super items of X.

![[intention_locks.png]]

We use:
- IS: Intention to request a shared lock on a sub-item 
- IX: Intention to request an exclusive lock on a sub-item

The full policy for granting these locks is below
![[policy_for_granting_locks.png]]

