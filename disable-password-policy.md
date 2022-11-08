# disable password policy

## From error

```
Alter failed for login 'somelogin'.

An exception occurred while executing a Transact-SQL statement or batch.

The CHECK_POLICY and CHECK_EXPIRATION options cannot be turned OFF when MUST_CHANGE is ON. (Microsoft SQL Server, Error: 15128)
```

## Command sql

```
USE master
GO

ALTER LOGIN [user1] WITH PASSWORD = 'p12345678'
GO

ALTER LOGIN [user1] WITH CHECK_POLICY = OFF, CHECK_EXPIRATION = OFF;
```
