## Why Transactions Abort
Transactions can abort for a number of reasons:
- Errors while executing transactions - Such as a violation of integrity constraints or other run time errors.
- Deadlocks - Concurrency control will request to abort the transactions
- Explicit requests - Rollback in SQL

There are also a number of reasons outside the control the DBMS:
- Media failures - the medium holding the database becomes partially or completely unreadable
- Catastrophic events - The medium holding the database is destroyed
- System failures - Information about the active transactions state is lost

There are safeguards to ensure that none of these are unrecoverable, mainly full and incremental archives at different locations prevent total loss of data from the first two.

>Full archives mean storing everything on the disk in the archive. Incremental means storing a list of changes.
>
>RAID is mentioned very briefly in the slide it doesn't seem important but [here](https://en.wikipedia.org/wiki/RAID) is a link.

System failures make logging important so that information about the current transaction are not lost. Logging is essential for ensuring atomicity, and durability.
## Logging
The idea behind logging is to deal with system failure by writing important activities to a log so that the desired database state can be recovered later.

Important activities include:
- Starts of transactions
- Commits
- Aborts
- Modification of database items

There are a few different types of logging that are important:
- Undo logging, which is used for maintaining atomicity
- Redo logging, which is used for maintaining durability
In practice a combination of these two things are used (Undo/Redo logging).

We can extend the syntax we used for transactions to include logging. 

The following items refer to the low level operations the DBMS is doing, and they will trigger certain logs:
- `write(X)` writes the item X to a buffer
- `output(X)` copies the item X from the buffer to the database
- `flush_log` write log entries that are currently residing in the buffer to the log
### Undo Logging
Undo logging, logs activities with the goal of restoring to a previous database state. This can ensure **atomicity** as it makes sure that transactions happen either altogether or not at all.

Log records include:
- `<START T>`: Transaction T has started
- `<COMMIT T>`: Transaction T has committed
- `<ABORT T>`: Transaction T was aborted
- `<T, X, v>`: Transaction T has updated the value of database item X and the old value of X was v

The last log is a response to `write(X)` and doesn't mean that the new value of X has been written to the database on disk yet. That is only true after a `<COMMIT>` log has been written.

If a transaction updates a database item and the old value was v, then `<T, X, v>` must be written to the log on disk **before** X is written to disk.

If transaction T commits, then `<COMMIT>` must be written to the log on disk as soon as all database elements changed by T have been written to disk.

For example consider the transaction below
![[undo_log_transaction.png]]

Now consider what happens if a system failure happens. In this case the recovery manager traverses the log to restore the last consistent database state, on:
- `<COMMIT T>` - It remembers that T was committed successfully and does nothing
- `<ABORT T>` - It remembers that T was aborted and does nothing
- `<T, X, v>` - if there is no subsequent commit or abort then change the value of X back to v.

It then writes `<ABORT T>` for each uncommitted transaction T that was not previously aborted and calls `flush_log`.

If a transaction aborts, the same process is followed. In this case however the recovery manager only considers items from that transaction goes from the last item to the first.

Here's an example of what undo-logging looks like on a schedule, instead of on a transaction.
![[undo_log_schedule.png]]
### Redo Logging
Redo Logging is done with the goal of restoring committed transactions.

The log records are the same as before except now:
- In `<T, X, v>` v is the new value of X, not the previous.

The way redo logging works is:
- T writes all log records for all updates
- T write `<COMMIT T>` to the log on disk
- T writes all committed updates to disk

The fundamental properties of redo logs are:
- `<COMMIT T>` is in log implies that the log contains complete information on T
- `<COMMIT T>` is not in log implies that nothing has been written to disk yet

Below you can see an example of redo logging in a transaction
![[redo_log_transaction.png]]

To recover when using a redo logging system:
- Identify all transactions that have a COMMIT record
- Traverse the log from first item to last item
- If there is a `<T, X, v>` item and `T` has a COMMIT log record then change the value of X on disk to v
- For each incomplete transaction write `<ABORT T>` into the log on disk

Here's an example of redo logging with a two transaction schedule
![[redo_log_schedule.png]]
### Undo/Redo Logging
Undo logging ensures atomicity for certain. It can also ensure durability using **Force**, which means to force the writing of updates to the disk before committing. Although this is expensive in terms of disk operations.

Redo logging essentially ensures durability, but it can also ensure atomicity using **No Steal**, which means that uncommitted data may not overwrite committed date on disk, although this is expensive in terms of main memory to ensure.

As a result most (if not all) commercial DMBS use **undo/redo logging** which simply means to have two separate logs. One undo log, one redo log. This allows the DBMS to use **No Force** and **Steal** which is much cheaper.