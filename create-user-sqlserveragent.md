# create user for sqlserver agent


## sql command create user by password
```sql
USE [master]
GO
CREATE LOGIN [sqlserveragent] WITH PASSWORD=N'password1234', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF
GO
USE [msdb]
GO
CREATE USER [sqlserveragent] FOR LOGIN [sqlserveragent]
GO
USE [msdb]
GO
ALTER ROLE [SQLAgentOperatorRole] ADD MEMBER [sqlserveragent]
GO
USE [msdb]
GO
ALTER ROLE [SQLAgentReaderRole] ADD MEMBER [sqlserveragent]
GO
USE [msdb]
GO
ALTER ROLE [SQLAgentUserRole] ADD MEMBER [sqlserveragent]
GO
```
