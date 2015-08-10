---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]:



Primary:  
Hostname: england  
Instance: london  
IP: 192.168.1.11  

StandBy:  
Hostname: spain  
Instance: madrid  
IP: 192.168.1.12  


1) Устанавливаю сервер как здесь
http://oracle-dba.ru/oracle-database-installation/asm/linux/6.7/oracle/12.1/


<br/>

### Primary


<br/>

	# vi /etc/hosts

	***
	192.168.1.11 england.localdomain england
	192.168.1.12 spain.localdomain spain


<br/>

Переменные окружения главного сервера.

	#### Oracle Parameters ###########################

	    umask 022

	    export ORACLE_BASE=/u01/oracle
	    export ORACLE_HOME=$ORACLE_BASE/database/12.1

	    export GRID_HOME=$ORACLE_BASE/grid/12.1

	    export ORACLE_SID=london
	    export ORACLE_UNQNAME=london
	    export NLS_LANG=AMERICAN_AMERICA.AL32UTF8

	    export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin
	    export LD_LIBRARY_PATH=$ORACLE_HOME/lib

	    alias sqlplus='rlwrap sqlplus'
	    alias rman='rlwrap rman'

	#### Oracle Parameters ###########################


<br/>

	$ ps -edf | grep pmon
	oracle12  6902     1  0 Aug09 ?        00:00:05 asm_pmon_+ASM
	oracle12 13205     1  0 Aug09 ?        00:00:05 ora_pmon_london
	oracle12 14498 14456  0 08:24 pts/1    00:00:00 grep pmon


<br/>

	$ sqlplus / as sysdba

<br/>


	SQL> archive log list;
	Database log mode	       No Archive Mode
	Automatic archival	       Disabled
	Archive destination	       USE_DB_RECOVERY_FILE_DEST
	Oldest online log sequence     8
	Current log sequence	       10

<br/>


	SQL> ALTER DATABASE ARCHIVELOG;

<br/>


	SQL> select force_logging from v$database;

	FORCE_LOGGING
	---------------------------------------
	NO


<br/>

	SQL> ALTER DATABASE FORCE LOGGING;
