# Monitor transaction log growth

````
USE [testdb]
GO

SELECT name AS [File Name],
    physical_name AS [Physical Name],
    size / 128.0 AS [Total Size in MB],
    size / 128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int) / 128.0 AS [Available Space In MB],
    [growth],
    [file_id]
FROM sys.database_files
WHERE type_desc = 'LOG'
````

You can also use DBCC SQLPERF (‘logspace’) which has been around for a while. This command displays useful details such as DB name, Log Size (MB) and Log Space Used (%):
````
DBCC SQLPERF ('logspace')
````
