# DISABLE TRIGGER

## WINDOWS AUTH
sqlcmd -S localhost -d master -A

## SPACIFIC USER AUTH
sqlcmd -S localhost -d master -A -U smedam

ENTER PASSWORD

## DISABLE
DISABLE TRIGGER trgAudit_LoginHistory ON ALL SERVER

## ENABLE
enable trigger tr_logon on all server
  
## LIST
select * from master.sys.server_triggers
