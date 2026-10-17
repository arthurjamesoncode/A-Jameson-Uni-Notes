## ACID
ACID is a set of properties that good databases will adhere to. 

The four properties are:
- Atomicity
- Consistency
- Isolation
- Durability

This lecture will go over what each property is exactly, and roughly how it is enforced.
## Atomicity
Atomicity means that each transaction is an **atomic unit of processing**. This means that each transaction is indivisible, and therefore it is executed entirely or not at all.

This is necessary because it can deal with failure through aborting transactions:
- If a user aborts a transaction by cancelling it
- A system aborts a transaction because of deadlock
- Transaction aborts itself because the database is in an unexpected state
- The system crashes, or there is a network failure etc.

If an error prevents full execution the transaction is aborted and the database state is reset to what it was before the transaction. This is done through `ROLLBACK`.

If there is no error the entire transaction executes and the database state is updated correctly. This is done through `COMMIT`.
## Consistency
Consistency means that a correct execution of a transaction must take the database from one consistent state to another. 

There are various definitions of this, the slides for lecture 6 give two different definitions from different textbooks. Ironically it is the only ACID property without a consistent definition.

The slightly weaker, but common, definition is: Transactions must not violate constraints.

A stronger version is: It should correctly transform the database state to reflect the effect of a real world event.

Transactions, by virtue of atomicity, preserve consistency if run on their own. They always transform a consistent database state into another consistent database state.

This means that any serial schedule is consistent. This can be generalised to "Any schedule that changes the database in the same way as a serial schedule is consistent". We call such schedules **serialisable**.

>There is a note in the slide about consistency not being defined by being serialisable, but that for the purposes of this course we consider a schedule being serialisable to imply consistency.
## Isolation
A schedule satisfies isolation if and only if it is **serialisable**. Any schedule that satisfies isolation is serialisable.

The SQL standard divides isolation into different tiers of strength. From weakest to strongest they are:
- **Read Uncommitted** - No isolation. It is fine if you read data which has not been committed.
- **Read Committed** - Everything you read must have been committed before you can see it
- **Repeatable Read** - If you read the same thing twice in a transaction, you must get the same return value
- **Serializable** - All previous levels are satisfied and it is also serialisable.

This is decided by you before starting a transaction using:
```sql
SET TRANSACTION READ WRITE
ISOLATION LEVEL READ UNCOMMITED;
```

You can also set a transaction to be `READ ONLY` instead of `READ WRITE`.

After `LEVEL` you can also put:
- `READ COMMITED`
- `REPEATABLE READ`
- `SERIALIZABLE` (Must use American spelling for most implementations)
The default value is `SERIALIZABLE`, some implementations may have more isolation levels but this is all you need for this course.
## Durability
Durability means that once a transaction commits and changes the database, these changes cannot be lost due to subsequent failure. 

The effect of a transaction on the database should not be lost after the commit point. It can still be overwritten by future updates/transactions.

If there are any problems that cause a transaction to not happen, or for its effect to be reversed we must **REDO** the transaction.

This deals with things like **media failure**.
## DBMS Transaction Manager
Below you can see some components of a DBMS:
![[DBMS_components.png]]

You can see that there are two components which make up the transaction manager:
- Logging and Recovery
- Concurrency Control

Both of these components exist to satisfy ACID:
- Atomicity is satisfied via Recovery Control (Logging and Recovery)
- Consistency is satisfied via Scheduler (Concurrency Control)
- Isolation is satisfied via Scheduler (Concurrency Control)
- Durability is satisfied via Recovery Control