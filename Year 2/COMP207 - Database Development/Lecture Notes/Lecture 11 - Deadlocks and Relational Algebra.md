## Deadlocks
Deadlocks occur when at least two transactions are waiting for locks each other to release a lock before they will release the lock the other one(s) need.

For example if we had the transactions
$$
T1:\;l_1(X);l_1(Y);...
$$
and
$$
T2:\; l_2(Y);l_2(X);...
$$
and a resulting schedule
$$
S:\; l_1(X);l_2(Y);l_1(Y);l_2(X)
$$
This would result in deadlock since $T2$ would hold a lock for $Y$ and $T1$ would not be granted access but still won't unlock $X$.

Strict 2PL gives us conflict serialisable strict schedules but can lead to deadlocks. This is obviously a problem, and we need to deal with it by either:
- **Detecting Deadlocks** and fixing them
- **Preventing Deadlocks** (by using scheduling that is not 2PL)
## Detecting Deadlocks
There are two simple ways to detect deadlocks.
- Timeouts - Assume a transaction is in deadlock if it exceeds a given time limit
- Wait-for graphs - Draw directed graphs with transactions as nodes and edges to indicate that one transaction is waiting for another. Any cycles indicate a deadlock.

The problem with timeouts is that we don't know how long a transaction should take to execute which can obviously lead to problems if we set our timeout timer too long or too short.

Wait-for graphs are expensive to maintain, and it can be hard to efficiently detect cycles using graphs. This makes them too expensive to maintain in terms of processing power and memory.

Many DBMS use the above methods but there other methods of preventing deadlocks rather than detecting them.
## Timestamp Based Deadlock Prevention
This means that each transaction is given a unique integer $TS(T)$ upon arrival. If 
$$
TS(T1)>TS(T2)
$$
then it means that $T1$ arrived after $T2$ and we would say that $T1$ is older and that $T2$ is younger.

Transactions keep their timestamps even on a restart. **This is different from the timestamp based schedules we will see after this**.

Using these timestamps, we can enforce a policy that determines which transactions will wait for other transactions depending on their age.
### Wait-Die Policy
In a **wait-die** policy older transactions will always wait for unlocks.

Imagine a transaction $T1$ requests a lock that is held by $T2$:
- If $T1$ is older than $T2$, $T1$ is allowed to wait until $T2$ unlocks (wait)
- If $T1$ is younger than $T2$, $T1$ must be rolled back (die)

Since only older transactions are allowed to wait at all, no cyclic dependencies can ever be created.
### Wound-Wait Policy
In a **wound-wait** policy older transactions never wait for unlocks.

Imagine a transaction $T1$ requests a lock that is held by $T2$:
- If $T1$ is older than $T2$, $T1$ *wounds* (or kills) $T2$ forcing it roll back. (wound)
- If $T1$ is younger than $T2$, $T1$ is allowed to wait until $T2$ unlocks (wait)

Since only younger transactions can wait no cyclic dependencies can ever be created.

>Note for remembering these policies: Both of them are two words where the first word describes what the older one does, and the second word describes what the younger one does.
>
>In also in both cases, **the young ones die**.
## Preventing Deadlocks With Timestamp Based Schedules
The basic idea of using timestamp based schedules is to schedule transaction so that the effect is the same as executing each transaction instantaneously when it started.

This creates a schedule that is serialisable since this is equivalent to a serial schedule which executes transactions in the order of their start time.

To look at these schedules we need to consider what options the scheduler has when a transaction requests to read or write an item. It can:
- Grant the request
- Abort the transaction
- Delay the transaction

When working with timestamp based schedules, give each transaction a new timestamp upon restart, and we ensure that two transactions do not have the same timestamp. **This is different compared the previous timestamp based prevention discussed**.

To maintain these timestamp based schedules we need to do some extra bookkeeping.

For each database item $X$ we maintain:
- $RT(X)$ meaning the **Read Time** of $X$ which is the timestamp of the youngest transaction which has read $X$.
- $WT(X)$ meaning the **Write Time** of $X$ which is the timestamp of the youngest transaction which has written $X$.

Given all of this information our scheduler can now handle requests in a way that prevents deadlock.

If a transaction $T$ requests to read $X$ then the scheduler will abort and restart $T$ if:
- $WT(X)>TS(T)$
- Otherwise grant the request

If a transaction $T$ requests to write $X$ then the scheduler will abort and restart $T$ if:
- $WT(X)>TS(T)$
- or $RT(X) > TS(T)$
- Otherwise grant the request.

