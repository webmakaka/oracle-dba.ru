---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle_database_installation/linux/6.4/oracle/12.1/oracle-multiplex-redologs/
---

# <a href="/oracle_database_installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Мультиплексирование redologs


	$ mkdir -p /u02/oracle/oradata/${ORACLE_SID}/redo
	$ mkdir -p /u03/oracle/oradata/${ORACLE_SID}/redo


<br/>

	$ sqlplus / as sysdba


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

     1 /u02/oracle/oradata/orcl/redo01.log	INACTIVE     50
     2 /u02/oracle/oradata/orcl/redo02.log	INACTIVE     50
     3 /u02/oracle/oradata/orcl/redo03.log	CURRENT      50


Удалить можно только файлы неактивной группы. Группы можно переключать, что будет показано ниже.  
Удаляем файлы группы в состоянии INACTIVE


1) Нужно пересоздать группу 1 и файлы данной группы.


Удаляем файлы группы 1

	SQL> alter database drop logfile group 1;

	SQL> quit

<br/>

	$ rm /u02/oracle/oradata/orcl/redo01.log



<br/>

	$ sqlplus / as sysdba


Добавляем новую группу, перечисляем файлы новой группы и определяем их размер.

	SQL> alter database add logfile group 1 ('/u02/oracle/oradata/orcl/redo/redo01.log' , '/u03/oracle/oradata/orcl/redo/redo01.log') size 100M;

<br/>

2) Нужно пересоздать группу 2 и файлы данной группы.<br/>
Удаляем файлы группы 2


	SQL> alter database drop logfile group 2;

	SQL> quit

<br/>

	$ rm /u02/oracle/oradata/orcl/redo02.log



<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> alter database add logfile group 2 ('/u02/oracle/oradata/orcl/redo/redo02.log' , '/u03/oracle/oradata/orcl/redo/redo02.log') size 100M;


3) Нужно пересоздать группу 3 и файлы данной группы.<br/>
Так как группа активна, необходимо переключиться на следующую группу файлов, сделав группу 2 INACTIVE.


Для переключения, достаточно выполнить команды:


	SQL> alter system checkpoint;
	SQL> alter system switch logfile;


Удаляем файлы группы 3

	SQL> alter database drop logfile group 3;

	SQL> quit

<br/>

	$ rm /u02/oracle/oradata/orcl/redo03.log


<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> alter database add logfile group 3 ('/u02/oracle/oradata/orcl/redo/redo03.log' , '/u03/oracle/oradata/orcl/redo/redo03.log') size 100M;

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

     1 /u02/oracle/oradata/orcl/redo/redo01.log INACTIVE    100
     1 /u03/oracle/oradata/orcl/redo/redo01.log INACTIVE    100
     2 /u02/oracle/oradata/orcl/redo/redo02.log CURRENT     100
     2 /u03/oracle/oradata/orcl/redo/redo02.log CURRENT     100
     3 /u02/oracle/oradata/orcl/redo/redo03.log UNUSED	    100
     3 /u03/oracle/oradata/orcl/redo/redo03.log UNUSED	    100

	6 rows selected.

<br/>

	SQL> quit
