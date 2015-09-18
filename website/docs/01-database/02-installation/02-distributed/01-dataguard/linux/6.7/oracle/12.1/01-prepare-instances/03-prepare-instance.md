---
layout: page
title: Предварительные шаги по настройке параметров instance
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/prepare-instance/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Предварительные шаги по настройке параметров instance


### Primary


<br/>

	SQL> show parameter db_name

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	db_name 			     string	 orcl12


<br/>

	SQL> show parameter db_unique_name

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	db_unique_name			     string	 master


<br/>

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

	SQL> archive log list;
	Database log mode	       Archive Mode
	Automatic archival	       Enabled
	Archive destination	       USE_DB_RECOVERY_FILE_DEST
	Oldest online log sequence     8
	Next log sequence to archive   10
	Current log sequence	       10


<br/>

**ENABLE FORCE LOGGING**

Режим force logging нужен для принудительной записи транзакций в redo logs даже для операций, выполняемых с опцией NOLOGGING. Отсутствие этого режима может привести к тому, что на standby базе будут повреждены некоторые файлы данных, т.к. при «накатке» архивных журналов из них нельзя будет получить данные о транзакциях, выполненных с опцией NOLOGGING.

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


<br/>

### Посмотреть на свежие архивлоги

	SQL> alter system switch logfile;

<br/>

	SQL> select name from v$archived_log;

	NAME
	--------------------------------------------------------------------------------
	+ARCH/MASTER/ARCHIVELOG/2015_08_12/thread_1_seq_8.260.887572251


<br/>

	$ cd ~
	$ . asm.sh

<br/>

	$ asmcmd

<br/>

	ASMCMD> ls
	ARCHIVELOG/
	CONTROLFILE/

	ASMCMD> cd ARCHIVELOG

	ASMCMD> cd 2015_08_12

	ASMCMD> ls
	thread_1_seq_9.260.887541937
