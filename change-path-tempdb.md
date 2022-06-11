# change path tempdb

## check current path

````
Use master
GO

SELECT 
name AS [LogicalName]
,physical_name AS [Location]
,state_desc AS [Status]
FROM sys.master_files
WHERE database_id = DB_ID(N'tempdb');
GO
````



## Change the location of TempDB Data and Log files using ALTER DATABASE

````

USE master;
GO

ALTER DATABASE tempdb 
MODIFY FILE (NAME = tempdev, FILENAME = 'T:\MSSQL\DATA\tempdb.mdf');
GO

ALTER DATABASE tempdb 
MODIFY FILE (NAME = templog, FILENAME = 'T:\MSSQL\DATA\templog.ldf');
GO
````


## Verify the File Change

````
Use master
GO

SELECT 
name AS [LogicalName]
,physical_name AS [Location]
,state_desc AS [Status]
FROM sys.master_files
WHERE database_id = DB_ID(N'tempdb');
GO
````
