---
layout: page
title: Oracle DataBase 12c - Linux -  Мультиплексирование controlfiles
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-controlfiles-multiplexing/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Мультиплексирование controlfiles



	$ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/CONTROLFILE
	$ mkdir -p /u03/oracle/oradata/12.2/${ORACLE_SID}/CONTROLFILE



<br/>

	$ sqlplus / as sysdba



<br/>

	SQL> select name from v$CONTROLFILE;

<br/>

	NAME
	--------------------------------------------------------------------------------
	/u02/oracle/oradata/12.1/orcl12/control01.ctl
	/u02/oracle/oradata/12.1/orcl12/control02.ctl


<br/>


	SQL> shutdown immediate;



<br/>

	SQL> quit

<br/>


	$ cp /u02/oracle/oradata/12.2/orcl/control01.ctl /u02/oracle/oradata/12.2/${ORACLE_SID}/CONTROLFILE/control01.ctl

	$ cp /u02/oracle/oradata/12.2/orcl/control01.ctl /u02/oracle/oradata/12.2/${ORACLE_SID}/CONTROLFILE/control02.ctl

	$ cp /u02/oracle/oradata/12.2/orcl/control01.ctl /u03/oracle/oradata/12.2/${ORACLE_SID}/CONTROLFILE/control03.ctl


<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> startup nomount;

<br/>

	SQL> ALTER SYSTEM SET control_files = '/u02/oracle/oradata/12.2/orcl12/CONTROLFILE/control01.ctl', '/u02/oracle/oradata/12.2/orcl12/CONTROLFILE/control02.ctl', '/u03/oracle/oradata/12.2/orcl12/CONTROLFILE/control03.ctl' scope=spfile;


<br/>

	SQL> shutdown immediate;

<br/>

	SQL> startup;

<br/>

	SQL> SELECT name FROM v$CONTROLFILE;

<br/>

	NAME
	--------------------------------------------------------------------------------
	/u02/oracle/oradata/12.1/orcl12/CONTROLFILE/control01.ctl
	/u02/oracle/oradata/12.1/orcl12/CONTROLFILE/control02.ctl
	/u03/oracle/oradata/12.1/orcl12/CONTROLFILE/control03.ctl


<br/>

	SQL> quit


Удаляем старые controlfile

	$ rm /u02/oracle/oradata/12.2/orcl/control01.ctl
	$ rm /u02/oracle/oradata/12.2/orcl/control02.ctl
