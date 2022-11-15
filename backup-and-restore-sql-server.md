# Backup and Restore SQL Server

This article describes the basics of backup and restore a SQL Server database.
T-SQL statements allow to back up and restore your SQL SERVER database.
Also, you can export and import security certificates and keys.

## BACKUP DATABASE

The T-SQL statement BACKUP DATABASE is used to backup entire database to disk file

````
USE model;
GO
BACKUP DATABASE model
TO DISK = 'E:\SQLServerBackup\model.bak'
WITH FORMAT,
MEDIANAME = 'SQLServerBackup',
NAME = 'Full Backup of model database';
GO
````

## PARTIAL BACKUPS

The T-SQL statement BACKUP DATABASE READ_WRITE_FILEGROUPS is used to backup partial backup to disk file.

````
USE model;
GO
BACKUP DATABASE model READ_WRITE_FILEGROUPS
TO DISK = 'E:\SQLServerBackup\model_partial.bak'
GO
````

## RESTORE DATABASE

The T-SQL statement RESTORE DATABASE is used to restore a SQL Server database.

````
USE model;
GO
RESTORE DATABASE model
FROM DISK = 'E:\SQLServerBackup\model.bak'
GO
````

## RESTORE DATABASE WITH DIFFERENTIAL

The T-SQL statement RESTORE DATABASE WITH DIFFERENTIAL is used to restore full and differential database backup

````
--backup database with Differential
USE model;
GO
BACKUP DATABASE model
TO DISK = 'E:\SQLServerBackup\model_1.bak'
WITH DIFFERENTIAL;
GO

--restore database model
RESTORE DATABASE model
FROM DISK = 'E:\SQLServerBackup\model_1.bak'
GO
````
