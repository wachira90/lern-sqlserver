# auto shrink database

## create store procedure

````
USE [testdb]
GO
CREATE PROCEDURE sp_shrinkdb
AS
	BEGIN
		DECLARE @DBNAME VARCHAR(255);
		SET @DBNAME = 'testdb'
		DECLARE @SIMPLE_TEMPLATE VARCHAR(MAX)
		DECLARE @SHRINKLOG_TEMPLATE VARCHAR(MAX)
		DECLARE @FULL_TEMPLATE VARCHAR(MAX)
		SET @SIMPLE_TEMPLATE = 'ALTER DATABASE {DBNAME} SET RECOVERY SIMPLE'
		SET @SHRINKLOG_TEMPLATE='DBCC SHRINKFILE( {DBNAME}_Log , 1)'
		SET @FULL_TEMPLATE='ALTER DATABASE {DBNAME} SET RECOVERY FULL'
		DECLARE @SQL_SCRIPT VARCHAR(MAX)
		SET @SQL_SCRIPT = REPLACE(@SIMPLE_TEMPLATE, '{DBNAME}', @DBNAME)
		EXECUTE (@SQL_SCRIPT)
		SET @SQL_SCRIPT = REPLACE(@SHRINKLOG_TEMPLATE, '{DBNAME}', @DBNAME)
		EXECUTE (@SQL_SCRIPT)
		SET @SQL_SCRIPT = REPLACE(@FULL_TEMPLATE, '{DBNAME}', @DBNAME)
		EXECUTE (@SQL_SCRIPT)
	END
GO
````

## run store procedure

````
EXEC sp_shrinkdb
````

## check size

````
SELECT name AS [File Name],
    physical_name AS [Physical Name],
    size / 128.0 AS [Total Size in MB],
    size / 128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int) / 128.0 AS [Available Space In MB],
    [growth],
    [file_id]
FROM sys.database_files
WHERE type_desc = 'LOG'
````




