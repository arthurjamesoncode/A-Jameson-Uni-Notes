## Simple Checkpoints (For Undo Logging)
Checkpoints can be used to decrease the size of log files that need to be traversed.

The idea is simple, checkpoint the log either after every *m* minutes or after every *t* transactions since the last checkpoint. Therefore we don't need to undo any transactions before the checkpoint.

When checkpointing the log, we:
1. Stop accepting new transactions
2. Wait until all active transactions finish and have `<COMMIT>` or `<ABORT>` written to the log.
3. Flush the log to disk
4. Write a log record `<CHECKPOINT>`
5. Flush the log to disk again
6. Resume accepting transactions

This allows us to be sure that everything before the checkpoint has been dealt with and the rest of the log can be disregarded during recovery (or even discarded).

This simple kind of checkpoint is not used widely in DBMS because:
- New transactions cannot be started while checkpointing
- We have to wait for transactions to be done before checkpointing
which results in a lot of delays.

What is more common are **ARIES** checkpoints which are covered below.
## ARIES Checkpoints
**ARIES** (Algorithm for Recovery and Isolation Exploiting Semantics) checkpoints are checkpoints which are widely used in DBMSs because they don't require the DBMS to stop accepting transactions while checkpointing. 

ARIES checkpoints have a few requirements of the DBMS:
- Must use undo/redo logging
- Transactions do not write to buffers before they are sure they want to commit

>Rasmus says that he is simplifying this a bit, I assume the hidden complexities are not relevant for the exam though so I don't care.

Now when checkpointing the log, we:
- Write `<CHECKPOINT(T_1, T_2,...)` in the log and flush it where `T_1` and `T_2` are the transactions in progress
- Write the content of the buffer to disk
- Write `<END CHECKPOINT>` in the log and flush it

Now when recovering we process the log as before except we stop at the first active transaction in the `<CHECKPOINT(transactions)` log. All transactions before this are already committed and as such we can stop there.
## Recoverable Schedules & Cascading Rollbacks
Consider the a schedule in which a transaction depends on previous transactions.

For example two users in a bank transferring money between each other. If there is a problem of partial execution where the first transaction happens but not the second this can cause some problems.

If we do nothing, money is lost and this breaks **atomicity**.

If we undo the first transaction but not the second, then the second transaction might not be valid anymore because there could have been other transactions and now the account can't transfer the money. This breaks **consistency** and **isolation**.

We could undo both transactions, but since the second one has finished and the person doing it might have already left and won't see the update. This breaks **durability**.

The reason problems like this happen is that, in practice, isolation is often not fully enforced and **dirty reads** might occur. This is to gain efficiency parallelism by spending less time on preventing dirty reads.

You can decide this using isolation levels for example:
```
SET TRANSACTION READ WRITE 
ISOLATION LEVEL READ UNCOMMITTED;
```
allows dirty reads.

One solution to this could be to have **cascading rollbacks**:
1. If a transaction T aborts, find all transactions that have read items written by T
2. Abort these transactions and repeat step 1 recursively

In practice this is very slow. However if we don't do this then we break isolation. However even if we do do it, rolling back previous transactions can break durability.

The way we actually deal with this problem is **Recoverable schedules**.

A schedule is **recoverable** if a transaction $T_i$ commits and has read an item $X$ that was written before by $T_j$, then $T_j$ must commit before $T_i$ commits. (Note only affects $r_i(X)$ and $w_j(X)$ combos)

This means that now when cascading rollbacks occur, they can only force active transactions to abort. This ensures that **durability** is not broken while allowing the rollback to ensure **isolation**.

Take the examples below
![[recoverable_examples.png]]

The implicit assumption here is that all log records must reach the disk in the order that they are written.
## Cascadeless Schedules & Strict Schedules
A cascadeless schedule is a schedule in which each transaction in it reads only values that were written by transactions that have already committed.

This ensures:
- No cascading rollbacks
- No reading of dirty data

Consider the examples below
![[cascadeless_examples.png]]

Note that cascadeless schedules are not necessarily serialisable. This is obviously a problem since we generally want our schedules to be conflict serialisable.

The solution to this is **strict** schedules.

A schedule is strict if each transaction in it reads and writes only values that were written by transactions that have already committed.

This is like cascadeless schedules, but with the added quality that writes have the same restriction as reads.

Any strict schedule is both **recoverable and cascadeless**.

Below you can see an example of a strict schedule
![[strict_examples.png]]

But the following schedule is only cascadeless, not strict
![[strict_anti_example.png]]

Again, it's very important that log records reach disk in the right order.
## Strict 2PL
Strict 2PL is a way to enforce both:
- Strict schedules
- Conflict serializability

It has the same condition as regular 2PL (view [[Lecture 8 - Locks#2PL|here]]), but with the added condition that a transaction T must not release any lock (that allows T to write data) until:
- T has committed or aborted and
- The commit/abort log has been written to disk

![[strict_2pl_example.png]]

Strict 2PL can enforce, conflict serializability and strict schedules but still has the problem of deadlocks.

There are two approaches for deadlock prevention:
- Detecting deadlocks and fixing them
- Enforcing deadlock free schedules (would have to be not Strict 2PL)