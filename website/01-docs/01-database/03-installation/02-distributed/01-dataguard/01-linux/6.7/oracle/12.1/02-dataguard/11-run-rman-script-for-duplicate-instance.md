---
layout: page
title: Создание rman скрипта для создания дупликата primary и его выполнение
description: Создание rman скрипта для создания дупликата primary и его выполнение
keywords: Oracle DataBase 12.1, Centos 6.7, DataGuard
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/run-rman-script-for-duplicate-instance/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание rman скрипта для создания дупликата primary и его выполнение

### На Primary

<br/>

    $ cd /tmp/

<br/>

    $ vi rmanscript.rman

<br/>

    run {
    	allocate channel prmy1 type disk;
    	allocate auxiliary channel stby type disk;
    	DUPLICATE TARGET DATABASE
    	  FOR STANDBY
    	  FROM ACTIVE DATABASE
    	  DORECOVER
    	  SPFILE

    		### SET ANY PARAMS FOR STANDBY

    		SET "db_unique_name"="slave"

    		### END of SET ANY PARAMS FOR STANDBY

    	  NOFILENAMECHECK;
    }

Я решил, что лучше я сделаю дубликат, а параметры задам уже позднее в консоли. Поэтому в скрипте, только один параметр set.

Параметр nofilenamecheck нам нужен, чтобы rman не ругался на повторяющиеся имена файлов (если мы используем одинаковую структуру каталогов на основном и standby серверах).

The following example illustrates how to use DUPLICATE for active duplication. This example requires the NOFILENAMECHECK option because the primary database files have the same names as the standby database files. The SET clauses for SPFILE are required for log shipping to work properly. The db_unique_name must be set to ensure that the catalog and Data Guard can identify this database as being different from the primary.

RMAN automatically copies the server parameter file to the standby host, starts the auxiliary instance with the server parameter file, restores a backup control file, and copies all necessary database files and archived redo logs over the network to the standby host. RMAN recovers the standby database, but does not place it in manual or managed recovery mode.

DORECOVER option to recover the database after standby creation

http://docs.oracle.com/cd/B28359_01/server.111/b28294/rcmbackp.htm

Если мы хотим разместить нашу standby базу в каталогах, отличных от тех, в которых размещена основная база, нам понадобятся дополнительные параметры:

db_file_name_convert='/oradata_new/test','/oradata/test' – этот параметр указывает, что в именах файлов данных, которые будут создаваться в standby базе (т.е. когда наш основной экземпляр начнет работать в режиме standby), необходимо изменить пути с '/oradata_new/test' на '/oradata/test'.

log_file_name_convert='/oradata_new/test/archive','/oradata/test/archive' – этот параметр указывает, что в именах журнальных файлов, которые будут создаваться в standby базе, необходимо изменить пути с '/oradata_new/test/archive' на '/oradata/test/archive'.

<br/>

Проверим синтаксис скрипта.

    $ rman CHECKSYNTAX @rmanscript.rman

    ***
    The cmdfile has no syntax errors

Поехали:

    $ rman target sys/manager@primary auxiliary sys/manager@standby @rmanscript.rman

<br/>

    ***
    Finished Duplicate Db at 12-AUG-15
    released channel: prmy1
    released channel: stby

    Recovery Manager complete.

<!--

SQL>  select to_char(CURRENT_SCN) CURRENT_SCN FROM V$DATABASE;

-->

<br/>

### Ошибка!

Иногда возникала ошибка на primary.

    Oracle instance shut down

    connected to auxiliary database (not started)
    released channel: prmy1
    RMAN-00571: ===========================================================
    RMAN-00569: =============== ERROR MESSAGE STACK FOLLOWS ===============
    RMAN-00571: ===========================================================
    RMAN-03002: failure of Duplicate Db command at 08/14/2015 06:42:26
    RMAN-05501: aborting duplication of target database
    RMAN-03015: error occurred in stored script Memory Script
    RMAN-04014: startup failed: ORA-00119: invalid specification for system parameter LOCAL_LISTENER
    ORA-00132: syntax error or unresolved network name 'LISTENER_ORCL12'

Вылечилась следующим образом:

    SQL> alter system set local_listener='(DESCRIPTION =(ADDRESS = (PROTOCOL = TCP)(HOST = moscow.localdomain)(PORT = 1521)))' scope=both;
