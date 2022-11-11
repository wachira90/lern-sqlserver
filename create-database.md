# CREATE DATABASE

## CREATE SCRIPT

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

## CHECK CURRENT COLLATE

````
SELECT name, collation_name FROM sys.databases WHERE name = 'sqltestdb';
````
