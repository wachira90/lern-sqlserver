# error audit 

## error message
````
Logon failed for login 'sa' due to trigger execution.
Changed database context to 'master'.
Changed language setting to us_english. (Microsoft SQL Server, Error: 17892)
````

## login 
````
C:adrian> sqlcmd -S LocalHost -d master -A
 1>
 ````
 
 ## find trigger name
 
 ````
  C:Usersadrian>sqlcmd -S LocalHost -d master -A
SELECT
    SSM.definition
FROM
    sys.server_triggers AS ST JOIN
    sys.server_sql_modules AS SSM
         ON ST.object_id = SSM.object_id
         GO
````

## result trigger
````
definition

CREATE TRIGGER TEST_JOB
ON ALL SERVER WITH EXECUTE AS 'sharepointMonitor'
FOR LOGON
AS
BEGIN
        DECLARE @statusJob VARCHAR(10)
        DECLARE @lb_Exit BIT
        SET @lb_Exit = 0;
        DECLARE Jobs CURSOR LOCAL FOR
                SELECT LastRunStatus
                FROM dbo.nag
````


## delete trigger
````
DROP TRIGGER TEST_JOB ON ALL SERVER
````
