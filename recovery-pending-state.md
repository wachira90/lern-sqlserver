# Recovery Pending State

## check

```sql
SELECT name, state_desc from sys.databases 
GO
```

## run by

```sql
USE [AnalyticsDB]
GO

ALTER DATABASE [AnalyticsDB] SET EMERGENCY;
GO

ALTER DATABASE [AnalyticsDB] set single_user
GO

DBCC CHECKDB ([AnalyticsDB], REPAIR_ALLOW_DATA_LOSS) WITH ALL_ERRORMSGS;
GO

ALTER DATABASE [AnalyticsDB] set multi_user
GO
```
