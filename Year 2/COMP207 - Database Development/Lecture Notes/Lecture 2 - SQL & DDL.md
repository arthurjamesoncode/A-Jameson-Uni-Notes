## Contents
Todays lecture will cover:
- Creating Databases in SQL
- How to create a table
- Persistency
- How to create constraints
- How to insert data
- How to update data
- How to delete data
## SQL & DDL
**SQL** stands for "**Structured Query Language**" and is a programming language designed for interacting with databases. 

This lectures covers some basic SQL but does not covering using it to query databases. Instead we are focusing on the commands of SQL which form a **DDL** or "**Data Definition Language**". These are a subset of commands that are used to define modify and manage the **schema**, or structure, of a database.

We will also look at some **DML**, or "**Data Manipulation Language**" commands, which are used to modify the data in a database.
### Creating Databases and Tables
To create a database in SQL we use:
```SQL
CREATE DATABASE xyz;
USE xyz;
```

The `CREATE` command makes whatever keyword follows it and then label that creation that creation the following identifier. In this case it creates a `DATABASE` and calls it `xyz`.

The `USE` command changes the currently active database to the specified database.

When working on the university server, each student has access to their own database, but doesn't have permission to create new database or change the currently active one. As a result you will never be required to use either of these commands in this module, but you should still know what they do.

To create a table you use the following command:
```SQL
CREATE TABLE TableName (
	field1 TYPE1,
	field2 TYPE2
);
```

`TableName` specifies what the table should be called and should be a valid identifier. 

Inside the brackets should be a comma separated list of all the fields in a single row of the table. Each item in the list should consist of:
- A valid identifier
- A valid type (will be covered shortly)

For example:
```SQL
CREATE TABLE Students (
	name VARCHAR(20),
	number INT,
	programme VARCHAR(4)
);
```

`VARCHAR` specifies a string of characters. The number inside the brackets specifies the max number of characters. `INT` specifies an integer number.

The casing of identifiers and keywords comes down to convention:
- Keywords are capitalised e.g. `CREATE` and `VARCHAR`
- Table name identifiers are in title case e.g. `TableName` and `Students`
- Other identifies are in snake case e.g. `first_name`
This is just to do with readability, it has nothing to do with performance or anything like that.
## Constraints
When creating tables we usually want to define some rules for the data in a table. This stops us from being able to insert data that may not be valid. 

There are many different types of constraints, but the main ones that we will cover today are:
- Primary Keys
- Foreign Keys
### Primary Keys
A primary key is a unique identifier for a relation in a table. This will usually be something like:
- A unique numeric ID
- A combination of fields which will always be unique
You technically can create tables without primary keys, but this is (almost) never a good idea in practice. I don't know of a situation where it would be a good idea, I say almost only because there may be some niche use I don't know about.

Given a table with a primary key constraint:
- If you try to add data to a table with a primary key that already exists, this will not work. 
- If you try to insert data without a primary key, this will not work

The way we specify a primary key constraint is with a line of the following format at the end of table definition:
```SQL
CONSTRAINT pk_identifier PRIMARY KEY (fields)
```

`pk_identifier` should be a valid identifier which serves as the label for the primary key constraint. By convention it should be `pk_table_name`.

`PRIMARY KEY` are keywords which specify this is a primary key constraint. 

`fields` should be a comma separated list of fields which make up the primary key.

For example, in our `Students` table we would add a primary key like so:
```SQL
CREATE TABLE Students (
	name VARCHAR(20),
	number INT,
	programme VARCHAR(4),
	CONSTRAINT pk_students PRIMARY KEY (number)
);
```
This specifies `number` to be the primary key of the table `Students`. 

You can use multiple fields together to form a primary key. This will be shown below in the section on foreign keys.
### Foreign Keys
Foreign keys are fields used to connect a row of one table to a row of another. They must always be the primary key of the other table.

Given a table with a foreign key constraint:
- Multiple different rows can contain the same foreign key
- If you try to create a new row without a foreign key this will fail
- If you try to create a new row with a foreign key that doesn't exist in the referenced table then this will fail

The way to add a foreign key constraint is
```SQL
CONSTRAINT fk_table1_table2 FOREIGN KEY (table1_field) 
REFERENCES Table2(table2_field)
```

`fk_table1_table2` is an identifier for the constraint. Since foreign keys relate two tables it is convention to include both tables in the identifier for it.

`FOREIGN KEY` are keywords which specify the constraint to be a foreign key constraint. The brackets which follow should contain the field from the current table which acts as the foreign key.

