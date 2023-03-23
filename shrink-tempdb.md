# shrink-tempdb

## show size

```sql
SELECT name,
    file_id,
    type_desc,
    size * 8 / 1024 [TempdbSizeInMB]
FROM tempdb.sys.database_files
ORDER BY type_desc DESC,
    file_id;
```

## shrink


```sql
-- 64 number of mb
USE tempdb
GO 
DBCC SHRINKFILE (templog, 64)
GO
```
