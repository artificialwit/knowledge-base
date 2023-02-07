# Basic

## What is SQL?
SQL is a non-procedural programming language developed by IBM in the 1970s and then later by Oracle. SQL is used by almost all relational databases to write queries, access, edit, and retrieve data.

## Explain the different types of SQL commands.
There are six basic types of SQL commands. DDL,MDL etc.

## What is a PRIMARY KEY constraint?
A PRIMARY KEY constraint is a column (or combination of columns) used to designate each table row with a unique identifier. You can think of a primary key as having a similar function to national government-issued identification numbers, a citizen's Social Security Number, or a vehicle identification number (VIN).

Note: There’s a limit of one PRIMARY KEY constraint per table. All columns defined within a PRIMARY KEY constraint must be defined as NOT NULL.

## What is a FOREIGN KEY constraint?
A FOREIGN KEY is a column or collection of fields in a table referencing a PRIMARY KEY in another table. The table containing the primary key is known as the parent table, and the table containing the foreign key is called the child table.

For example, the PRIMARY KEY in the parent table below is OwnerID. The PRIMARY KEY uniquely identifies individual pet owners.


For this child table, the PRIMARY KEY is PetID, and the OwnerID column is a FOREIGN KEY because it references the primary key of another table.


## What is a UNIQUE constraint?
Like the PRIMARY KEY, the UNIQUE constraint also ensures that each value is different from the others in its column. However, tables can have multiple columns with UNIQUE constraints, unlike the PRIMARY KEY constraint, limited to just one.

## What are SQL joins? What are the different types of joins?
In SQL, a JOIN clause combines rows of data in different tables with a shared column. You can SELECT and return records with matching values in both tables based on this relationship.

There are four kinds of JOIN clauses in SQL:


Related article: What are SQL joins? Types of SQL joins explained

## What is a self-join?
A JOIN clause combines rows from two or more tables based on a related column between them. A self-join is a regular join, but the table is joined with itself – this is extremely useful for comparisons within a table.

Joining a table with itself means that each table row is combined with itself and with every other row of the table.

## What is a cross join (Cartesian join)?
In SQL, the cross join combines each row of the first table with each row of the second table. It is also known as the Cartesian join since it returns the Cartesian product of the sets of rows from the joined tables.

## What’s the difference between a WHERE clause and a HAVING clause?
The WHERE clause can be used to establish the first condition that groups and returns only the rows that meet that condition into a result set. Then, secondary conditions can be applied using the HAVING clause to return only the groups within that set that meet your new criteria.

## What’s the difference between a TRUNCATE command and a DELETE command?

The TRUNCATE command is faster than DELETE, but unlike the DELETE command, data cannot be rolled back after using it to recover data that has been mistakenly deleted.

## What is a subquery?
A subquery or nested query is a query within a query.

There are two types of subqueries: Correlated and Non-correlated.

Correlated subqueries refer to a column in a table specified by the FROM keyword of the main query.
Non-correlated subqueries are independent and their output is substituted in the main query.

## What are UNION, UNION ALL, MINUS, and INTERSECT set operators?
- The UNION operation combines the results of two or more SELECT statements. For example, getting the UNION of sets A and B, this operation would return all rows from both sets, excluding any duplicate rows.

- The UNION ALL operation does the same thing as UNION, but includes duplicate rows in its result set.

- The INTERSECT operation combines the results of two SELECT statements but only returns the rows with matching values in both sets.

- The MINUS operation combines the results of two SELECT statements but only returns rows with values that belong to the first set of the result.

## What are Normalization and Denormalization?
- Normalization refers to the methods used to remove redundancies and inconsistencies in a database.

- Denormalization refers to methods used to improve the performance of queries.

- Normalization introduces more tables to a database, whereas Denormalization reduces the number of tables.

## What are scalar functions?
Scalar functions are defined by the user and return a single value (i.e., int, char, float, etc.) based on the input value.

Common SQL scalar functions:

