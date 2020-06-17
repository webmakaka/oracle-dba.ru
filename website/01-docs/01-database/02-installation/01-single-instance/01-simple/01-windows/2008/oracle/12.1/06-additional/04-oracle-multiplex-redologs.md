---
layout: page
title: Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server - Мультиплексирование redologs
description: Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server - Мультиплексирование redologs
keywords: Oracle DataBase, Installation, Windows 2008, Мультиплексирование redologs
permalink: /database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-multiplex-redologs/
---

# <a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/">[Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server]</a>: Мультиплексирование redologs

<br/>

    md e:\app\oracle\oradata\ora121\redo
    md f:\app\oracle\oradata\ora121\redo

<br/>

    sqlplus / as sysdba

Блок команд, чтобы удобнее представить на экране результаты выполнения запросов.

    SQL> set linesize 250;
    SQL> set pagesize 0;
    SQL> col  GROUP# format 99;
    SQL> col  MEMBER format a40;
    SQL> col  STATUS format a10;
    SQL> col  MB format 999;

<br/>

    SQL> select a.group#, member, a.status, bytes/1024/1024 as "MB"
    from v$log a, v$logfile b
    where a.group# = b.group#
    order by 1;

<br/>

     1 E:\APP\ORACLE\ORADATA\ORA121\REDO01.LOG  INACTIVE     50
     2 E:\APP\ORACLE\ORADATA\ORA121\REDO02.LOG  INACTIVE     50
     3 E:\APP\ORACLE\ORADATA\ORA121\REDO03.LOG  CURRENT      50

<br/>

Удалить можно только файлы неактивной группы. Группы можно переключать, что будет показано ниже.
Удаляем файлы группы в состоянии INACTIVE

1. Нужно пересоздать группу 1 и файлы данной группы.

<br/>

Удаляем файлы группы 1

    SQL> alter database drop logfile group 1;

<br/>

    SQL> quit

<br/>

    del E:\APP\ORACLE\ORADATA\ORA121\REDO01.LOG

<br/>

    $ sqlplus / as sysdba

Добавляем новую группу, перечисляем файлы новой группы и определяем их размер.

    SQL> alter database add logfile group 1 ('e:\app\oracle\oradata\ora121\redo\redo01.log', 'f:\app\oracle\oradata\ora121\redo\redo01.log') size 100M;

2.  Нужно пересоздать группу 2 и файлы данной группы.<br/>
    Удаляем файлы группы 2

        SQL> alter database drop logfile group 2;

<br/>

    SQL> quit

<br/>

    del E:\APP\ORACLE\ORADATA\ORA121\REDO02.LOG

<br/>

    $ sqlplus / as sysdba

<br/>

       SQL> alter database add logfile group 2 ('e:\app\oracle\oradata\ora121\redo\redo02.log', 'f:\app\oracle\oradata\ora121\redo\redo02.log') size 100M;

<br/>

3. Нужно пересоздать группу 3 и файлы данной группы.<br/>
   Так как группа активна, необходимо переключиться на следующую группу файлов, сделав группу 2 INACTIVE.
   <br/>
   Для переключения, достаточно выполнить команды:

<br/>

    SQL> alter system checkpoint;
    SQL> alter system switch logfile;

<br/>

Удаляем файлы группы 3

    SQL> alter database drop logfile group 3;

<br/>

    SQL> quit

<br/>

    del E:\APP\ORACLE\ORADATA\ORA121\REDO03.LOG

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> alter database add logfile group 3 ('e:\app\oracle\oradata\ora121\redo\redo03.log', 'f:\app\oracle\oradata\ora121\redo\redo03.log') size 100M;

<br/>

    SQL> set linesize 250;
    SQL> set pagesize 0;
    SQL> col  GROUP# format 99;
    SQL> col  MEMBER format a40;
    SQL> col  STATUS format a10;
    SQL> col  MB format 999;

<br/>

    SQL> select a.group#, member, a.status, bytes/1024/1024 as "MB"
    from v$log a, v$logfile b
    where a.group# = b.group#
    order by 1,2;

<br/>

     1 E:\APP\ORACLE\ORADATA\ORA121\REDO\REDO01.LOG CURRENT     100
     1 F:\APP\ORACLE\ORADATA\ORA121\REDO\REDO01.LOG CURRENT     100
     2 E:\APP\ORACLE\ORADATA\ORA121\REDO\REDO02.LOG UNUSED      100
     2 F:\APP\ORACLE\ORADATA\ORA121\REDO\REDO02.LOG UNUSED      100
     3 E:\APP\ORACLE\ORADATA\ORA121\REDO\REDO03.LOG UNUSED      100
     3 F:\APP\ORACLE\ORADATA\ORA121\REDO\REDO03.LOG UNUSED      100

<br/>

    SQL> quit
