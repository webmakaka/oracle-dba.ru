---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /oracle_database_installation/linux/6.3/oracle/11.2/oracle-multiplex-controlfiles/
---

# <a href="/oracle_database_installation/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Мультиплексирование controlfiles:


<br/>


	$ mkdir -p /u02/oradata/${ORACLE_SID}/control
	$ mkdir -p /u03/oradata/${ORACLE_SID}/control



<br/>

	$ sqlplus / as sysdba


<br/>


	SQL> select name from v$CONTROLFILE;

<br/>

	NAME
	--------------------------------------------------------------------------------
	/u02/oradata/ora112/control01.ctl
	/u02/oradata/ora112/control02.ctl


<br/>

	SQL> shutdown immediate;



<br/>

	SQL> quit

<br/>

	$ cp /u02/oradata/ora112/control01.ctl /u02/oradata/${ORACLE_SID}/control/control01.ctl
	$ cp /u02/oradata/ora112/control01.ctl /u02/oradata/${ORACLE_SID}/control/control02.ctl
	$ cp /u02/oradata/ora112/control01.ctl /u03/oradata/${ORACLE_SID}/control/control03.ctl



<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> startup nomount;

<br/>

	SQL> ALTER SYSTEM SET control_files = '/u02/oradata/ora112/control/control01.ctl', '/u02/oradata/ora112/control/control02.ctl', '/u03/oradata/ora112/control/control03.ctl' scope=spfile;

<br/>

	SQL> shutdown immediate;

<br/>

	SQL> startup;

<br/>

	SQL> SELECT name FROM v$CONTROLFILE;

<br/>

	NAME
	--------------------------------------------------------------------------------
	/u02/oradata/ora112/control/control01.ctl
	/u02/oradata/ora112/control/control02.ctl
	/u03/oradata/ora112/control/control03.ctl

<br/>

	SQL> quit


<br/>


Удаляем старые controlfile

	$ rm /u02/oradata/ora112/control01.ctl
	$ rm /u02/oradata/ora112/control02.ctl