- CONCAT() concatenates two or more character strings.
- FORMAT() sets the format to display a collection of values.
- LEN() calculates the total length of a given column.
- MID() extracts substrings from a collection of string values.
- ROUND() rounds the integer value for a numeric field.
- NOW() returns the current date and time.
- RAND() calculates a random collection of numbers of a given length.

## What are aggregate functions?
In SQL, aggregate functions (also known as group functions) are applied to a group of values (or all values) to calculate and return a single value.

Common SQL aggregate functions:

- AVG calculates the average or mean of all values in a group.
- COUNT calculates the number of rows in group, including rows with NULL values.
- MIN and MAX returns the smallest and largest value in a group, respectively.
- SUM returns the sum of all non-NULL values in a group.
- STDDEV calculates the standard deviation.
- VARIANCE calculates the variance.

## What is a stored procedure?
Instead of writing the same SQL query multiple times, you can save it as a stored procedure and call on it whenever necessary to execute it.

```sql
CREATE PROCEDURE procedure_name
AS
sql_statements
GO;
Execute a stored procedure:

EXEC procedure_name;

```

## What is an index?
An SQL index is a lookup table used by the database search engine to find and retrieve data quickly. An index can help makeSELECT and WHERE clauses faster but can slow down the use of UPDATE and INSERT statements.

```sql

CREATE INDEX index_name ON table_name;
```

## What are character manipulation functions?
Character manipulation functions can edit, change, or reformat character strings.

For example, you can concatenate two character strings by passing them into the CONCAT function using a SELECT query.

## What is an SQL Server cursor? How do you use it?
When you want to process result sets one row at a time, you can use a database cursor, a control structure that allows you to traverse records in a database. Cursors can be used to point to individual rows in a group of rows.

```sql

DECLARE variable_name CHAR(20) 
DECLARE cursor_name CURSOR FOR
SELECT column_name 
FROM table_name

```

## What are the different types of indexes?
- Clustered indexes are clustered together with the main body of data. A clustered index sorts and stores rows of data in a table or view sequentially, based on key values of the table to match the order of the index. There can only be one clustered index per table.
- Non-clustered indexes are separate from, and cannot be used to store or sort data in the main table. The key values of the index, and not the table are used to define the order of a non-clustered index.
- Column store indexes are a standard form of index that efficiently stores data in a column-based format, rather than row-oriented.
- Filtered indexes are used to index a section of rows within a table.
- Hash indexes are arrays, and use the Hash function F(K, N), where K is critical and N is the number of slots containing a pointer and row.
- Unique indexes assign unique values to every row of data, so that the index key does not contain any duplicates.

## What is the difference between a clustered index and a non-clustered index?
- The order of rows in a clustered index corresponds to the order of rows in the database. A table can only have one clustered index at a time.

- A non-clustered index functions similarly to a clustered index, but is slower and creates a separate entity within the table that references the original table. A table can have multiple non-clustered indices.

## What are ACID properties?

The ACID properties refer to properties that must be followed for transactions in a database management system to remain consistent.

- Atomicity: The entire transaction takes place at once or not at all.
- Consistency: A database must be consistent before and after a transaction takes place.
- Isolation: Transactions occur independently and can run concurrently with others.
- Durability: Updates to the database must be stored in and written to disk so that transaction records can persist in the event of a system failure.

## What is a schema?
An SQL schema is an abstract representation of logically structured data elements. Database schemas in SQL are defined at the logical level by a database user known as the schema owner.

Related article: What are database schemas? 5-minute guide with examples

## What is an alias command?
The alias (AS) command makes columns or tables easier to read by giving them temporary names for the duration of a query.

## How do you create empty tables with the same structure as another table?

You can use shallow cloning to create a copy of an existing table’s data structure and column attributes.
This command creates an empty table based on the parent table.

```sql

CREATE TABLE new_table LIKE table_1;
```

## How do you select unique records from a table?
The SELECT DISTINCT clause will only return unique values from a table.

## What are some case manipulation functions in SQL?

- LOWER or LCASE takes in a given character string and converts it to lower case.
- UPPER or UCASE takes in a given character string and converts it to upper case.

## What’s the standard syntax for group functions?

