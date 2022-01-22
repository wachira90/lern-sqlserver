# shrink log

## command

````
ALTER DATABASE AdventureWorks
SET RECOVERY SIMPLE
GO
DBCC SHRINKFILE (AdventureWorks_log, 1)
GO
ALTER DATABASE AdventureWorks
SET RECOVERY FULL
````
