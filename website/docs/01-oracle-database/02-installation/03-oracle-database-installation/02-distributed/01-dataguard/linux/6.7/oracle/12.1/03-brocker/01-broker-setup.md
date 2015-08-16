---
layout: page
title: Установка брокера (DGMGRL)
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/dataguard/linux/6.7/oracle/12.1/broker/setup/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Устанавливаем Broker



<br/>

### Primary и Standby


Для начала мне пришось выполнить команду на primary и standby:

    SQL> ALTER SYSTEM SET LOG_ARCHIVE_DEST_2=" ";

Далее создаю файлы конфигов для брокера

    SQL> ALTER SYSTEM set dg_broker_config_file1='+DATA/db_brocker1.dat' SCOPE=both;
    SQL> ALTER SYSTEM set dg_broker_config_file2='+ARCH/db_brocker2.dat' SCOPE=both;



Запускаю broker

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

или

    DGMGRL> CONNECT sys@primary
    Password:
    Connected as SYSDBA.


<br/>

    DGMGRL> show configuration
    ORA-16532: Oracle Data Guard broker configuration does not exist

    Configuration details cannot be determined by DGMGRL

<br/>

// primary - в данном случае service прописанный в tnsnames

    DGMGRL> CREATE CONFIGURATION 'DG_ORCL12' AS PRIMARY DATABASE IS 'master' CONNECT IDENTIFIER IS primary;

    Configuration "DG_ORCL12" created with primary database "master"

<br/>


// standby - в данном случае service прописанный в tnsnames

    DGMGRL> ADD DATABASE 'slave' AS CONNECT IDENTIFIER IS standby maintained as physical;
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

    DGMGRL> ENABLE CONFIGURATION;

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
      Transport Lag:      0 seconds (computed 1 second ago)
      Apply Lag:          0 seconds (computed 1 second ago)
      Average Apply Rate: 565.00 KByte/s
      Real Time Query:    ON
      Instance(s):
        orcl12

    Database Status:
    SUCCESS


<br/>

Логи:

    $ less /u01/oracle/diag/rdbms/master/orcl12/trace/drcorcl12.log


<br/>


<br/>

### Посмотреть параметры:

    SQL> show parameter dg_broker_config_file1
    SQL> show parameter dg_broker_start


<br/>

### Команды для информации:


    SQL> show parameter broker

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    connection_brokers		     string	 ((TYPE=DEDICATED)(BROKERS=1)),
    						  ((TYPE=EMON)(BROKERS=1))
    dg_broker_config_file1		     string	 +DATA/db_brocker1.dat
    dg_broker_config_file2		     string	 +ARCH/db_brocker2.dat
    dg_broker_start 		     boolean	 TRUE
    use_dedicated_broker		     boolean	 FALSE



Остановить bkoker

    SQL> ALTER SYSTEM SET dg_broker_start=FALSE SCOPE=both;


Выключить конфигурацию:

    DGMGRL> disable configuration;

Удалить конфигурацию:

    DGMGRL> REMOVE CONFIGURATION;


Получить подробную информации по базе:

    DGMGRL> show database verbose master

Получить подробную информации по экземпляру:

    DGMGRL> show instance verbose orcl12 on database master

<br/>

### Ошибки:


**Ошибка 1:**

    DGMGRL> create configuration 'DG_ORCL12' as primary database is 'master' connect identifier is master;
    Error: ORA-16698: LOG_ARCHIVE_DEST_n parameter set for object to be added


You must clear any remote redo transport destinations on the primary database that do not have the NOREGISTER attribute, before a configuration can be created. Otherwise, the following error message is returned when you attempt to create the configuration:

    ORA-16698: LOG_ARCHIVE_DEST_n parameter set for object to be added

    Failed.

<br/>

    SQL> ALTER SYSTEM SET LOG_ARCHIVE_DEST_2=" ";


<br/>

 **Ошибка 2**  

     DGMGRL> show database slave

     Database - slave

       Role:               PHYSICAL STANDBY
       Intended State:     APPLY-ON
       Transport Lag:      0 seconds (computed 0 seconds ago)
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

 На standby

    SQL> alter database recover managed standby database using current logfile disconnect;





http://docs.oracle.com/cd/B28359_01/server.111/b28295/dgmgrl.htm#i78344