## What is the difference between CHAR and VARCHAR datatypes in SQL?

- The character or CHAR datatype stores fixed length character strings.
- The variable character or VARCHAR datatype stores variable length character strings.
- CHAR has better performance than VARCHAR, but VARCHAR can be useful for anticipating data values without a set length.

## What are user-defined functions in SQL? What are the various types?
There are two types of functions in SQL:

- System Defined Functions (SDF) and
- User-Defined Functions (UDF)
- User-Defined Functions (UDFs) are similar to functions found in programming languages. UDFs accept parameters, perform complex calculations, and return their results.

There are three types of UDFs:

- Scalar Functions return only a single value (scalar value) of any data type except text, ntext, image, cursor, and timestamp.
- Inline Table-Valued Functions return a table of values. Only one SELECT statement can be prepared by the return statement, and this statement defines the structure of the table that function returns.
- Multi-Statement Table-Valued Functions also return a table of values, but can contain multiple statements, and its table structure is defined by the user.

## What is collation? What are the different collation sensitivity?
Collation is a configuration setting that specifies how a database sorts and compares data. Different collation rules can be configured to determine the correct character sequence used to sort the character data.

Collation sensitivity can be used to specify how different characters are treated.

- Accent sensitivity differentiates between a and á.
- Case sensitivity differentiates between A and a.
- Kana sensitivity differentiates between Japanese Hiragana and Katakana.
- Width sensitivity treats characters of different widths (single-byte and double-byte) differently.

## Can you explain the difference between a clustered and a non-clustered index in SQL Server?
A: A clustered index determines the physical order of data in a table, whereas a non-clustered index provides a fast way to look up data without affecting the physical order of the table. A table can have only one clustered index, but multiple non-clustered indexes.

## How do you monitor the performance of a SQL Server database?
A: There are multiple ways to monitor the performance of a SQL Server database, including using performance counters, dynamic management views (DMVs), and extended events. You can also use third-party tools such as SQL Server Profiler, Database Engine Tuning Advisor, and SQL Server Performance Dashboard Reports.

## Can you explain the difference between a primary key and a unique key in SQL Server?
A: A primary key is a unique constraint that uniquely identifies each record in a table, and it cannot contain null values. A unique key is similar to a primary key, but it can contain null values. A table can have only one primary key, but multiple unique keys.

## How do you implement transaction management in SQL Server?
A: Transaction management in SQL Server can be implemented using the BEGIN TRANSACTION, COMMIT, and ROLLBACK statements, or by using the Transaction class in ADO.NET.

## Can you explain the difference between a subquery and a join in SQL Server?
A: A subquery is a query within another query that returns a single value or a table, whereas a join is a query that combines rows from two or more tables based on a related column between them. Subqueries can be used to simplify complex joins and to create complex conditions.

## How do you handle exceptions in SQL Server?
A: Exceptions in SQL Server can be handled using the TRY...CATCH block, which allows you to catch and handle exceptions raised by SQL Server.

## Can you explain the difference between a stored procedure and a user-defined function in SQL Server?
A: A stored procedure is a pre-compiled collection of Transact-SQL statements that can be executed multiple times, whereas a user-defined function is a subroutine that returns a single value or a table. Stored procedures can modify data and return multiple resultsets, whereas functions can only return a single value or a table.

## How do you implement row-level security in SQL Server?
A: Row-level security in SQL Server can be implemented using security predicates, which are predicates that restrict access to data based on a user's role or security context. Security predicates can be defined using security policies or by using dynamic data masking.

## Can you explain the difference between a view and a table-valued function in SQL Server?
A: A view is a virtual table that is based on the result of a SELECT statement, whereas a table-valued function is a user-defined function that returns a table. Views can simplify complex queries and provide a level of abstraction, whereas table-valued functions can be used to encapsulate complex logic or to return multiple result sets.

## How do you implement data partitioning in SQL Server?
A: Data partitioning in SQL Server can be implemented using partitioned views, which allow you to partition a large table into smaller, more manageable pieces, or by using table partitioning, which allows you to physically partition a table into multiple filegroups.



