---
layout: page
title: Стартую instance на standby
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/startup-instance-on-standby/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Стартую instance на standby



### Standby


	$ cd $ORACLE_HOME/dbs

<br/>

	$ echo DB_NAME=orcl > initorcl.ora

<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> startup nomount pfile=$ORACLE_HOME/dbs/initorcl.ora

<br/>

	SQL> select status from v$instance;

	STATUS
	------------------------------------
	STARTED