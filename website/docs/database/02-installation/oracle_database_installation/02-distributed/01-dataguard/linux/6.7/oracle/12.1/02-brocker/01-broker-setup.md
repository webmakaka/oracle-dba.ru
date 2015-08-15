---
layout: page
title: Описание системы, которое будет настраиваться
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/broker/setup/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Устанавливаем Broker



<br/>

### Primary и Standby


Для начала мне пришось выполнить команду на primary и standby:

    SQL> ALTER SYSTEM SET LOG_ARCHIVE_DEST_2=" ";

Далее создаю файлы конфигов для брокера

    SQL> ALTER SYSTEM set dg_broker_config_file1='+DATA/db_brocker1.dat' SCOPE=both;
    SQL> ALTER SYSTEM set dg_broker_config_file2='+ARCH/db_brocker2.dat' SCOPE=both;



Запускаю bkoker

    SQL> ALTER SYSTEM SET dg_broker_start=TRUE SCOPE=both;


<br/>

### Primary



    $ dgmgrl

<br/>

    DGMGRL> connect /
    Connected as SYSDG.

или

    DGMGRL> connect sys/manager
    Connected as SYSDG.

<br/>

    DGMGRL> show configuration
    ORA-16532: Oracle Data Guard broker configuration does not exist

    Configuration details cannot be determined by DGMGRL

<br/>

    DGMGRL> create configuration 'DG_ORCL12' as primary database is 'master' connect identifier is master;
    Configuration "DG_ORCL12" created with primary database "master"

<br/>

// standby - в данном случае service прописанный в tnsnames

    DGMGRL> add database 'slave' as connect identifier is standby maintained as physical;
    Database "slave" added


<br/>

    DGMGRL> show configuration

    Configuration - DG_ORCL12

      Protection Mode: MaxPerformance
      Members:
      master - Primary database
        slave  - Physical standby database

    Fast-Start Failover: DISABLED

    Configuration Status:
    DISABLED

<br/>

    DGMGRL> enable configuration;

<br/>

    DGMGRL> show configuration

    Configuration - DG_ORCL12

      Protection Mode: MaxPerformance
      Members:
      master - Primary database
        slave  - Physical standby database
          Error: ORA-16664: unable to receive the result from a database

    Fast-Start Failover: DISABLED

    Configuration Status:
    ERROR   (status updated 72 seconds ago)




<br/>

    DGMGRL> show database master

    Database - master

      Role:               PRIMARY
      Intended State:     TRANSPORT-ON
      Instance(s):
        orcl12

    Database Status:
    SUCCESS

<br/>

    DGMGRL> show database slave

    Database - slave

      Role:               PHYSICAL STANDBY
      Intended State:     APPLY-ON
      Transport Lag:      (unknown)
      Apply Lag:          (unknown)
      Average Apply Rate: (unknown)
      Real Time Query:    OFF
      Instance(s):
        orcl12

    Database Status:
    DGM-17016: failed to retrieve status for database "slave"
    ORA-16664: unable to receive the result from a database



<br/>

Логи:

    $ less /u01/oracle/diag/rdbms/master/orcl12/trace/drcorcl12.log


<br/>

### На Standby

    DGMGRL> show database master

    Database - master

      Role:               PRIMARY
      Intended State:     TRANSPORT-ON
      Instance(s):
        orcl12

    Database Status:
    DGM-17016: failed to retrieve status for database "master"
    ORA-16501: The Oracle Data Guard broker operation failed.
    ORA-16625: cannot reach database "master"


<br/>

    Database - slave

      Role:               PHYSICAL STANDBY
      Intended State:     APPLY-ON
      Transport Lag:      0 seconds (computed 1 second ago)
      Apply Lag:          (unknown)
      Average Apply Rate: (unknown)
      Real Time Query:    OFF
      Instance(s):
        orcl12
          Warning: ORA-16714: the value of property ArchiveLagTarget is inconsistent with the database setting
          Warning: ORA-16714: the value of property LogArchiveMaxProcesses is inconsistent with the database setting
          Warning: ORA-16714: the value of property LogArchiveMinSucceedDest is inconsistent with the database setting
          Warning: ORA-16714: the value of property LogArchiveTrace is inconsistent with the database setting
          Warning: ORA-16675: database instance restart required for property value modification to take effect
          Warning: ORA-16714: the value of property LogArchiveFormat is inconsistent with the database setting

      Database Error(s):
        ORA-16766: Redo Apply is stopped

    Database Status:
    ERROR




<br/>

### Посмотреть параметры:

    SQL> show parameter dg_broker_config_file1
    SQL> show parameter dg_broker_start


<br/>

### Команды для информации:

    -- остановить bkoker (пока не делаю)

    SQL> ALTER SYSTEM SET dg_broker_start=FALSE SCOPE=both;


<br/>

### Ошибки:


    DGMGRL> create configuration 'DG_ORCL12' as primary database is 'master' connect identifier is master;
    Error: ORA-16698: LOG_ARCHIVE_DEST_n parameter set for object to be added


You must clear any remote redo transport destinations on the primary database that do not have the NOREGISTER attribute, before a configuration can be created. Otherwise, the following error message is returned when you attempt to create the configuration:

    ORA-16698: LOG_ARCHIVE_DEST_n parameter set for object to be added

    Failed.

<br/>

    SQL> ALTER SYSTEM SET LOG_ARCHIVE_DEST_2=" ";
