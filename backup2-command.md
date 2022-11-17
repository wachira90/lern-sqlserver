# Creating a backup using SQL Server Command Line (T-SQL)

## Overview

Creating command line backups is very straightforward.  There are basically two commands that allow you to create backups, BACKUP DATABASE and BACKUP LOG.

## Explanation

Here are some simple examples on how to create database and log backups using T-SQL.  This is the most basic syntax that is needed to create backups to disk.

### Create a SQL Server full backup

````
BACKUP DATABASE AdventureWorks 
TO DISK = 'C:\AdventureWorks.BAK'
GO
````

### Create a SQL Server transaction log backup

````
BACKUP LOG AdventureWorks 
TO DISK = 'C:\AdventureWorks.TRN'
GO
````

This is basically all you need to do to create the backups.  There are other options that can be used, but to create a valid and useable backup file this is all that needs to be done.

