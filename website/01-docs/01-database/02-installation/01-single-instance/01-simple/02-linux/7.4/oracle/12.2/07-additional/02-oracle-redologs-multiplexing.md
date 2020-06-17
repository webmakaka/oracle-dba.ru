---
layout: page
title: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4 - Мультиплексирование redologs
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Мультиплексирование redologs
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, Мультиплексирование redologs
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-redologs-multiplexing/
---

<br/>

<div style="padding:10px; border:thin solid black;">

    <h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Мультиплексирование redologs

<br/>

    $ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/REDOLOGS
    $ mkdir -p /u03/oracle/oradata/12.2/${ORACLE_SID}/REDOLOGS

<br/>

    $ sqlplus / as sysdba

Блок команд, чтобы удобнее представить на экране результаты выполнения запросов.

    SQL> set linesize 250;
    SQL> set pagesize 0;
    SQL> col  GROUP# format 99;
    SQL> col  MEMBER format a50;
    SQL> col  STATUS format a10;
    SQL> col  MB format 999;

<br/>

    SQL> select a.group#, member, a.status, bytes/1024/1024 as "MB"
    from v$log a, v$logfile b
    where a.group# = b.group#
    order by 1;

<br/>

    1 /u02/oracle/oradata/12.2/orcl12/redo01.log	  INACTIVE     50
    2 /u02/oracle/oradata/12.2/orcl12/redo02.log	  INACTIVE     50
    3 /u02/oracle/oradata/12.2/orcl12/redo03.log	  CURRENT      50

Удалить можно только файлы неактивной группы. Группы можно переключать, что будет показано ниже.  
Удаляем файлы группы в состоянии INACTIVE

1. Нужно пересоздать группу 1 и файлы данной группы.

Удаляем файлы группы 1

    SQL> alter database drop logfile group 1;

    SQL> quit

<br/>

    $ rm /u02/oracle/oradata/12.2/orcl/redo01.log

<br/>

    $ sqlplus / as sysdba

Добавляем новую группу, перечисляем файлы новой группы и определяем их размер.

    SQL> alter database add logfile group 1 ('/u02/oracle/oradata/12.2/orcl12/REDOLOGS/redo01.log' , '/u03/oracle/oradata/12.2/orcl12/REDOLOGS/redo01.log') size 100M;

<br/>

2. Нужно пересоздать группу 2 и файлы данной группы.<br/>
   Удаляем файлы группы 2


    SQL> alter database drop logfile group 2;

    SQL> quit

<br/>

    $ rm /u02/oracle/oradata/12.2/orcl/redo02.log

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> alter database add logfile group 2 ('/u02/oracle/oradata/12.2/orcl12/REDOLOGS/redo02.log' , '/u03/oracle/oradata/12.2/orcl12/REDOLOGS/redo02.log') size 100M;

3. Нужно пересоздать группу 3 и файлы данной группы.<br/>
   Так как группа активна, необходимо переключиться на следующую группу файлов, сделав группу 2 INACTIVE.

Для переключения, достаточно выполнить команды:

    SQL> alter system checkpoint;
    SQL> alter system switch logfile;

Удаляем файлы группы 3

    SQL> alter database drop logfile group 3;

    SQL> quit

<br/>

    $ rm /u02/oracle/oradata/12.2/orcl/redo03.log

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> alter database add logfile group 3 ('/u02/oracle/oradata/12.2/orcl12/REDOLOGS/redo03.log' , '/u03/oracle/oradata/12.2/orcl12/REDOLOGS/redo03.log') size 100M;

<br/>

    SQL> set linesize 250;
    SQL> set pagesize 0;
    SQL> col  GROUP# format 99;
    SQL> col  MEMBER format a55;
    SQL> col  STATUS format a10;
    SQL> col  MB format 999;

<br/>

    SQL> select a.group#, member, a.status, bytes/1024/1024 as "MB"
    from v$log a, v$logfile b
    where a.group# = b.group#
    order by 1,2;

<br/>

    1 /u02/oracle/oradata/12.2/orcl12/REDOLOGS/redo01.log     CURRENT	   100
    1 /u03/oracle/oradata/12.2/orcl12/REDOLOGS/redo01.log     CURRENT	   100
    2 /u02/oracle/oradata/12.2/orcl12/REDOLOGS/redo02.log     UNUSED	   100
    2 /u03/oracle/oradata/12.2/orcl12/REDOLOGS/redo02.log     UNUSED	   100
    3 /u02/oracle/oradata/12.2/orcl12/REDOLOGS/redo03.log     UNUSED	   100
    3 /u03/oracle/oradata/12.2/orcl12/REDOLOGS/redo03.log     UNUSED	   100

    6 rows selected.

<br/>

    SQL> quit
