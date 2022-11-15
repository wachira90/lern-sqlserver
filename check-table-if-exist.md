# CHECK TABLE IF EXIST

## BY SCHEMA

````
USE [testdb]
GO
IF (EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'dbo' AND TABLE_NAME = 'DestinationTableName'))
   BEGIN
      PRINT 'Database Table Exists'
   END;
ELSE
   BEGIN
      PRINT 'No Table in database'
   END;
````   

## Using OBJECT_ID() function

````
USE [testdb]
GO
IF OBJECT_ID('model.dbo.DestinationTableName') IS NOT NULL
   BEGIN
      PRINT 'Database Table Exists'
   END;
ELSE
   BEGIN
      PRINT 'No Table in database'
   END;
````
