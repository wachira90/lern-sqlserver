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

### ADDITION COMMAND
````
EXEC sp_dropserver '<old_name>';  
GO  
EXEC sp_addserver '<new_name>', local;  
GO  

EXEC sp_dropserver '<old_name\instancename>';  
GO  
EXEC sp_addserver '<new_name\instancename>', local;  
GO
````
