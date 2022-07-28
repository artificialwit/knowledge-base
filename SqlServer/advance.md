# Advance

#### ROW_NUMBER()
```sql

SELECT  ROW_NUMBER() OVER (PARTITION BY empType ORDER BY templateName), * FROM employees
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

### To get current date from database, must use
```sql
    GETUTCDATE()
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
