---
layout: page
title: Oracle DataBase 12c - Linux -  Мультиплексирование controlfiles
permalink: /database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-multiplex-controlfiles/
---

# <a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Мультиплексирование controlfiles



	$ mkdir -p /u02/oracle/oradata/${ORACLE_SID}/control
	$ mkdir -p /u03/oracle/oradata/${ORACLE_SID}/control



<br/>

	$ sqlplus / as sysdba



<br/>

	SQL> select name from v$CONTROLFILE;

<br/>

	/u02/oracle/oradata/orcl/control01.ctl
	/u02/oracle/oradata/orcl/control02.ctl

<br/>


	SQL> shutdown immediate;



<br/>

	SQL> quit

<br/>


	$ cp /u02/oracle/oradata/${ORACLE_SID}/control01.ctl /u02/oracle/oradata/${ORACLE_SID}/control/control01.ctl

	$ cp /u02/oracle/oradata/${ORACLE_SID}/control01.ctl /u02/oracle/oradata/${ORACLE_SID}/control/control02.ctl

	$ cp /u02/oracle/oradata/${ORACLE_SID}/control01.ctl /u03/oracle/oradata/${ORACLE_SID}/control/control03.ctl


<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> startup nomount;

<br/>

	SQL> ALTER SYSTEM SET control_files = '/u02/oracle/oradata/orcl/control/control01.ctl', '/u02/oracle/oradata/orcl/control/control02.ctl', '/u03/oracle/oradata/orcl/control/control03.ctl' scope=spfile;


<br/>

	SQL> shutdown immediate;

<br/>

	SQL> startup;

<br/>

	SQL> SELECT name FROM v$CONTROLFILE;

<br/>

	/u02/oracle/oradata/orcl/control/control01.ctl
	/u02/oracle/oradata/orcl/control/control02.ctl
	/u03/oracle/oradata/orcl/control/control03.ctl

<br/>

	SQL> quit


Удаляем старые controlfile

	$ rm /u02/oracle/oradata/orcl/control01.ctl
	$ rm /u02/oracle/oradata/orcl/control02.ctl



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
