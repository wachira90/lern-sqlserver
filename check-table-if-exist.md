# CHECK TABLE IF EXIST


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
