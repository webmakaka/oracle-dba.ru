---
layout: page
title: Инсталляция Oracle DataBase 12c в Oracle Linux 6.7 -  Создание резервной копии созданной базы данных (холодный бекап)
description: Инсталляция Oracle DataBase 12c в операционной системе Oracle Linux 6.7 -  Создание резервной копии созданной базы данных (холодный бекап)
keywords: Oracle DataBase 12c, Oracle Linux 6.7, Холодный бекап, Cold Backup
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/oracle-cold-backup/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Создание резервной копии созданной базы данных (холодный бекап)

Выполните следующие команды:

    $ rman target /

<br/>

    RMAN> shutdown immediate;
    RMAN> startup mount;

<br/>

    RMAN> BACKUP DATABASE TAG "FULL_DATABASE_DATAFILES";
    RMAN> BACKUP CURRENT CONTROLFILE TAG "FULL_DATABASE_CONTROLFILE";
    RMAN> BACKUP SPFILE TAG "FULL_DATABASE_SPFILE";

<br/>

    RMAN> alter database open;

<br/>

    RMAN> quit

<br/>

    $ sqlplus / as sysdba

Получить информацию о использовании FRA

    SQL> SELECT
        TO_CHAR(SPACE_USED, '999,999,999,999') AS "Used",
        TO_CHAR(SPACE_LIMIT - SPACE_USED + SPACE_RECLAIMABLE, '999,999,999,999')
           AS "Free",
        ROUND((SPACE_USED - SPACE_RECLAIMABLE)/SPACE_LIMIT * 100, 1)
           AS "Used %"
        FROM V$RECOVERY_FILE_DEST;

<br/>

    Used		 Free		      Used %
    ---------------- ---------------- ----------
         754,827,264   20,730,118,144	 3.5

<br/>

    SQL> quit
