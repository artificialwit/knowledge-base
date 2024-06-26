# Interview

## Here are some steps you can follow to start taking an interview:

Good afternoon,

My name is Pratul Dwivedi, and I am working as a technical consultant with PCS Infinity. We are a product-based company primarily focused on asset management. Currently, we are actively seeking a skilled SQL Server developer to join our team.

- Preparation: Before the interview, research the company, the position you're hiring for, and the requirements for the role. This will help you ask relevant and informed questions.

- Introduction: Begin the interview by introducing yourself and the company, explaining the purpose of the interview, and providing an overview of the interview process.

- Ask open-ended questions: Start the interview by asking open-ended questions to get the candidate talking. This will give you a sense of their communication skills, personality, and how they approach problem-solving.

- Dig deeper: Once you've gotten a general understanding of the candidate's background, ask more specific and technical questions related to the role. This will help you assess their qualifications and skills.

- Listen actively: Pay attention to the candidate's responses and be an active listener. Take notes and ask follow-up questions to clarify their answers.

- Provide feedback: Give the candidate feedback on their responses, including both positive and constructive feedback.

- Wrap up: At the end of the interview, thank the candidate for their time and let them know what the next steps are in the hiring process.

## PARSE() vs CAST() vs CONVERT() in SQL Server: What’s the Difference?
Use PARSE only for converting from string to date/time and number types. For general type conversions, continue to use CAST or CONVERT. Keep in mind that there is a certain performance overhead in parsing the string value.

https://database.guide/parse-vs-cast-vs-convert-in-sql-server-whats-the-difference/

## Window Functions
Window functions allow you to perform calculations across a set of rows that are related to the current row. They are useful for tasks such as calculating running totals and ranking results. Here's an example of using the ROW_NUMBER function to rank customers by their total order amount:
```sql
SELECT customer_name, order_amount, 
       ROW_NUMBER() OVER (ORDER BY order_amount DESC) AS rank
FROM orders;
```
## What is difference between count and count (*)
  1. Count function require column to count data but count (*) will count all rows
  2. Count function do not count NULL values in column but count (*) will count all rows whether
  any column having null or not.

## What is difference between where and having clause
  1. Where clause is used to filter the row but having clause is used to filter groups
  2. We can use where clause with select, insert and update statements but having can be used
  only with select statement.
  3. Where clause comes before group and having always comes after the group in select
  statement.

## What is difference between stored procedure and user defined function
  There are following difference between stored procedure and user defined function
  a) We can use all DML command like insert, update and delete and select command in stored
  procedure but user defined function can use only select statement.
  b) Function must have to return a value but in case stored procedure it is not mandatory.
  c) We can call function from stored procedure but we can’t call stored procedure from function.

  d) We can use function in select statement and can use its output with select query but we can’t
  call stored procedure from select query. We need to use exec command to execute stored
  procedure.
  e) We can’t use transactions and exception handling in function but stored procedure support
  both transactions and exception handling.
  f) Function support only input parameter not ouput parameter but in stored procedure we can
  use both.
  g) User defined function can return only single value but stored procedure can return multiple
  value result set.
  
##  How to delete column from the table?
##  How to delete table in sql server

## SQL Commands are case sensitive or not
  No, sql commands are not case sensitive.

## What does Null Represent
  Null Represents undefined value

##  What is distinct
  Distinct is used to supress duplicate row in select query

## How to sort data in sql
  We use order by clause to sort data either in ascending or descending order

## What is the default order of sorting in sql
  Ascending is the default order

## What is Stored Procedure
  The stored procedure is a set of SQL Statements. It is precompiled object. Stored procedure
  increases the performance of the database as they are precompiled.

## What is trigger
  Triggers can be defined as an area of code Which executes in response of a particular action like
  insert, update, delete, Create, drop etc. Triggers executes automatically.

## What is the type of triggers
  We have two types of triggers
  a) DDL Triggers b) DML Trigger
  DML Triggers further categorized in following two category
  ● a) For trigger
  ● b) Instead of trigger
  
## Which operator is used to select null value
  We use IS NULL operator to select null value.

##  Which operator we use to match pattern
  We use like operator to match pattern.

## What is difference between primary key and unique key
  Difference between primary key and unique key are as follows: -
  a) We cannot enter null in primary key but we can have one null value in unique key column.

  b) When we create primary key cluster index created automatically but unique key non
  clustered index created automatically.
  c) Searching will be fast with the help of primary key as compare to unique key.
  d) A table can have only one primary key but we can have more than one unique key.
  
