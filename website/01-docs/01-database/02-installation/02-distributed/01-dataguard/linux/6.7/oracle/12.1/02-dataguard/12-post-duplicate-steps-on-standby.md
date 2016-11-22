---
layout: page
title:  Настройка параметров Instance после создания дупликата на standby
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-on-standby/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Настройка параметров Instance после создания дупликата на standby




### STANDBY


    SQL> alter system set LOG_ARCHIVE_CONFIG="DG_CONFIG=(master, slave)" scope=both;


Сам я хрен знает сколько времени сидел из-за того, что неправильно указывал SERVICE. В общем значение SERVICE из tnanames.ora. Я же ставил в поле SERVICE - db_unique_name.

    SQL> alter system set log_archive_dest_2="SERVICE=primary LGWR SYNC VALID_FOR=(ONLINE_LOGFILES,PRIMARY_ROLE) db_unique_name=master" scope=both;

<br/>

    SQL> alter system set log_archive_dest_state_2="enable" scope=both;

<br/>

    SQL> alter system set standby_file_management= AUTO scope=both;

<br/>

    SQL> alter system set FAL_SERVER="master" scope=both;
    SQL> alter system set FAL_CLIENT="slave" scope=both;



### Донастройка Listener на standby

Не нравится, что listener.ora в разных каталогах.

    $ cp /u01/oracle/grid/12.1/network/admin/listener.ora /u01/oracle/grid/12.1/network/admin/listener.ora.bkp

    $ mv /u01/oracle/database/12.1/network/admin/listener.ora /u01/oracle/grid/12.1/network/admin/listener.ora


    SQL> alter system set local_listener='(DESCRIPTION =(ADDRESS = (PROTOCOL = TCP)(HOST = piter.localdomain)(PORT = 1521)))' scope=both;


    $ lsnrctl status

    LSNRCTL for Linux: Version 12.1.0.2.0 - Production on 15-AUG-2015 13:37:58

    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                15-AUG-2015 13:30:22
    Uptime                    0 days 0 hr. 7 min. 35 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Parameter File   /u01/oracle/grid/12.1/network/admin/listener.ora
    Listener Log File         /u01/oracle/diag/tnslsnr/piter/listener/alert/log.xml
    Listening Endpoints Summary...
      (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521)))
      (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))
    Services Summary...
    Service "+ASM" has 1 instance(s).
      Instance "+ASM", status READY, has 1 handler(s) for this service...
    Service "orcl12XDB" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
    Service "slave" has 2 instance(s).
      Instance "orcl12", status UNKNOWN, has 1 handler(s) for this service...
      Instance "orcl12", status READY, has 1 handler(s) for this service...
    Service "slave_DGB" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
    The command completed successfully
