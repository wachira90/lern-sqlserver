# memory-setting

## set command

```sql
EXEC sys.sp_configure N'min server memory (MB)', N'2048'
GO
EXEC sys.sp_configure N'max server memory (MB)', N'6144'
GO
RECONFIGURE WITH OVERRIDE
GO
```

## in gui right instance => memory 