## Difference between Delete and Truncate
  Both commands are used to remove data from tables but they have following differences: -
  1. Delete is DML command but Truncate is DDL command.
  2. Delete command can be used with where clause if we need to delete specific row but
  truncate command doesn’t work with where clause so it removes all rows.
  3. Truncate set the identity from the beginning but delete not.
  4. Delete command delete row one by one and maintains its data in transaction log but truncate
  de allocates its data pages.
  5. Delete is slower than truncate as it has to maintains its each entry in transaction log.
  6. Delete can be roll backed but truncate not.
  7. Delete command activates all triggers if any associated but truncate not.
  Note: - delete and truncate both can be roll backed if used with transaction.
  
##  What is the difference between varchar and nvarchar?
## Write SQL Query to display the current date.
## Write SQL Query to display the current time.
## Write an SQL Query to find the year from date.
## What is CTE?
```sql
WITH year_metrics AS (
  SELECT
    YEAR(day) AS year,
    SUM(daily_amount) AS year_amount
  FROM sales
  GROUP BY YEAR(day)
)
INSERT INTO yearly_sales (year, year_amount)
SELECT year, year_amount
FROM year_metrics;
```
```sql
WITH category_discounts AS (
  SELECT
    category_id,
    AVG(discount) AS avg_discount
  FROM products
  GROUP BY category_id
)
UPDATE products
SET discount = cd.avg_discount
FROM products p
JOIN category_discounts cd
ON p.category_id = cd.category_id;

```
```sql
WITH old_logs AS (
  SELECT *
  FROM logs
  WHERE log_date < DATEADD(YEAR, -1, GETDATE())
)
DELETE FROM logs
WHERE log_id IN (SELECT log_id FROM old_logs);

```
```sql
CREATE VIEW yearly_sales_summary AS
WITH year_metrics AS (
  SELECT
    YEAR(day) AS year,
    SUM(daily_amount) AS total_sales,
    SUM(quantity_sold) AS total_products_sold
  FROM sales
  GROUP BY YEAR(day)
),
average_price AS (
  SELECT
    YEAR(s.day) AS year,
    AVG(p.price) AS avg_price
  FROM sales s
  JOIN products p ON s.product_id = p.product_id
  GROUP BY YEAR(s.day)
),
category_sales AS (
  SELECT
    YEAR(s.day) AS year,
    c.category_id,
    c.category_name,
    SUM(s.daily_amount) AS category_sales
  FROM sales s
  JOIN products p ON s.product_id = p.product_id
  JOIN categories c ON p.category_id = c.category_id
  GROUP BY YEAR(s.day), c.category_id, c.category_name
),
top_category_sales AS (
  SELECT
    year,
    category_id,
    category_name,
    category_sales,
    ROW_NUMBER() OVER (PARTITION BY year ORDER BY category_sales DESC) AS rank
  FROM category_sales
)
SELECT
  ym.year,
  ym.total_sales,
  ym.total_products_sold,
  ap.avg_price,
  tcs.category_name AS top_category,
  tcs.category_sales AS top_category_sales
FROM year_metrics ym
JOIN average_price ap ON ym.year = ap.year
JOIN top_category_sales tcs ON ym.year = tcs.year
WHERE tcs.rank = 1
ORDER BY ym.year;

```


## What is normalization?
## A Table Is Classified As A Parent Table And You Want To Drop And Re-create It.
How Would You Do This Without Affecting The Children Tables?
Name any three funciton in sql and usages?

## CLR functions 
can be used to access external resources such as files, network resources, Web Services, other databases (including remote instances of SQL Server). This can be achieved by using various classes in the .NET Framework, such as System.IO, System.WebServices, System.Sql, and so on. The assembly that contains such functions should at least be configured with the EXTERNAL_ACCESS permission set for this purpose. For more information, see CREATE ASSEMBLY (Transact-SQL).
## Machine Test for procedure validation
Write a procedure named SaveItem with two input parameters: ItemId of type int and mrp of type int. The procedure will perform a validation that If the mrp value is less than or equal to zero, an appropriate error or exception should be raised.

```sql
CREATE PROCEDURE SaveItem
    @ItemId INT,
    @mrp INT
AS
BEGIN
    -- Validation: Check if the MRP is greater than zero
    IF @mrp <= 0
    BEGIN
        RAISERROR('MRP must be greater than zero.', 16, 1);
    END
END

```
## Machine test for CTE

