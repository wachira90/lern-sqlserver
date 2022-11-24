# DATABASE MAIL

````
USE [msdb]
GO

-- ENABLE FEATURE
sp_configure 'Database Mail XPs', 1;
GO
RECONFIGURE
GO
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO


-- Create a Database Mail profile  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'Notifications',  
    @description = 'Profile used for sending outgoing notifications using Gmail.' ;  
GO


-- Grant access to the profile to the DBMailUsers role  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'Notifications',  
    @principal_name = 'public',  
    @is_default = 1 ;
GO


-- Create a Database Mail account  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'Gmail',  
    @description = 'Mail account for sending outgoing notifications.',  
    @email_address = 'Use a valid e-mail address',  
    @display_name = 'Automated Mailer',  
    @mailserver_name = 'smtp.gmail.com',
    @port = 465,
    @enable_ssl = 1,
    @username = 'Use a valid e-mail address',
    @password = 'Use the password for the e-mail account above' ;  
GO


-- Add the account to the profile  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'Notifications',  
    @account_name = 'Gmail',  
    @sequence_number =1 ;  
GO


-- roll back the changes:====
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp @profile_name = 'Notifications'
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp @profile_name = 'Notifications'
EXECUTE msdb.dbo.sysmail_delete_account_sp @account_name = 'Gmail'
EXECUTE msdb.dbo.sysmail_delete_profile_sp @profile_name = 'Notifications'


--Test Database Mail configuration
EXEC msdb.dbo.sp_send_dbmail
    @profile_name = 'Notifications',
    @recipients = 'Use a valid e-mail address',
    @body = 'The database mail configuration was completed successfully.',
    @subject = 'Automated Success Message';
GO


-- Troubleshooting Database Mail
sp_configure 'show advanced', 1; 
GO
RECONFIGURE;
GO
sp_configure;
GO


-- The Database Mail system logs e-mail
SELECT * FROM msdb.dbo.sysmail_event_log;
````

FROM => https://www.sqlshack.com/configure-database-mail-sql-server/
