# Creating a Stored Procedure to create SQL Agent jobs

## sql command

````
USE [msdb]
GO
CREATE procedure [dbo].[sp_add_job_quick] 
@job nvarchar(128),
@mycommand nvarchar(max), 
@servername nvarchar(28),
@startdate nvarchar(8),
@starttime nvarchar(8)
as

--Add a job
EXEC dbo.sp_add_job
    @job_name = @job ;

--Add a job step named process step. This step runs the stored procedure
EXEC sp_add_jobstep
    @job_name = @job,
    @step_name = N'process step',
    @subsystem = N'TSQL',
    @command = @mycommand

--Schedule the job at a specified date and time
exec sp_add_jobschedule @job_name = @job,
@name = 'MySchedule',
@freq_type=1,
@active_start_date = @startdate,
@active_start_time = @starttime

-- Add the job to the SQL Server 
EXEC dbo.sp_add_jobserver
    @job_name =  @job,
    @server_name = @servername
````    


## This is a stored procedure named sp_add_job_quick that calls 4 msdb stored procedures:

1. `sp_add_job` creates a new job

2. `sp_add_jobstep` adds a new step in the job

3. `sp_add_jobschedule` schedules a job for a specific date and time

4. `sp_add_jobserver` adds the job to a specific server


## Let's invoke the stored procedure in order to create the job:


````
exec dbo.sp_add_job_quick 
@job = 'myjob', -- The job name
@mycommand = 'sp_who', -- The T-SQL command to run in the step
@servername = 'serverName', -- SQL Server name. If running locally, you can use @servername=@@Servername
@startdate = '20130829', -- The date August 29th, 2013
@starttime = '160000' -- The time, 16:00:00
````

If everything is OK, a job named myjob will be created with a step that runs the sp_who stored procedure that will run on August 29th at 4:00PM.

