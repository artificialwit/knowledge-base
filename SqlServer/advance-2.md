## Generating formatted number based on prefix and datetime
```sql
CREATE FUNCTION dbo.GetDisplayNumber
(
    @TableName NVARCHAR(128),
    @Prefix NVARCHAR(50),
    @DateFormat NVARCHAR(50)
)
RETURNS NVARCHAR(255)
AS
BEGIN
    DECLARE @DisplayNumber NVARCHAR(255);
    SET @DisplayNumber
        = @Prefix + N'-' + FORMAT(GETUTCDATE(), @DateFormat) + N'-'
          + CAST(ISNULL(IDENT_CURRENT(@TableName), 0) + 1 AS NVARCHAR);

    RETURN @DisplayNumber;
END;
GO

SELECT dbo.GetDisplayNumber('TKT.Tickets', 'TKT', 'yyyy-MM-dd') -- TKT-2024-12-23-350
SELECT dbo.GetDisplayNumber('TKT.Tickets', 'TKT', 'yyyy-MM') -- TKT-2024-12-350
SELECT dbo.GetDisplayNumber('TKT.Tickets', 'TKT', 'yyyy') -- TKT-2024-350
SELECT dbo.GetDisplayNumber('Mst.Task', 'TSK', 'yyyy-MM-dd') -- TKT-2024-350

```
