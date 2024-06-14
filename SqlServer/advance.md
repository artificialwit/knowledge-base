# Advance
### Running total
```sql
SELECT date, sales, SUM(sales) OVER (ORDER BY date) AS running_total
FROM
sales_data;
```
### Ranking Rows Based on a Specific Ordering Criteria
```sql
WITH employee_ranking AS (
  SELECT
    employee_id,
    last_name,
    first_name,
    salary,
    RANK() OVER (ORDER BY salary DESC) as ranking
  FROM employee
)
SELECT
  employee_id,
  last_name,
  first_name,
  salary
FROM employee_ranking
WHERE ranking <= 5
ORDER BY ranking
```
### List the Second Highest Salary By Department
```sql
WITH employee_ranking AS (
  SELECT
    employee_id,
    last_name,
    first_name,
    salary,
    dept_id
    RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) as ranking
  FROM employee
)
SELECT
  dept_id,
  employee_id,
  last_name,
  first_name,
  salary
FROM employee_ranking
WHERE ranking = 2
ORDER BY dept_id, last_name

```

### List the First 50% Rows in a Result Set
```sql
WITH employee_ranking AS (
  SELECT
    employee_id,
    last_name,
    first_name,
    salary,
    NTILE(2) OVER (ORDER BY salary ) as ntile
  FROM employee
)
SELECT
  employee_id,
  last_name,
  first_name,
  salary
FROM employee_ranking
WHERE ntile = 1
ORDER BY salary
```

### Number the Rows in a Result Set
```sql
SELECT
  employee_id,
  last_name,
  first_name,
  salary,
  ROW_NUMBER() OVER (ORDER BY employee_id) as ranking_position
FROM employee
```

### Employees with Salaries Higher Than Their Departmental Average
```sql
SELECT
  first_name,
  last_name,
  salary
FROM employee e1
WHERE salary >
    (SELECT AVG(salary)
     FROM employee e2
     WHERE e1.departmet_id = e2.department_id)
```

### Find Common Records Between Tables
```sql
SELECT
  last_name,
  first_name
FROM employee
INTERSECT
SELECT
  last_name,
  first_name
FROM employee_2020_jan
```

### Grouping Data with ROLLUP
```sql
SELECT
  dept_id,
  expertise,
  SUM(salary) total_salary
FROM employee
GROUP BY ROLLUP (dept_id, expertise)
```

### Compute a Moving Average in SQL
```sql
SELECT
  day,
  daily_amount,
  AVG (daily_amount) OVER (ORDER BY day ROWS 6 PRECEDING)
    AS moving_average
FROM sales
```

### Compute a Difference (Delta) Between Two Columns on Different Rows
Let’s suppose we want to obtain a report with the total amount sold on each day, but we also want to obtain the difference (or delta) related to the previous day.
```sql
SELECT
  day,
  daily_amount,
  daily_amount - LAG(daily_amount) OVER (ORDER BY day)
    AS delta_yesterday_today
FROM sales

```

### Compute a Year-Over-Year Difference
```sql
WITH year_metrics AS (
  SELECT
    extract(year from day) as year,
    SUM(daily_amount) as year_amount
  FROM sales
  GROUP BY year)
SELECT
  year,
  year_amount,
  LAG(year_amount) OVER (ORDER BY year) AS revenue_previous_year,
  year_amount - LAG(year_amount) OVER (ORDER BY year) as yoy_diff_value,
  ((year_amount - LAG(year_amount) OVER (ORDER BY year) ) /
     LAG(year_amount) OVER (ORDER BY year)) as yoy_diff_perc
FROM year_metrics
ORDER BY 1

```
### Compute a Year-Over-Year Difference
```sql
WITH year_metrics
AS (SELECT YEAR(CreatedDate) AS year,
           SUM(Amount) AS year_amount
    FROM dbo.PurchaseOrder
    GROUP BY YEAR(CreatedDate))
SELECT year,
       year_amount,
       LAG(year_amount) OVER (ORDER BY year) AS revenue_previous_year,
       year_amount - LAG(year_amount) OVER (ORDER BY year) AS yoy_diff_value,
       CASE
           WHEN LAG(year_amount) OVER (ORDER BY year) = 0 THEN
               NULL
           ELSE
       ((year_amount - LAG(year_amount) OVER (ORDER BY year)) * 1.0 / LAG(year_amount) OVER (ORDER BY year))
       END AS yoy_diff_perc
FROM year_metrics
ORDER BY year;

```

### Use Recursive Queries to Manage Data Hierarchies
list of all category under (directly or indirectly) to the main category 
```sql
WITH subordinate
AS (SELECT CategoryId,
           CategoryName,
           ParentCategoryId
    FROM Mst.Category
    WHERE CategoryId = 141 -- id of the top hierarchy category (Furniture & Fixtures)

    UNION ALL
    SELECT e.CategoryId,
           e.CategoryName,
           e.ParentCategoryId
    FROM Mst.Category e
        JOIN subordinate s
            ON e.ParentCategoryId = s.CategoryId)
SELECT *
FROM subordinate;

```
### Generate duplicate records

