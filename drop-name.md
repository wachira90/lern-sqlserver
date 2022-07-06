# DROP NAME INTANCES

## DELETE OLD NAME 

````
EXEC sp_dropserver 'oldservername';  
GO
````

## ADD NEW NAME AND RESTART SERVICE
````
EXEC sp_addserver 'newservername', local;  
GO  

EXEC sp_addserver 'SQL2019', local;  
GO 
````