```sql


  CREATE TABLE [dbo].[Control]
(
    [controlId] [INT] IDENTITY(1, 1) NOT NULL,
    [keyname] [NVARCHAR](50) NULL,
    [keyname_value] [NVARCHAR](50) NULL
);

GO
CREATE TABLE [dbo].[product]
(
    [productid] [INT] IDENTITY(1, 1) NOT NULL,
    [productname] [NVARCHAR](50) NOT NULL,
    [remarks] [NVARCHAR](50) NULL
);

GO
INSERT [dbo].[Control]
(
    [keyname],
    [keyname_value]
)
VALUES
(N'productname', N'I Phone 12'),
(N'remarks', N'An Apple company product.');



```
## PIVOT

```sql

SELECT productname, remarks
FROM
(SELECT keyname, keyname_value FROM controltest) AS Source
PIVOT
(
    MAX(keyname_value)
    FOR keyname IN (productname, remarks)
) AS PivotTable;

```
## What is the use of the SET NOCOUNT function?
Ans: This function helps to stop the message that indicates how many rows are being affected while executing a T-SQL statement or stored procedure.

The syntax for the function is given as:

SET NOCOUNT { ON | OFF } 
If you set this function ON, then no count is returned in the result set; on the other hand, if you set this function OFF, then count is returned.


##  What do you mean by Magic Tables in SQL server?
Ans: Magic tables are virtual tables that exist in two types – INSERTED AND DELETED. They hold the information of the newly INSERTED and DELETED rows. The INSERTED table will have the newly inserted rows on top of it. The DELETED tables will have the recently deleted rows on top of it on similar tracks. Magic tables are stored in tempDB.

##  How can you prevent SQL injection vulnerabilities?
Ans: We can prevent SQL injection vulnerabilities in the following ways:

Using Type-Safe SQL parameters
Using parameterized input with stored procedures
Filtering inputs
Reviewing codes
Wrapping parameters


##  How can you use HAVING and WHERE clauses in a single query?
Ans: Generally, the WHERE Clause acts on individual rows, whereas the HAVING clause acts on groups. A SQL query can be constructed using the HAVING clause and WHERE clause. In that situation, WHERE Clause acts first based on the given conditions and groups rows in a table. Then, the HAVING clause acts on the groups and creates a result set only including the groups based on the given conditions.

##  How can you hold the Stored Procedure scripts in the SQL server?
Ans: We can store the stored procedure scripts in a server table known as Sys.SQL_Modules. Also, Sys. procedures table is used to store the name of the stored procedures.


##  Differentiate EXCEPT and INTERSECT commands?
Ans: These commands are used to return distinct rows by comparing the results of two separate queries.

EXCEPT: operator allows returning distinct rows from the left input query only.

INTERCEPT: operator allows returning distinct rows from both left and right input queries.

## Dynamic Pivot
```sql

EXEC dbo.GetPivotData @TableName = N'controltest',   
                 @KeyColumnName = N'keyname',  
                 @ValueColumnName = N'keyname_value', 
                 @ValueFunction = N'max'  

ALTER PROC GetPivotData
(
    @TableName NVARCHAR(50),
    @KeyColumnName NVARCHAR(50),
    @ValueColumnName NVARCHAR(50),
	@ValueFunction NVARCHAR(50) ='max'
)
AS
BEGIN



    DECLARE @Columns NVARCHAR(MAX),
            @SQL NVARCHAR(MAX);

    SET @SQL = N'SELECT @Columns =STRING_AGG( QUOTENAME(keyname), '','') FROM (SELECT DISTINCT keyname AS keyname  FROM ' + @TableName + ') as Source';

	PRINT @SQL;
    -- Execute the dynamic SQL statement
    EXECUTE sp_executesql @SQL,
                          N'@Columns NVARCHAR(MAX) OUTPUT',
                          @Columns OUTPUT;



    -- Build the dynamic SQL statement
    SET @SQL = N'SELECT ' + @Columns + N'
    FROM (
        SELECT ' + @KeyColumnName + N', ' + @ValueColumnName + N'
        FROM ' + @TableName + N'
    ) AS Source
    PIVOT (
        ' + @ValueFunction+'('  + @ValueColumnName + N')
        FOR '  + @KeyColumnName + N' IN (' + @Columns + N')
    ) AS PivotTable';

	PRINT @SQL;
    -- Execute the dynamic SQL statement
    EXEC (@SQL);

END;
```
