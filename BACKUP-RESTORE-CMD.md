# BACKUP RESTORE CMD

## RESTORE SQL

```sql
USE [master]
GO
ALTER DATABASE [AnalyticsDB] SET SINGLE_USER WITH ROLLBACK IMMEDIATE 
RESTORE DATABASE [AnalyticsDB]
FROM DISK = N'F:\jam-data\uat_AnalyticsDB_20230330.bak' WITH FILE = 1,
    MOVE N'AnalyticsDB' TO N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\AnalyticsDB.mdf',
    MOVE N'AnalyticsDB_log' TO N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\AnalyticsDB_log.ldf', NOUNLOAD, REPLACE, STATS = 5
ALTER DATABASE [AnalyticsDB] SET MULTI_USER
GO
```

## RESTORE SHORT SQL

```sql
USE [master]
RESTORE DATABASE [AnalyticsDB] FROM  DISK = N'F:\jam-data\uat_AnalyticsDB_20230330.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE,  STATS = 5
GO
```

## BACKUP SQL

```sql
USE [AnalyticsDB]
GO
BACKUP DATABASE [AnalyticsDB] TO  DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\AnalyticsDB_20230330.bak' WITH NOFORMAT, NOINIT,  NAME = N'AnalyticsDB-Full Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
GO
```
