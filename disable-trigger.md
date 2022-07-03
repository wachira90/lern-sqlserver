# DISABLE TRIGGER

## WINDOWS AUTH
sqlcmd -S localhost -d master -A

## SPACIFIC USER AUTH
sqlcmd -S localhost -d master -A -U smedam

<passhere>

## DISABLE
DISABLE TRIGGER trgAudit_LoginHistory ON ALL SERVER

## ENABLE
enable trigger tr_logon on all server
  
  
