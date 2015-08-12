---
layout: page
title: Предварительные шаги по настройке environment
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/prepare-env/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Предварительные шаги по настройке environment


### Следующие шаги выполняются на Primary и Standby


Все время забываю, где прописывается hostname сервера

	# vi /etc/sysconfig/network

**После переименования, лучше перезагрузить сервер или каким-то способом применить изменения, или иначе в конфигах будет прописано что-то не то и придется их потом еще и править**

<br/>

Устанавливаю пакет scp для копирования данных между серверами на обоих узлах

	# yum install -y openssh-clients


<br/>

	# vi /etc/hosts

<br/>

	## Localdomain and Localhost

	127.0.0.1 localhost.localdomain localhost


	## DataBases

	# moscow - primary; piter - standby

	192.168.1.11 moscow.localdomain moscow
	192.168.1.12 piter.localdomain piter


<br/>


	vi /home/oracle12/.bash_profile

<br/>

	#### Oracle Parameters ###########################

		umask 022

		export ORACLE_BASE=/u01/oracle
		export ORACLE_HOME=$ORACLE_BASE/database/12.1

		export GRID_HOME=$ORACLE_BASE/grid/12.1

		export ORACLE_SID=orcl
		export ORACLE_UNQNAME=orcl
		export NLS_LANG=AMERICAN_AMERICA.AL32UTF8

		export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin
		export LD_LIBRARY_PATH=$ORACLE_HOME/lib

		alias sqlplus='rlwrap sqlplus'
		alias rman='rlwrap rman'

	#### Oracle Parameters ###########################


<br/>

### Primary

**ENABLE ARCHIVELOG**


	SQL> archive log list;
	Database log mode	       No Archive Mode
	Automatic archival	       Disabled
	Archive destination	       USE_DB_RECOVERY_FILE_DEST
	Oldest online log sequence     8
	Current log sequence	       10

<br/>

	SQL> shutdown immediate;
	SQL> startup mount;
	SQL> alter database archivelog;
	SQL> alter database open;

<br/>

	SQL>  archive log list;
	Database log mode	       Archive Mode
	Automatic archival	       Enabled
	Archive destination	       USE_DB_RECOVERY_FILE_DEST
	Oldest online log sequence     8
	Next log sequence to archive   10
	Current log sequence	       10

<br/>

	SQL> select name, total_mb, free_mb from v$asm_diskgroup;

	NAME				 TOTAL_MB    FREE_MB
	------------------------------ ---------- ----------
	DATA				   245754     241163



<br/>

**FORCE_LOGGING**


	SQL> select force_logging from v$database;

	FORCE_LOGGING
	---------------------------------------
	NO


<br/>

	SQL> alter database force logging;


<br/>

	SQL> select force_logging from v$database;

	FORCE_LOGGING
	---------------------------------------
	YES
