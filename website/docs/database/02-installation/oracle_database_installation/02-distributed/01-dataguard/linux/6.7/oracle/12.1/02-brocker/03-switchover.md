---
layout: page
title: Приступаем к switchover на Primary
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/broker/switchover/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Приступаем к switchover на Primary


<br/>

### Приступаем к switchover на Primary



$ dgmgrl

<br/>

DGMGRL> connect /

<br/>


    DGMGRL> SHOW DATABASE VERBOSE MASTER

    Database - master

      Role:               PRIMARY
      Intended State:     TRANSPORT-ON
      Instance(s):
        orcl12

      Properties:
        DGConnectIdentifier             = 'primary'
        ObserverConnectIdentifier       = ''
        LogXptMode                      = 'ASYNC'
        RedoRoutes                      = ''
        DelayMins                       = '0'
        Binding                         = 'optional'
        MaxFailure                      = '0'
        MaxConnections                  = '1'
        ReopenSecs                      = '300'
        NetTimeout                      = '30'
        RedoCompression                 = 'DISABLE'
        LogShipping                     = 'ON'
        PreferredApplyInstance          = ''
        ApplyInstanceTimeout            = '0'
        ApplyLagThreshold               = '0'
        TransportLagThreshold           = '0'
        TransportDisconnectedThreshold  = '30'
        ApplyParallel                   = 'AUTO'
        StandbyFileManagement           = 'AUTO'
        ArchiveLagTarget                = '0'
        LogArchiveMaxProcesses          = '4'
        LogArchiveMinSucceedDest        = '1'
        DbFileNameConvert               = ''
        LogFileNameConvert              = ''
        FastStartFailoverTarget         = ''
        InconsistentProperties          = '(monitor)'
        InconsistentLogXptProps         = '(monitor)'
        SendQEntries                    = '(monitor)'
        LogXptStatus                    = '(monitor)'
        RecvQEntries                    = '(monitor)'
        StaticConnectIdentifier         = '(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=moscow.localdomain)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=master_DGMGRL)(INSTANCE_NAME=orcl12)(SERVER=DEDICATED)))'
        StandbyArchiveLocation          = 'USE_DB_RECOVERY_FILE_DEST'
        AlternateLocation               = ''
        LogArchiveTrace                 = '0'
        LogArchiveFormat                = '%t_%s_%r.dbf'
        TopWaitEvents                   = '(monitor)'

    Database Status:
    SUCCESS


**1. Ensure standby redologs are configured on all databases.**

    on primary:
    SQL> SELECT TYPE,MEMBER FROM V$LOGFILE;


**2. Ensure the LogXptMode Property is set to SYNC.**


    DGMGRL> EDIT DATABASE master SET PROPERTY 'LogXptMode'='SYNC';
    DGMGRL> EDIT DATABASE slave SET PROPERTY 'LogXptMode'='SYNC';



**3.Specify the FastStartFailoverTarget property**


    DGMGRL> EDIT DATABASE master SET PROPERTY FastStartFailoverTarget='slave';
    DGMGRL> EDIT DATABASE slave SET PROPERTY FastStartFailoverTarget='master';


**4.Upgrade the protection mode to MAXAVAILABILITY, if necessary.**

    DGMGRL> EDIT CONFIGURATION SET PROTECTION MODE AS MAXAVAILABILITY;


**5. Enable Flashback Database on the Primary and Standby Databases.**

==============

    DGMGRL> ENABLE FAST_START FAILOVER;













show configuration verbose





http://oracleinstance.blogspot.ru/2010/01/configuration-of-10g-data-guard-broker.html



    Use the SHOW DATABASE VERBOSE command to check the state, health, and properties of the primary database, as follows:

    state
    health


    LogXptMode - 'SYNC'





You can switch the role of the primary database and a standby database using the SWITCHOVER command. Before you issue the SWITCHOVER command, you must ensure:

* The state of the primary and standby databases are TRANSPORT-ON and APPLY-ON, respectively.

* All participating databases are in good health, without any errors or warnings present.

* The standby database properties were set on the primary database, so that the primary database can function correctly when transitioning to a standby database (shown in the following examples in boldface type).

* Standby redo log files on the primary database are set up, and the LogXptMode configurable database property is set to SYNC if the configuration is operating in either maximum availability mode or maximum protection mode.

* If fast-start failover is enabled, you can perform a switchover only to the standby database that was specified as the target standby database.

















    DGMGRL> show configuration

    Configuration - DG_ORCL12

      Protection Mode: MaxPerformance
      Members:
      master - Primary database
        slave  - Physical standby database

    Fast-Start Failover: DISABLED

    Configuration Status:
    SUCCESS   (status updated 12 seconds ago)


<br/>

    DGMGRL> switchover to slave;

<br/>

    DGMGRL> show configuration

    Configuration - DG_ORCL12

      Protection Mode: MaxPerformance
      Members:
      master - Primary database
        slave  - Physical standby database

    Fast-Start Failover: DISABLED

    Configuration Status:
    SUCCESS   (status updated 30 seconds ago)





=======================================

на primary (бывшем) master
alter databaser recover manager current logfile disconnect


select open_mode, database_role from v$database;


на slave

create tablespace test datafile '+DATA' size 10M autoextend off;


select name from v$tablespace;


    SQL> SELECT 'Last Applied : ' Logs, to_char(next_time, 'DD-MON-YYYY:HH24:MI:SS') Time
    FROM v$archived_log
    WHERE sequence# = (select max(sequence#) FROM v$archived_log where applied='YES')
    UNION
    SELECT 'Last Received : ' Logs, to_char(next_time, 'DD-MON-YYYY:HH24:MI:SS') Time
    FROM v$archived_log
    WHERE sequence# = (select max(sequence#) FROM v$archived_log)