Essentially it does three things:
- Enforces that no other transaction which started after the given transaction has **manipulated** an item that the current transaction **wants to read**
- Enforces that no other transaction which started after the given transaction has **manipulated** an item that the current transaction **wants to write** 
- Enforces that no other transaction which started after the given transaction has **read** an item that the current transaction **wants to write**

Timestamp based schedules have some nice properties:
- Enforces conflict serialisable schedules
- Deadlocks do not happen
But they also have some problems:
- Cascading rollbacks can happen
- Starvation can occur due to cyclic aborts and restarts of transactions. This can be prevented but the techniques to do so are not covered in this module.
- Schedules are not strict.

We can make timestamp based schedules strict by adding a single condition:
- Delay read or write requests until the youngest transactions that wrote to $X$ has committed or aborted.
### Multiversion Concurrency Control
Multiversion concurrency control is a variant of time stamp based approaches that many DBMS are implementing. 

The idea is the same as timestamp based scheduling but you have multiple versions of the database:
- This means that write operations don't overwrite each other but instead $w_i(X)$ creates a new version of $X$ at time $TS(T_i)$.
- Whenever you read you take the latest version before the transactions timestamp.

This means that a transaction only needs to restart if it tries to write and the read timestamp is later than your timestamp. This is nice because it means reads can always be granted, and transactions have to restart far less often.

There is also a strict version of this, where you delay reads until the transaction you read from commits.
## Relational Algebra
Relational algebra is like algebra but works on tables instead of numbers. This is important for optimising query plans, which is one of the next topics in this module.

These are essentially maths functions which roughly translate to SQL queries. The difference is that they ignore duplicates and have no order.

There are a number of relational algebra functions that we need to know.
### Projection ($\pi$)
If we write 
$$
\pi_{atrributes}(R)
$$
this restricts the table/relation $R$ to the attributes in $attributes$.

For example if we have the following table
![[employees_sample_table.png]]

Then 
$$
\pi_{\text{family\_name,birthday}}(Employees)
$$
is
![[employees_projection.png]]

This would be roughly equivalent to
```sql
SELECT DISTINCT family_name, birthday 
FROM Employees;
```

### Renaming ($\rho$)
If we write
$$
\rho_{A1\to B1,A2\to B2}(R)
$$
This returns a table with the attribute $A1$ renamed to $B1$ and $A2$ renamed to $B2$.

So if we have the table ![[employees_sample_table.png]]

Then
$$
\rho_{birthday\to bday}(Employees)
$$
would give us the table
![[employees_renaming.png]]

This would be roughly equivalent to
```sql
SELECT DISTINCT 
	birthday AS bday, 
	first_name, 
	family_name 
FROM Employees;
```
### Selection ($\sigma$)
If we write
$$
\sigma_{condition}(R)
$$
then we get the set of tuples in $R$ that satisfy the condition.

So if we have![[employees_sample_table.png]]

And we write
$$
\sigma_{\text{first\_name='Anne'}}(Employees)
$$
then we get
![[employees_selection.png]]

This is roughly the same as
```sql
SELECT DISTINCT * 
FROM Employees 
WHERE first_name=‘Anne’;
```

### Cartesian Product ($\times$)
If we write 
$$
R_1\times R_2
$$
Then we get the result of combining all tuples in $R_1$ with all tuples in $R_2$.

For example if we have the tables![[modules_and_lectures.png]]

If we wrote
$$
Modules \times Lecturers
$$
We would get the table
![[modules_and_lecturers_cross.png]]

This would be roughly the same as
```
SELECT DISTINCT * 
FROM Modules, Lecturers;
```
### Natural Join ($\bowtie$)
If we write 
$$
R_1\bowtie R_2
$$
We get the join of each tuple in $R_1$ and $R_2$ with matching common attributes.

For example if we had the tables
![[employees_sample_table.png]]

![[transaction_sample.png]]

And we wrote
$$
Employees \bowtie Transactions
$$
We would get the table
![[employee_transaction_nat_join.png]]

This is roughly equivalent to
```sql
SELECT DISTINCT * 
FROM Employees 
NATURAL JOIN Transactions;
```
### Other Functions
There are many other functions that are used in relational algebra. However these 5 are needed for this module.

Group By, and left/right semi joins are also mentioned, but it doesn't seem like we will need the definitions for these.