`REFERENCES` is a keyword with specifies the table and field which the foreign key relates to by the identifiers which follow. Note that while `REFERENCES` is placed on a separate line, there is no comma and therefore it is part of the same statement. Placing it on the next line is done purely for readability reasons.

For example, if we were to create a table which tracks which students are enrolled in which course, we could do so like this
```SQL
CREATE TABLE Enrolment (
	student_number INT, 
	course_id VARCHAR(20),
	CONSTRAINT pk_students PRIMARY KEY(student_number,course_id), 
	CONSTRAINT fk_enrolment_students FOREIGN KEY (student_number) 
	REFERENCES Students(number) 
);
```

This specifies `student_number` to be a foreign key which references a student in `Students` by their primary key.

Also note that in this table the primary key is a combination of the student's id number and the course id, not just a single number.
## Manipulating Data
We are now going to go over common ways to manipulate the data in a database including:
- Inserting data
- Updating data
- Deleting data
### Inserting Data
To insert data into a table we use the following syntax:
```SQL
INSERT INTO TableName VALUES (field_values);
```

`INSERT INTO` are keywords specifying that we want to insert a new row into a table. `TableName` is the identifier specifying which table. 

`VALUES` is a keyword which allows us to specify what values the new row should have. `field_values` is a comma separated list of values which should map to the fields in the table. The order of the values should be the same as the order the fields are defined in the table.

For example to insert a new student into `Students` we could do:
```SQL
INSERT INTO Students VALUES ('Oliver', 20241112, 'G702');
```

If you want specify a different order, for example if you don't remember which order the fields are defined in, you can do so like this:
```SQL
INSERT INTO TableName(field1,field2) VALUES (field1_value,field2_value);
```

So another way to add the same student into `Students` would be:
```SQL
INSERT INTO Students(number, name, programme) VALUES (20241112, 'Oliver', 'G702');
```

You can also use this method to leave a field blank. For example
```SQL
INSERT INTO Students(number, programme) VALUES (20241112, 'G702');
```
Although if you try to use this method to avoid a primary key, or any other required field, it will give you an error.

You can also add multiple entries at once by using a comma separated list of brackets after `VALUES`, for example:
```SQL
INSERT INTO Students(number, name, programme) 
VALUES
	(20241100, 'Amy', 'G402'),
	(20241112, 'Oliver', 'G702');
```

The indentation isn't necessary, I just think it helps readability.
### WHERE Clauses
While not necessary for `INSERT` statements, when you want to change the data that is in the database, we need a way to specify which data we want to change. The way to do this is through `WHERE` clauses.

These will go on the end of an `UPDATE` or `DELETE` statement and take the form:
```SQL
WHERE condition;
```

`condition` must be a valid condition. These generally take the form of:
```SQL
field <compartor> value
```
For example:
```SQL
name = 'Oliver'
```

For comparisons we have the operators:
- `=`
- `<`
- `<=`
- `>=`
- `<>` or `!=` (both mean not equals)

You can also combine or reverse conditions with:
- `AND`
- `OR`
- `NOT`

There is also `BETWEEN` which is true if a value is between 2 values, for example:
```SQL
Price BETWEEN 10 AND 20
```
and `LIKE` which is used for string matching, for example:
```SQL
Name LIKE 'O%r'
```
or
```SQL
Name LIKE 'O____r'
```

`%` matches any number of letters, and `_` matches any single letter. Both of the above examples would match `Oliver` for example, but would also match `Oghffr`.

There is also the special keyword `IN` which makes the condition true if the field is one of a list of values. For example:
```SQL
name IN ('John', 'Sebastian')
```
### Update and Delete
To update a row (or rows) of a table you can do:
```SQL
UPDATE Students 
SET name = 'Danny', programme = 'G700' 
WHERE number = 20241112;
```

`UPDATE` is a keyword which updates a table specified after it. `SET` is a keyword which specifies which fields you want to update, and to what values. The last part of the statement is a `WHERE` clause which specifies which rows should be updated.

To delete one or more rows of a table you can do:
```SQL
DELETE FROM Students WHERE number = 20241112;
```

`DELETE FROM` are keywords which specify which tables you want to delete from. The where clause specifies which rows should be delete.

Note a few things:
- You can't change a primary key
- If the primary key of a row is referenced as a foreign key in a different table, you cannot delete that row. The row referencing it must be deleted first.
- Most SQL servers or engines will default to a "safe mode" which stops `UPDATE` or `DELETE` queries from happening without a `WHERE` clause.
- If `UPDATE` or `DELETE` do not have a `WHERE` clause and safe mode is off they will affect every row in the table.