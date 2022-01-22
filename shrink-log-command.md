# Shrink log


## Shrink the log using TSQL

If the database is in the SIMPLE recovery model you can use the following statement to shrink the log file:

````
DBCC SHRINKFILE (AdventureWorks_log, 1)
````

## Command

If the database is in the FULL recovery model you can change the following 

````
ALTER DATABASE AdventureWorks
SET RECOVERY SIMPLE
GO
DBCC SHRINKFILE (AdventureWorks_log, 1)
GO
ALTER DATABASE AdventureWorks
SET RECOVERY FULL
````

## You can find the logical name of the log file by using the following query:
````
SELECT name FROM sys.master_files WHERE type_desc = 'LOG'
````

Another option to shrink the log using the FULL recovery model is to backup the log for your database using the BACKUP LOG statement and then issue the SHRINKFILE command to shrink the transaction log:
````
BACKUP LOG AdventureWorks TO BackupDevice
````