```sql

-- Create a CTE with numbers from 1 to 50
WITH NumberSequence AS (
    SELECT 1 AS Number
    UNION ALL
    SELECT Number + 1
    FROM NumberSequence
    WHERE Number < 50
)
-- Perform a cross join with DummyUser
SELECT *
FROM CFG.Users
CROSS JOIN NumberSequence;


```
### Paging

```sql

ALTER PROCEDURE usp_GetAssets
(
    @pageIndex INT,
    @pageSize INT
)
AS
/*
EXEC dbo.usp_GetAssets @pageIndex = 1,                    -- int
                             @pageSize = 30                     -- int
                             

*/
BEGIN
    DECLARE @OffsetRows INT;
    SET @OffsetRows = (@pageIndex - 1) * @pageSize;


    SELECT *,
           totalRecord
    FROM
    (
        SELECT COUNT(*) OVER () AS totalRecord,
               *,
               ROW_NUMBER() OVER (ORDER BY AssetId) AS RowNum
        FROM usp_AssetViewTrackerDiscard
    ) AS SubQuery
    WHERE RowNum > @OffsetRows
    ORDER BY AssetId OFFSET @OffsetRows ROWS FETCH NEXT @pageSize ROWS ONLY;

END;

```
### ROW_NUMBER()
```sql

SELECT  ROW_NUMBER() OVER (PARTITION BY empType ORDER BY templateName), * FROM employees
```

### Returning the database ID of the current database
```sql
SELECT DB_ID() AS [Database ID];  
GO
```

### Returning the database ID of a specified database
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO
```

### Use of DB_ID and OBJECT_ID
```sql
DECLARE @db_id INT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO
```

### Returning the current database name
```sql
SELECT DB_NAME() AS [Current Database];  
GO
```

### Returning the database name of a specified database ID
```sql
USE master;  
GO  
SELECT DB_NAME(3) AS [Database Name];  
GO
```

#### Get List of column of table type
```sql
DECLARE @tableTypeName VARCHAR(100) = 'tvpEmployeeTableType';

SELECT t.name [TableTypeName],
       SCHEMA_NAME(t.schema_id) [SchemaName],
       c.name [Column Name],
       y.name [Data Type],
       c.max_length,
       c.precision,
       c.is_identity,
       c.is_nullable
FROM sys.table_types t
    INNER JOIN sys.columns c
        ON c.object_id = t.type_table_object_id
    INNER JOIN sys.types y
        ON y.system_type_id = c.system_type_id
           AND y.system_type_id = y.user_type_id
WHERE t.is_user_defined = 1
      AND t.is_table_type = 1
      AND t.name LIKE @tableTypeName;
    
```

#### Drop temporary table if exist check as good practice
```sql
    IF OBJECT_ID('tempdb..#tmp') IS NOT NULL    
        DROP TABLE #tmp;  
```

#### Return the first non-null value in a list
```sql
    SELECT COALESCE(NULL, NULL, NULL, 'W3Schools.com', NULL, 'Example.com');
```

### @@IDENTITY and SCOPE_IDENTITY()
The Sales.Customer table has a maximum identity value of 29483. If you insert a row into the table, @@IDENTITY and SCOPE_IDENTITY() return different values. SCOPE_IDENTITY() returns the value from the insert into the user table, whereas @@IDENTITY returns the value from the insert into the replication system table. Use SCOPE_IDENTITY() for applications that require access to the inserted identity value.
```sql
INSERT INTO Sales.Customer ([TerritoryID],[PersonID]) VALUES (8,NULL);  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO
```

### Find a text within all procedure 

```sql
 SELECT *
          FROM sys.procedures
          WHERE OBJECT_DEFINITION(object_id) LIKE '%token%'
```

### NULL IF and INULL function use

```sql
SELECT *
FROM employees 
    WHERE empId = ISNULL(NULLIF(@empId, 0), empId)
    
```

### UTC Date for multiple country product
```sql
    SET @TodayDate = GETUTCDATE();
````


### New GUID
```sql
SELECT NEWID()
```


### SQL Templating and PIVOT using json
An example of OPENJSON , Cursor and dynamic sql with parameter 

