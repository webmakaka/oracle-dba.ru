---
layout: page
title: switchover (переключение ролей между primary и standby instance)
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/broker/switchover/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Устанавливаем Broker



<br/>

### Primary и Standby



$ lsnrctl status

LSNRCTL for Linux: Version 12.1.0.2.0 - Production on 15-AUG-2015 12:52:32

Copyright (c) 1991, 2014, Oracle.  All rights reserved.

Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
Start Date                14-AUG-2015 07:48:36
Uptime                    1 days 5 hr. 3 min. 56 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Parameter File   /u01/oracle/database/12.1/network/admin/listener.ora
Listener Log File         /u01/oracle/diag/tnslsnr/piter/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))
Services Summary...
Service "+ASM" has 1 instance(s).
  Instance "+ASM", status READY, has 1 handler(s) for this service...
Service "slave" has 1 instance(s).
  Instance "orcl12", status UNKNOWN, has 1 handler(s) for this service...
The command completed successfully









swithchover to "NODUDAS"


show configuration



на primary (бывшем) master
alter databaser recover manager current logfile disconnect


select open_mode, database_role from v$database;


на slave

create tablespace test datafile '+DATA' size 10M autoextend off;


select name from v$tablespace;


SELECT 'Last Applied : ' Logs, to_char(next_time, 'DD-MON-YYYY:HH24:MI:SS') Time
FROM v$archived_log
WHERE sequence# = (select max(sequence#) FROM v$archived_log where applied='YES')
UNION
SELECT 'Last Received : ' Logs, to_char(next_time, 'DD-MON-YYYY:HH24:MI:SS') Time
FROM v$archived_log
WHERE sequence# = (select max(sequence#) FROM v$archived_log)
