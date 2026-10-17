## Breaking Keys
This was covered to some extent last lecture but will be explicitly spelt out here.

**Primary Keys** can be broken if you:
- **Insert** a new entry with an existing primary key
- **Update** an existing entry such that you change it's primary key to an existing one.
Both of these restrictions simply come from the property that primary keys should be unique. 

Since that is the only restriction, it follows that you cannot break it by **deleting** a entry, since it is impossible for this to result in a non-unique key.

**Foreign Keys** can also be broken. 

Consider we have 2 tables, A and B, where a column in B is a foreign key that references a column in A. We can break this if we:
- **Insert** a new entry into B which contains a foreign key that doesn't exist as a primary key in A.
- **Update** an existing entry in B such that the foreign key no longer points to an existing entry in A.
- **Delete** an entry in A which is referenced by one or more entries in B.
## SELECT Statements
`SELECT` is how we get output from SQL tables. `SELECT` statements determine what things should be selected from a given input. The input is determined by the `FROM` statement and that will covered after.

The most basic query would just select all columns of all entries from a given table. This can be done using the wildcard symbol `*`. 

For example, take the table below
![[employees_table_example.png]]

If we wanted to select all columns from this table we could do:
```sql
SELECT * FROM Employees;
```

which would return the following
![[select_wildcard.png]]

We will now go over the four ways to modify this sort of statement:
- Projection
- DISTINCT
- Renaming
- Creating new columns
### Projection
We can also select specific attributes we want to keep, this is called **projection**. 

For example:
```sql
SELECT family_name, birthday
FROM Employees; 
```
which returns
![[select_projection.png]]

When doing this the **attribute order matters**. That is to say if I reversed the order of the columns I asked for, the result would have *birthday* come first and *family_name* come second.
### Distinct
The `DISTINCT` keyword can be used with `SELECT` in order to remove duplicate rows.

For example take the table below:
![[employees_table_distinct_example.png]]

If we did the following statement:
```sql
SELECT first_name
FROM Employees;
```

Then we would get
![[select_non_distinct.png]]

However if we used the `DISTINCT` keyword like so:
```sql
SELECT DISTINCT first_name
FROM Employees;
```

Then we would get
![[select_distinct.png]]

>The example they give for this is pretty weak because why would you filter for unique first names like this, but it's fairly obvious why this can be useful in more complicated queries.
### Renaming
You can rename attributes that you select using the `AS` keyword.

For example with the table below
![[employees_table_example.png]]

If we did the query:
```sql
SELECT 
	birthday,
	first_name,
	family_name AS surname
FROM Employees;
```

We would get the output:
![[select_renaming.png]]
### Creating New Columns
You can output new columns, that aren't in the original table, but performing operations on existing columns. You would usually give these new columns a name via renaming.

For example if you take the table below:
![[Pasted image 20261017163527.png]]

You could perform the following query:
```sql
SELECT
	name,
	price,
	number,
	price * number AS total_cost
FROM Items;
```

To get:
![[items_table_new_column.png]]

You can also use **constants** or similar to do operations. For example if you had **price** as an integer in pennies you could do:
```sql
price / 100 as price_in_pounds
```

We can also use aggregate operators like the following:
- `SUM(column_name)` returns the sum of all values in a given column.
- `COUNT(column_name)` returns the number of rows containing that column. Mostly used with `WHERE` clauses to count the number of rows which fit a filter.
- `AVG(column_name)` returns the average value of a column
- `MIN(column_name)` returns the minimum value of a column
- `MAX(column_name)` returns the maximum value of a column
## FROM Statements
`FROM` statements define the input for our queries. So far we have looked at very simple ones which only take one input such as
```sql
FROM Employees;
```

`FROM` statements do not only take single tables as inputs, we can combine tables in a number of ways. The main two covered in this course are:
- **Cross Product**
- **Natural Joins**
### Cross Product
The cross product is the more mathematically simple of these two ways of combining tables.

>We have covered cross product without referencing SQL in [[Lecture 20 - Relations]] of COMP109.

The cross product of two tables is just the combination of columns from all rows of two different tables.

It can be done in two ways:
- Using a comma separated list of tables
- Using the `CROSS JOIN` keywords

For example take the following tables
![[items_employees.png]]

If we do
```sql
SELECT first_name, name
FROM Employees, Items; 
```

We get the cross product of these two tables, which is:
![[items_employees_cross.png]]

This is the exact same result given by:
```sql
SELECT first_name, name
FROM Employees 
CROSS JOIN Items; 
```
I personally think this is clearer and easier to read

Note that if we did
```sql
SELECT *
FROM Employees, Items;
```
We would get the same number of rows, except each row would contain every column from both tables.
### Natural Join
`Natural Join` returns a table which contains all specified columns from both tables. The only rows in this new table are rows for which a column of the same name in each table share a value.

For example take the tables below 
![[transactions_employees.png]]

`e_id` is the name of a column in both of these tables.

If we performed a natural join of these tables we would get a table which has a row for every row in `Transaction` including the columns from `Employees` where `e_id` is shared.

So
```sql
SELECT *
FROM Employees 
NATURAL JOIN Transactions;
```
would return
![[transactions_nj_employees.png]]

Notice the order of the columns returned. Since `EMPLOYEES` was given to the FROM statement first, the columns from employees were placed first in the result. The remaining, non-shared columns from transaction come after.

Formally, when a natural join is taken, you:
- Take a cross product,
- Remove all rows where the common attributes are not the same
- Keep only one column for each common attribute

So the above is actually the same as:
```sql
SELECT 
	birthday, 
	first_name, 
	family_name,
	Employees.e_id AS e_id, t_id, c_id
FROM Employees, Transactions
WHERE Employees.e_id = Transactions.e_id;
```

Note that we use `TableName.attribute` to reference an attribute that multiple tables have in common. This ensures that there is a unique way to identify them.

If you wanted to shorten the names you can do so like this:
```sql
SELECT 
	birthday, 
	first_name, 
	family_name,
	E.e_id AS e_id, t_id, c_id
FROM Employees E, Transactions T
WHERE E.e_id = T.e_id;
```

You need to be careful when using natural joins. For example if we also had the table![[customers_table.png]]

And we tried to do:
```sql
SELECT *
FROM Employees 
NATURAL JOIN Transactions 
NATURAL JOIN Customers;
```

To join these three tables on `e_id` and `c_id` we would get nothing back.

This is because it tries to match **all common attributes** which in this case means also matching `first_name` and `family_name` between customers and employees.

Generally it is safer to use
```sql
INNER JOIN ON Table1.x_id = Table2.x_id;
```
instead, since this only matches the specified column, and not all common columns.
## WHERE Clauses
Where clauses were covered [[Lecture 2 - SQL & DDL|last lecture]] so I won't go over them again. This is simply a note to say that they can be used to filter select statements. 

Just place them after select statements and use them as shown before.