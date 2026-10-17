## Transaction
A transaction is just a sequence of queries that happen one after the other. This sounds easy, but there can be complications due to:
- **Concurrency**
- **Partial Execution**

There can be a lot of queries happening at similar times to each other which all effect a database in different ways. If we don't carefully handle how these interact, we can end up destroying the integrity of our database.

Similarly there can be queries that need to be executed together for the integrity of the database to not fall apart. For example moving money between users. Both the query to remove money from one user and add money to another user must occur together. If only one happens this is a massive problem for the database.
### Concurrency
Consider the following situation:
![[concurrency_problem.png]]

The Brown text corresponds to the following query:
```sql
SELECT seatNo 
FROM Flights 
WHERE 
	flightNo = 123 AND 
	date = ’2020-10-30’ AND 
	seatStatus = ’available’;
```

While the green text corresponds to the following query:
```sql
UPDATE Flights 
SET seatStatus = ’occupied’ 
WHERE 
	flightNo = 123 AND 
	date = ’2020-10-30’ AND 
	seatNo = ’14B’;
```

The current timeline causes no problems since all of user 2's queries are executed after all of user 1's queries. The problem comes in if user 2's brown query is executed after user 1's brown query but before user 1's green query.

This would cause issues as when user 2's green query goes through they would be booking a seat that user 1 has already booked.

>I think the example given is slightly weak since it doesn't connect a specific user to the seat, and so there is no actual downside to the seat being booked twice in this database but it should still hopefully show the gist of why we would use this. 
>
>This is more a complaint about the database itself being unusable compared to any statement about concurrency.

The solution is to wrap this up in a transaction. This ensures that a group of SQL statements must be executed without causing conflicts with any other statements. We will look at how this is enforced later.

```sql
START TRANSACTION;
SELECT seatNo 
FROM Flights 
WHERE 
	flightNo = 123 AND 
	date = ’2020-10-30’ AND 
	seatStatus = ’available’;
UPDATE Flights 
SET seatStatus = ’occupied’ 
WHERE 
	flightNo = 123 AND 
	date = ’2020-10-30’ AND 
	seatNo = ’14B’;
COMMIT; -- or ROLLBACK which aborts
```

`START TRANSACTION` starts the transaction. From here until the `COMMIT` statement, changes to the database are tentative. They only persist on the database after `COMMIT` has been run.

By labelling a sequence of statements as a transaction, makes the DBMS ensure that there is **serialisable behaviour**. Essentially, the transaction is executed as if it was executed in isolation from the other transactions happening concurrently. The end result is as if all queries that ran ran one after the other.

>I don't think this is the best explanation of this in practice. It kind of roughly gives the point of transactions and explains how they solve the problem in theory but I feel like the lack of an explanation for how they are enforced, the lack of a condition in the query that means that `Flights` being updated depends on if there is an available seat, and maybe some other stuff I don't know has left me lacking clarity on a lot of things.
>
>Unfortunately, I currently lack the understanding to do better than this so whatever I guess.
### Partial Execution
Consider the following situation
![[partial_execution_problem.png]]

The brown text corresponds to:
```sql
UPDATE Accounts
SET balance = balance + 100
WHERE accountNo = 456 
```

The green text corresponds to:
```sql
UPDATE Accounts 
SET balance = balance - 100 
WHERE acountNo = 123;
```

It's very important that both of these things happen. It is not acceptable for only one to happen. That means that if there is a failure in the middle of these two things it is a grave problem. Again transactions can solve this.

```sql
START TRANSACTION;
UPDATE Accounts
SET balance = balance + 100
WHERE accountNo = 456
UPDATE Accounts 
SET balance = balance - 100 
WHERE acountNo = 123;
COMMIT; -- or ROLLBACK which aborts
```

This is because telling the DBMS that a sequence of queries is a transaction ensures **atomicity**. This means that either the whole transaction happens, or none of it does.

