# Advance

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
