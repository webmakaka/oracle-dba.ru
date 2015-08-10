---
layout: page
title: Инсталляция Oracle DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/
---

# [Инсталляция Oracle DataGuard 12.1 в операционной системе Centos 6.7]:



Главный сервер:  
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

### Сервер england


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
