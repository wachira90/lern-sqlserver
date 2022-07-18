# DROP NAME INTANCES

## CHECK OLD SERVER NAME
````
SELECT @@SERVERNAME AS 'Server Name';  
````

## DELETE OLD NAME 

````
EXEC sp_dropserver 'oldservername';  
GO
````

## ADD NEW NAME
````
EXEC sp_addserver 'newservername', local;  
GO  

EXEC sp_addserver 'SQL2019', local;  
GO 
````

## RESTART SERVICE SQLSERVER
