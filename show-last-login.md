# show last login

-- 1. ====================creation history tables=================

````
IF (OBJECT_ID('dbo.LoginHistory') IS NULL) BEGIN
CREATE TABLE dbo.LoginHistory (
    Username VARCHAR(128) COLLATE SQL_Latin1_General_CP1_CI_AI NOT NULL,
    LoginTime DATETIME NOT NULL,
    ProgramName VARCHAR(255)
)
END IF (OBJECT_ID('dbo.LastLogin') IS NULL) BEGIN -- DROP TABLE dbo.LastLogin
CREATE TABLE dbo.LastLogin (
    Username VARCHAR(128) COLLATE SQL_Latin1_General_CP1_CI_AI NOT NULL,
    CreateDate DATETIME,
    LastLogin DATETIME NULL,
    DaysSinceLastLogin AS (
        DATEDIFF(
            DAY,
            ISNULL(LastLogin, CreateDate),
            CONVERT(DATE, GETDATE())
        )
    )
)
END 
````
-- 2. =================Creation Trigger=======================

````
CREATE TRIGGER [trgAudit_LoginHistory] ON ALL SERVER -- Para evitar problemas de permissão no insert na tabela
    WITH EXECUTE AS 'sa' FOR LOGON AS BEGIN
SET NOCOUNT ON -- Não loga conexões de usuários de sistema
    IF (
        ORIGINAL_LOGIN() LIKE 'NT %'
        OR ORIGINAL_LOGIN() LIKE '##%'
        OR ORIGINAL_LOGIN() LIKE '%SQLServerAgent'
    ) RETURN -- Não loga conexões de softwares que ficam se conectando constantemente
    IF (
        PROGRAM_NAME() LIKE 'Red Gate%'
        OR PROGRAM_NAME() LIKE '%IntelliSense%'
        OR PROGRAM_NAME() LIKE 'SQLAgent %'
        OR PROGRAM_NAME() IN (
            'Microsoft SQL Server',
            'RSPowerBI',
            'RSManagement',
            'TransactionManager',
            'DWDiagnostics',
            'Report Server'
        )
    ) RETURN
INSERT INTO dbo.LoginHistory (Username, LoginTime, ProgramName)
SELECT ORIGINAL_LOGIN(),
    GETDATE(),
    PROGRAM_NAME()
END
````

-- 3. ===========enable trigger===================

````
ENABLE TRIGGER [trgAudit_LoginHistory] ON ALL SERVER
````

-- 4. ===========Generates show last login===================
````
IF (OBJECT_ID('tempdb..#UltimoLogin') IS NOT NULL) DROP TABLE #UltimoLogin
CREATE TABLE #UltimoLogin (
[User] VARCHAR(128) COLLATE SQL_Latin1_General_CP1_CI_AI NOT NULL,
LogDate DATETIME NOT NULL )

INSERT INTO #UltimoLogin
SELECT Username,
    MAX(LoginTime) AS LogDate
FROM dbo.LoginHistory
GROUP BY Username -- Insere os logins criados na instância
INSERT INTO dbo.LastLogin (Username, CreateDate)
SELECT [name],
    create_date
FROM sys.server_principals A
    LEFT JOIN dbo.LastLogin B ON A.[name] COLLATE SQL_Latin1_General_CP1_CI_AI = B.Username
WHERE is_fixed_role = 0
    AND [name] NOT LIKE 'NT %'
    AND [name] NOT LIKE '##%'
    AND B.Username IS NULL
    AND A.[type] IN ('S', 'U') -- Atualiza a tabela de histórico com os dados atuais
UPDATE A
SET A.LastLogin = B.LogDate
FROM dbo.LastLogin A
    JOIN #UltimoLogin B ON A.Username = B.[User]
WHERE ISNULL(A.LastLogin, '1900-01-01') <> B.LogDate
SELECT *
FROM dbo.LastLogin
````
