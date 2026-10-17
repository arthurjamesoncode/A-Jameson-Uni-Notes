## ORDER BY
`ORDER BY` defines how the output is sorted.

For example, if I wanted to get all of the names of our employees and sort them by `family_name`, I could do:
```sql
SELECT 
	first_name, 
	family_name
FROM Employees
ORDER BY family_name;
```

You do not actually need to request the sorting column to sort by it. So
```sql
SELECT first_name
FROM Employees
ORDER BY family_name;
```

Returns only the first names, but would do it in  the same order as the first query does.

Different values are sorted in different ways:
- Numeric values are sorted by size
- String values are sorted lexicographically
- Dates are sorted by order

`ORDER BY` defaults to ascending order meaning:
- Smaller numbers come first
- Earlier letters/symbols come first
- Earlier dates come first

If you want to sort by descending order instead you can do this by using the `DESC` keyword. For example:
```sql
SELECT first_name
FROM Employees
ORDER BY family_name DESC;
```

You can also order by multiple attributes like so:
```sql
SELECT first_name
FROM Employees
ORDER BY family_name, first_name;
```

Higher priority is given to the first attribute passed to `ORDER BY`, in the above's case this would be `family_name`.

`DESC` is specified individually for each attribute, and each attribute still defaults to ascending order.
## GROUP BY
`GROUP BY` is used to organise results based on a given attribute.

For example consider the tables below
![[transactions_employees.png]]

If I wanted to find out how many transactions the employee with id 1 was a part of I can do:
```sql
SELECT Count(t_id)
FROM Transactions
WHERE e_id = 1;
```

If I wanted to do that for all employees I could use `GROUP BY` like so:
```sql
SELECT e_id COUNT(t_id)
FROM Transactions
GROUP BY e_id;
```

Which would return this
![[group_by_example_output.png]]

When using `GROUP BY` the only valid attributes to select are:
- Attributes we are grouping by (e.g. `e_id`)
- Aggregate attributes such as `COUNT()`, `SUM()` or `MAX()`

To get around this we can simply also group by other attributes that we want to select.

For example if we wanted to also show the `first_name` of the employee with the corresponding `e_id` we can't do:
```sql
SELECT 
	first_name, 
	e_id, 
	COUNT(t_id) 
FROM Employees 
NATURAL JOIN Transactions 
GROUP BY e_id;
```

and instead must do:
```sql
SELECT 
	first_name, 
	e_id, 
	COUNT(t_id) 
FROM Employees 
NATURAL JOIN Transactions 
GROUP BY first_name, e_id;
```

`GROUP BY` works like this:
- Performs the query up till group by but ignores the columns
- Splits the table into sub tables based on the attributes specified in `GROUP BY`
- Uses each of those sub tables for the aggregates specified in select
- Outputs a table made of the combined sub-table attributes and aggregates.
### HAVING
`HAVING` is like `WHERE` but done after `GROUP BY`. It does not affect the `GROUP BY` statement, but simply filters out which groups are shown.

It can use aggregates on the sub tables to do this. For example
```sql
SELECT 
	first_name, 
	e_id, 
	COUNT(t_id) 
FROM Employees 
NATURAL JOIN Transactions 
GROUP BY first_name, e_id 
HAVING MIN(c_id)<5;
```

Only shows groups where the smallest `c_id` in the resulting sub-table is less than 5.
## UNION
`UNION` in SQL functions the same as it does with sets in maths.

> Union in maths has been covered in [[Lecture 12 - Set Operations]] from COMP109.

It essentially combines the outputs of two different `SELECT` statements into one.

Take the following table
![[employees_union_start.png]]

If we perform the following query:
```sql
SELECT first_name AS name, e_id
FROM Employees
UNION
SELECT family_name, e_id
FROM Employees
```

It will return the results of both of these queries combined into one giving us the following table
![[employees_union_end.png]]

There are a few interesting things about how these queries work.

You may have noticed that we renamed `first_name` to `name` and that we didn't do this to `family_name`. 

Union matches columns based on the order they appear in each `SELECT` statement. The name of the column is taken from the first `SELECT` statement, hence why we don't need to rename the `last_name` attribute like we did the first.

When using `UNION`, each `SELECT` statement must contain the same number of columns, and each corresponding column must be of a similar data type. 

That means that 
```sql
SELECT first_name 
FROM Employees 
UNION 
SELECT last_name, e_id 
FROM Employees;
```
doesn't work since there is a different number of columns between the first statement and the second.

However
```sql
SELECT e_id, first_name AS name 
FROM Employees 
UNION 
SELECT family_name, e_id FROM Employees;
```
does work on many systems since `e_id` can be implicitly changed to a string or varchar. This does depend on specific implementation. The above works in MySQL but not SQL server for example. 

When it does work, you will see the output below.

![[backwards_union.png]]
## Views
`VIEWS` are also called:
- Saved Queries
- Virtual Tables

Take the tables below
![[transactions_employees.png]]

We could perform the following query on the table to find out the number of transactions each employee was a part of:
```sql
SELECT 
	first_name, 
	e_id, 
	COUNT(t_id) 
FROM Employees 
NATURAL JOIN Transactions 
GROUP BY first_name, e_id;
```

If we wanted to save this result as a table we could do
```sql
CREATE VIEW EmployeeTransactionCount AS
SELECT 
	first_name, 
	e_id, 
	COUNT(t_id) 
FROM Employees 
NATURAL JOIN Transactions 
GROUP BY first_name, e_id;
```
And we can now query this view like it was any other table.

By default, data in `VIEWS` can't be modified but we can change them by using
```sql
CREATE OR REPLACE VIEW EmployeeTransactionCount AS
SELECT 
	first_name, 
	e_id, 
	COUNT(t_id) 
FROM Employees 
NATURAL JOIN Transactions 
GROUP BY first_name, e_id;
```

And they can also be removed with
```sql
DROP VIEW EmployeeTransactionCount;
```