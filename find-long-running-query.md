# find long running query

## example 1

```sql
SELECT DISTINCT TOP 20 est.TEXT AS QUERY,
    Db_name(dbid),
    eqs.execution_count AS EXEC_CNT,
    eqs.max_elapsed_time AS MAX_ELAPSED_TIME,
    ISNULL(
        eqs.total_elapsed_time / NULLIF(eqs.execution_count, 0),
        0
    ) AS AVG_ELAPSED_TIME,
    eqs.creation_time AS CREATION_TIME,
    ISNULL(
        eqs.execution_count / NULLIF(DATEDIFF(s, eqs.creation_time, GETDATE()), 0),
        0
    ) AS EXEC_PER_SECOND,
    total_physical_reads AS AGG_PHYSICAL_READS
FROM sys.dm_exec_query_stats eqs
    CROSS APPLY sys.dm_exec_sql_text(eqs.sql_handle) est
ORDER BY eqs.max_elapsed_time DESC 
```

## example 2

```sql
SELECT creation_time,
    last_execution_time,
    total_physical_reads,
    total_logical_reads,
    total_logical_writes,
    execution_count,
    total_worker_time,
    total_elapsed_time,
    total_elapsed_time / execution_count avg_elapsed_time,
    SUBSTRING(
        st.text,
        (qs.statement_start_offset / 2) + 1,
        (
            (
                CASE
                    statement_end_offset
                    WHEN -1 THEN DATALENGTH(st.text)
                    ELSE qs.statement_end_offset
                END - qs.statement_start_offset
            ) / 2
        ) + 1
    ) AS statement_text
FROM sys.dm_exec_query_stats AS qs
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) st
ORDER BY total_elapsed_time / execution_count DESC;
```
