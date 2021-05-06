---
layout: page
title: Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server - Создание резервной копии созданной базы данных (холодный бекап)
description: Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server - Создание резервной копии созданной базы данных (холодный бекап)
keywords: Oracle DataBase, Installation, Windows 2008, холодный бекап
permalink: /database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-cold-backup/
---

# <a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/">[Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server]</a>: Создание резервной копии созданной базы данных (холодный бекап)

<br/>

Выполните следующие команды:

    sqlplus / as sysdba

<br/>

    SQL> shutdown immediate;
    SQL> startup mount;
    SQL> quit

<br/>

    $ rman target /

<br/>

    RMAN> backup full database noexclude include current controlfile spfile TAG "FULL_COLD_BACKUP";

<br/>

    ****
    channel ORA_DISK_1: backup set complete, elapsed time: 00:00:01
    Finished backup at 25-AUG-13

<br/>

    RMAN> sql 'alter database open';

<br/>

    RMAN> quit

<br/>

    sqlplus / as sysdba

<br/>

Получить информацию о использовании FRA

<br/>

    SQL> SELECT
        TO_CHAR(SPACE_USED, '999,999,999,999') AS "Used",
        TO_CHAR(SPACE_LIMIT - SPACE_USED + SPACE_RECLAIMABLE, '999,999,999,999')
           AS "Free",
        ROUND((SPACE_USED - SPACE_RECLAIMABLE)/SPACE_LIMIT * 100, 1)
           AS "Used %"
        FROM V$RECOVERY_FILE_DEST;

<br/>

    Used             Free                 Used %
    ---------------- ---------------- ----------
         520,380,416   20,974,837,760        2.3

<br/>

    SQL> quit
