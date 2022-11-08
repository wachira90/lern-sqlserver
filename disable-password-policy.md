# disable password policy


## command sql

```
USE master
GO

ALTER LOGIN [user1] WITH PASSWORD = 'p12345678'
GO

ALTER LOGIN [user1] WITH CHECK_POLICY = OFF, CHECK_EXPIRATION = OFF;
```
