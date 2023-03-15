# lern-sqlserver
lerning sqlserver


## shrink log

```sql
USE [AdventureWorks]
GO

ALTER DATABASE AdventureWorks SET RECOVERY SIMPLE
GO
DBCC SHRINKFILE (AdventureWorks_log, 1)
GO
ALTER DATABASE AdventureWorks SET RECOVERY FULL
GO
```

## Growth 1MB

```sql
SELECT 'ALTER DATABASE [' + db_name(s.database_id) + '] MODIFY FILE ( NAME = N''' + s.name + ''', FILEGROWTH = 1MB)' as ToExecute
FROM sys.master_files s
	INNER JOIN sys.databases db ON s.database_id = db.database_id
where (
		s.is_percent_growth = 1
		or s.growth * 8.0 / 1024 < 10
)
and db.state_desc = 'online'
ORDER BY s.database_id
```

## standard create

```sql
USE [master]
GO

CREATE DATABASE [ams-uat]
 CONTAINMENT = NONE
 ON  PRIMARY 
( NAME = N'ams-uat', FILENAME = N'/var/opt/mssql/data/ams-uat.mdf' , SIZE = 8192KB , FILEGROWTH = 65536KB )
 LOG ON 
( NAME = N'ams-uat_log', FILENAME = N'/var/opt/mssql/data/ams-uat_log.ldf' , SIZE = 8192KB , FILEGROWTH = 65536KB )
 COLLATE Thai_CI_AS
GO
ALTER DATABASE [ams-uat] SET COMPATIBILITY_LEVEL = 150
GO
ALTER DATABASE [ams-uat] SET ANSI_NULL_DEFAULT OFF 
GO
ALTER DATABASE [ams-uat] SET ANSI_NULLS OFF 
GO
ALTER DATABASE [ams-uat] SET ANSI_PADDING OFF 
GO
ALTER DATABASE [ams-uat] SET ANSI_WARNINGS OFF 
GO
ALTER DATABASE [ams-uat] SET ARITHABORT OFF 
GO
ALTER DATABASE [ams-uat] SET AUTO_CLOSE OFF 
GO
ALTER DATABASE [ams-uat] SET AUTO_SHRINK OFF 
GO
ALTER DATABASE [ams-uat] SET AUTO_CREATE_STATISTICS ON(INCREMENTAL = OFF)
GO
ALTER DATABASE [ams-uat] SET AUTO_UPDATE_STATISTICS ON 
GO
ALTER DATABASE [ams-uat] SET CURSOR_CLOSE_ON_COMMIT OFF 
GO
ALTER DATABASE [ams-uat] SET CURSOR_DEFAULT  GLOBAL 
GO
ALTER DATABASE [ams-uat] SET CONCAT_NULL_YIELDS_NULL OFF 
GO
ALTER DATABASE [ams-uat] SET NUMERIC_ROUNDABORT OFF 
GO
ALTER DATABASE [ams-uat] SET QUOTED_IDENTIFIER OFF 
GO
ALTER DATABASE [ams-uat] SET RECURSIVE_TRIGGERS OFF 
GO
ALTER DATABASE [ams-uat] SET  DISABLE_BROKER 
GO
ALTER DATABASE [ams-uat] SET AUTO_UPDATE_STATISTICS_ASYNC OFF 
GO
ALTER DATABASE [ams-uat] SET DATE_CORRELATION_OPTIMIZATION OFF 
GO
ALTER DATABASE [ams-uat] SET PARAMETERIZATION SIMPLE 
GO
ALTER DATABASE [ams-uat] SET READ_COMMITTED_SNAPSHOT OFF 
GO
ALTER DATABASE [ams-uat] SET  READ_WRITE 
GO
ALTER DATABASE [ams-uat] SET RECOVERY FULL 
GO
ALTER DATABASE [ams-uat] SET  MULTI_USER 
GO
ALTER DATABASE [ams-uat] SET PAGE_VERIFY CHECKSUM  
GO
ALTER DATABASE [ams-uat] SET TARGET_RECOVERY_TIME = 60 SECONDS 
GO
ALTER DATABASE [ams-uat] SET DELAYED_DURABILITY = DISABLED 
GO
USE [ams-uat]
GO
ALTER DATABASE SCOPED CONFIGURATION SET LEGACY_CARDINALITY_ESTIMATION = Off;
GO
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION = Primary;
GO
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 0;
GO
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY;
GO
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING = On;
GO
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING = Primary;
GO
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES = Off;
GO
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET QUERY_OPTIMIZER_HOTFIXES = Primary;
GO
USE [ams-uat]
GO
IF NOT EXISTS (SELECT name FROM sys.filegroups WHERE is_default=1 AND name = N'PRIMARY') ALTER DATABASE [ams-uat] MODIFY FILEGROUP [PRIMARY] DEFAULT
GO
```
