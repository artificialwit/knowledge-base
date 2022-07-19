# Advance

#### Get List of column of table type
```sql
DECLARE @tableTypeName VARCHAR(100) = 'tvpControl';

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
