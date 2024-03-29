# CREATE DATABASE

## CREATE SCRIPT

### LINUX

````
USE [master]
GO

CREATE DATABASE [sqltestdb] ON PRIMARY (
  NAME = N'sqltestdb',
  FILENAME = N'/var/opt/mssql/data/sqltestdb.mdf',
  SIZE = 8192KB,
  FILEGROWTH = 65536KB
) LOG ON (
  NAME = N'sqltestdb_log',
  FILENAME = N'/var/opt/mssql/data/sqltestdb_log.ldf',
  SIZE = 8192KB,
  FILEGROWTH = 65536KB
)
COLLATE Thai_CI_AS
GO
````

### WINDOWS

````
USE [master]
GO

CREATE DATABASE [sqltestdb] ON PRIMARY (
  NAME = N'sqltestdb',
  FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\sqltestdb.mdf',
  SIZE = 8192KB,
  FILEGROWTH = 65536KB
) LOG ON (
  NAME = N'sqltestdb_log',
  FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\sqltestdb_log.ldf',
  SIZE = 8192KB,
  FILEGROWTH = 65536KB
)
COLLATE Thai_CI_AS
GO
````

## CHECK CURRENT COLLATE

````
USE [sqltestdb]
GO
SELECT name, collation_name FROM sys.databases WHERE name = 'sqltestdb';
````

## CHECK CURRENT FILE PATH

````
SELECT name as [Logical_name], physical_name as [physical file name] FROM sys.database_files

````
