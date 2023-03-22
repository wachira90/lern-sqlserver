# check numa

```sql
select @@SERVERNAME,
SERVERPROPERTY('hostname'),
cpu_count, 
hyperthread_ratio, 
softnuma_configuration, 
softnuma_configuration_desc, 
socket_count, 
numa_node_count 
from 
sys.dm_os_sys_info
```

https://docs.aws.amazon.com/prescriptive-guidance/latest/sql-server-ec2-best-practices/maxdop.html

https://docs.aws.amazon.com/prescriptive-guidance/latest/sql-server-ec2-best-practices/parallelism.html