```sql
  
CREATE PROC usp_GetRenderedTemplates  
(  
    @DataSql NVARCHAR(MAX) = '', -- Either provide @DataSql or @JsonData with array brackets  
    @JsonData NVARCHAR(MAX) = '',  
    @TemplateHeader NVARCHAR(MAX) = '',  
    @TemplateBody NVARCHAR(MAX) = '',  
    @TemplateFooter NVARCHAR(MAX) = ''  
)  
AS  
BEGIN  

  
 IF @DataSql = ''  
       AND @JsonData = ''  
    BEGIN  
        RAISERROR('Please provide either @DataSql string or @JsonData.', 16, 1);  
  RETURN;  
    END;  
  
    DECLARE @MarkedKey NVARCHAR(100),  
            @SqlString NVARCHAR(MAX),  
            @KeyValue NVARCHAR(MAX);  
  
    IF @DataSql <> ''  
    BEGIN  
        SET @SqlString = N'SET @JsonData = (' + @DataSql + N' FOR JSON PATH)';  
  
        EXEC sp_executesql @SqlString,  
                           N'@JsonData NVARCHAR(MAX) OUTPUT',  
                           @JsonData = @JsonData OUTPUT;  
    END;  
     
  
    SELECT @JsonData AS jsondata;  
    -- to get first value  
    SELECT @JsonData = Value  
    FROM OPENJSON(@JsonData);  
  
  
    DECLARE jsonDataCursor CURSOR FOR  
    SELECT '{{' + [Key] + '}}' AS markedKey,  
           Value  
    FROM OPENJSON(@JsonData);  
  
    OPEN jsonDataCursor;  
    FETCH NEXT FROM jsonDataCursor  
    INTO @MarkedKey,  
         @KeyValue;  
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        SET @TemplateHeader = REPLACE(@TemplateHeader, @MarkedKey, @KeyValue);  
        SET @TemplateBody = REPLACE(@TemplateBody, @MarkedKey, @KeyValue);  
        SET @TemplateFooter = REPLACE(@TemplateFooter, @MarkedKey, @KeyValue);  
        FETCH NEXT FROM jsonDataCursor  
        INTO @MarkedKey,  
             @KeyValue;  
    END;  
  
    CLOSE jsonDataCursor;  
    DEALLOCATE jsonDataCursor;  
  
    SELECT @TemplateHeader AS TemplateHeader,  
           @TemplateBody AS TemplateBody,  
           @TemplateFooter AS TemplateFooter;  
  
END;
```

### ISJSON

- VALUE	Tests for a valid JSON value. This can be a JSON object, array, number, string or one of the three literal values (false, true, null)
- ARRAY	Tests for a valid JSON array
- OBJECT	Tests for a valid JSON object
- SCALAR	Tests for a valid JSON scalar – number or string
```sql
SELECT ISJSON('"test string"', SCALAR)
```


### JSON_OBJECT

```sql
SELECT JSON_OBJECT('name':'value', 'type':1)

--{"name":"value","type":1}

SELECT JSON_OBJECT('name':'value', 'type':NULL ABSENT ON NULL)

--{"name":"value"}

SELECT JSON_OBJECT('name':'value', 'type':JSON_ARRAY(1, 2))

-- {"name":"value","type":[1,2]}

SELECT s.session_id, JSON_OBJECT('security_id':s.security_id, 'login':s.login_name, 'status':s.status) as info
FROM sys.dm_exec_sessions AS s
WHERE s.is_user_process = 1;


```

### JSON_VALUE

```json
{"multicast_id":7037728382576867291,"success":1,"failure":0,"canonical_ids":0,"results":[{"message_id":"0:1661961941672938%0dc0a11e0dc0a11e"}]}
```

```sql

    SELECT @SuccessStatus = JSON_VALUE(@ResponseJson, '$.success');
    SELECT @FCMResponseID = JSON_VALUE(@ResponseJson, '$.results[0].message_id');

```
This example assumes that a table named Person.Person contains a jsonInfo column of JSON text
```sql
SELECT FirstName, LastName,
 JSON_VALUE(jsonInfo,'$.info.address.town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address.state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address.town')
````

### Compare JSON_VALUE and JSON_QUERY
The key difference between JSON_VALUE and JSON_QUERY is that JSON_VALUE returns a scalar value, while JSON_QUERY returns an object or an array
```json
{
	"a": "[1,2]",
	"b": [1, 2],
	"c": "hi"
}
```
Path | JSON_VALUE  returns |	JSON_QUERY returns
--- | --- | --- 
$	| NULL or error |	{ "a": "[1,2]", "b": [1,2], "c":"hi"}
$.a	 |[1,2]	| NULL or error
$.b	 | NULL or error |	[1,2]
$.b[0] | 	1 |	NULL or error
$.c | 	hi |	NULL or error

### JSON_MODIFY
```sql
JSON_MODIFY ( expression , path , newValue )  

UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,'$.info.address.town','London')
WHERE EmployeeID=17
```

### JSON_PATH_EXISTS
```sql
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{"info":{"address":[{"town":"Paris"},{"town":"London"}]}}';

SELECT JSON_PATH_EXISTS(@jsonInfo,'$.info.address'); -- 1
```
### Performace
```sql
SET STATISTICS IO { ON | OFF }

https://statisticsparser.com/
```
