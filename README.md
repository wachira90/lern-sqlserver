# lern-sqlserver
lerning sqlserver


## shrink log

````
ALTER DATABASE AdventureWorks
SET RECOVERY SIMPLE
GO
DBCC SHRINKFILE (AdventureWorks_log, 1)
GO
ALTER DATABASE AdventureWorks
SET RECOVERY FULL
````

## Growth 1MB

````
SELECT 'ALTER DATABASE [' + db_name(s.database_id) + '] MODIFY FILE ( NAME = N''' + s.name + ''', FILEGROWTH = 1MB)' as ToExecute
FROM sys.master_files s
	INNER JOIN sys.databases db ON s.database_id = db.database_id
where (
		s.is_percent_growth = 1
		or s.growth * 8.0 / 1024 < 10
)
and db.state_desc = 'online'
ORDER BY s.database_id
````
