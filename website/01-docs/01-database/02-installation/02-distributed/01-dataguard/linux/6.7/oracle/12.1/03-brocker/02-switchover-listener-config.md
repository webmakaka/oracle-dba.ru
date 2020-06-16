---
layout: page
title: Переконфигурирование Listener для Switchover
description: Переконфигурирование Listener для Switchover
keywords: Oracle DataBase 12.1, Centos 6.7, DataGuard
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/broker/switchover-listener-config/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Переконфигурирование Listener для Switchover

<br/>

### Перенастройка Listener на Primary

    $ cd /u01/oracle/database/12.1/network/admin/
    $ cp listener.ora listener.ora.bkp

<br/>

    $ vi listener.ora

<br/>

LISTENER =
(ADDRESS_LIST=
(ADDRESS=(PROTOCOL=tcp)(HOST=moscow.localdomain)(PORT=1521))
(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))

SID_LIST_LISTENER=
(SID_LIST=
(SID_DESC=
(GLOBAL_DBNAME=master_DGMGRL)
(ORACLE_HOME=/u01/oracle/database/12.1)
(SID_NAME=orcl12)
)
(SID_DESC=
(GLOBAL_DBNAME=slave_DGMGRL)
(ORACLE_HOME=/u01/oracle/database/12.1)
(SID_NAME=orcl12)
)
)

<br/>

### Перенастройка Listener на Standby

\*\_DGMGRL - название взято из конфига брокера.

    $ cd /u01/oracle/database/12.1/network/admin/
    $ cp listener.ora listener.ora.bkp

<br/>

    $ vi listener.ora

<br/>

    LISTENER =
    (ADDRESS_LIST=
            (ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521))
            (ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))

    SID_LIST_LISTENER=
                (SID_LIST=
                        (SID_DESC=
                            (GLOBAL_DBNAME=master_DGMGRL)
                            (ORACLE_HOME=/u01/oracle/database/12.1)
                            (SID_NAME=orcl12)
                        )
                        (SID_DESC=
                            (GLOBAL_DBNAME=slave_DGMGRL)
                            (ORACLE_HOME=/u01/oracle/database/12.1)
                            (SID_NAME=orcl12)
                        )
                )

<br/>

    $ lsnrctl stop
    $ lsnrctl start

<br/>

    $ lsnrctl status

    LSNRCTL for Linux: Version 12.1.0.2.0 - Production on 15-AUG-2015 16:30:21

    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=moscow.localdomain)(PORT=1521))
    STATUS of the LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                15-AUG-2015 16:29:31
    Uptime                    0 days 0 hr. 0 min. 49 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Parameter File   /u01/oracle/database/12.1/network/admin/listener.ora
    Listener Log File         /u01/oracle/diag/tnslsnr/moscow/listener/alert/log.xml
    Listening Endpoints Summary...
      (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=moscow.localdomain)(PORT=1521)))
      (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))
    Services Summary...
    Service "+ASM" has 1 instance(s).
      Instance "+ASM", status READY, has 1 handler(s) for this service...
    Service "master" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
    Service "orcl12XDB" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
    The command completed successfully
