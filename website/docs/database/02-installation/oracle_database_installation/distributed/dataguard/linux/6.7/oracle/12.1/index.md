---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]:


# В разработке!
# В разработке!
# В разработке!

<!--

Madrid -> Primary -> dudas
Barcelona -> Secondary -> nodudas

-->

# В разработке!
# В разработке!
# В разработке!



Primary:  
Hostname: england  
Instance: london  
IP: 192.168.1.11  

StandBy:  
Hostname: spain  
Instance: madrid  
IP: 192.168.1.12  


Нужен пакет scp для копирования данных между серверами

	# yum install -y openssh-clients


1) Устанавливаю сервер как здесь
http://oracle-dba.ru/oracle-database-installation/asm/linux/6.7/oracle/12.1/


<br/>


### Primary и StandBy

<br/>

	# vi /etc/hosts

	***
	192.168.1.11 england.localdomain england
	192.168.1.12 spain.localdomain spain




### Primary (england)

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

	$ ps -edf | grep tns
	root        13     2  0 Aug09 ?        00:00:00 [netns]
	oracle12  6604     1  0 Aug09 ?        00:00:02 /u01/oracle/grid/12.1/bin/tnslsnr LISTENER -no_crs_notify -inherit
	oracle12 16991 14456  0 09:26 pts/1    00:00:00 grep tns


<br/>

	$ env | grep ORA
	ORACLE_UNQNAME=london
	ORACLE_SID=london
	ORACLE_BASE=/u01/oracle
	ORACLE_HOME=/u01/oracle/database/12.1



<br/>

	$ sqlplus / as sysdba

<br/>


	SQL> show parameter db_unique_name

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	db_unique_name			     string	 london


<br/>


	SQL> select name from v$database;

	NAME
	---------
	LONDON


<br/>


### ENABLE ARCHIVELOG


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





### FORCE_LOGGING


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

### Passwordfile

	SQL> show parameter remote_login_passwordfile

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	remote_login_passwordfile	     string	 EXCLUSIVE


<br/>

	$ chmod 4640 $ORACLE_HOME/dbs/orapwlondon



<br/>

<!--

Зачем-то удалили файл паролей и создали новый. Возможно, чтобы просто показать.

orapwd fiel=orapwdlondon password=oracle entries=5


-->


	$ scp $ORACLE_HOME/dbs/orapwlondon oracle12@spain:$ORACLE_HOME/dbs/orapwmadrid



## StandBy (Spain)

Переменные окружения главного сервера.

	#### Oracle Parameters ###########################

	    umask 022

	    export ORACLE_BASE=/u01/oracle
	    export ORACLE_HOME=$ORACLE_BASE/database/12.1

	    export GRID_HOME=$ORACLE_BASE/grid/12.1

	    export ORACLE_SID=madrid
	    export ORACLE_UNQNAME=madrid
	    export NLS_LANG=AMERICAN_AMERICA.AL32UTF8

	    export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin
	    export LD_LIBRARY_PATH=$ORACLE_HOME/lib

	    alias sqlplus='rlwrap sqlplus'
	    alias rman='rlwrap rman'

	#### Oracle Parameters ###########################



	$ chmod 4640 $ORACLE_HOME/dbs/orapwmadrid

################################################
### Block 2 Creation of the standby instance

	$ cd /u01/oracle/database/12.1/dbs


<br/>

	$ vi initmadrid.ora

<br/>

	db_name=london
	db_unique_name=madrid


<br/>

	$ sqlplus / as sysdba

	SQL*Plus: Release 12.1.0.2.0 Production on Mon Aug 10 12:42:29 2015

	Copyright (c) 1982, 2014, Oracle.  All rights reserved.

	Connected to an idle instance.

	SQL>


<br/>


	SQL> startup nomount pfile='initspain.ora'

<br/>

	$ ps -edf

	***
	oracle12  2783     1  0 12:50 ?        00:00:00 ora_pmon_madrid
	oracle12  2785     1  0 12:50 ?        00:00:00 ora_psp0_madrid
	oracle12  2787     1  3 12:50 ?        00:00:01 ora_vktm_madrid
	oracle12  2791     1  0 12:50 ?        00:00:00 ora_gen0_madrid
	oracle12  2793     1  0 12:50 ?        00:00:00 ora_mman_madrid
	oracle12  2797     1  0 12:50 ?        00:00:00 ora_diag_madrid
	oracle12  2799     1  0 12:50 ?        00:00:00 ora_dbrm_madrid
	oracle12  2801     1  0 12:50 ?        00:00:00 ora_vkrm_madrid
	oracle12  2803     1  0 12:50 ?        00:00:00 ora_dia0_madrid
	oracle12  2805     1  0 12:50 ?        00:00:00 ora_dbw0_madrid
	oracle12  2807     1  0 12:50 ?        00:00:00 ora_lgwr_madrid
	oracle12  2809     1  0 12:50 ?        00:00:00 ora_ckpt_madrid
	oracle12  2811     1  0 12:50 ?        00:00:00 ora_smon_madrid
	oracle12  2813     1  0 12:50 ?        00:00:00 ora_reco_madrid
	oracle12  2815     1  0 12:50 ?        00:00:00 ora_lreg_madrid
	oracle12  2817     1  0 12:50 ?        00:00:00 ora_pxmn_madrid
	oracle12  2819     1  0 12:50 ?        00:00:00 ora_mmon_madrid
	oracle12  2821     1  0 12:50 ?        00:00:00 ora_mmnl_madrid
	***

<br/>

	$ ps -edf | grep tns

<br/>

	$ ps -edf | grep tns
	root        13     2  0 08:47 ?        00:00:00 [netns]
	oracle12  2837  2656  0 12:52 pts/0    00:00:00 grep tns
	oracle12 30123     1  0 11:07 ?        00:00:00 /u01/oracle/grid/12.1/bin/tnslsnr LISTENER -no_crs_notify -inherit



Должен быть не в грид а в бд


	$ cd /u01/oracle/database/12.1/network/admin

<br/>

	$ vi listener.ora

<br/>

	LISTENER =
	  (ADDRESS_LIST=
	        (ADDRESS=(PROTOCOL=tcp)(HOST=spain)(PORT=1521))
	        (ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))

	 SID_LIST_LISTENER=
	   (SID_LIST=
	        (SID_DESC=
	          (GLOBAL_DBNAME=london)
	          (ORACLE_HOME=/u01/oracle/database/12.1)
	          (SID_NAME=madrid)
	        )
	    )


<br/>



	$ lsnrctl stop

<br/>

	$ lsnrctl start LISTENER

<br/>

	LSNRCTL for Linux: Version 12.1.0.2.0 - Production on 10-AUG-2015 13:07:31

	Copyright (c) 1991, 2014, Oracle.  All rights reserved.

	Starting /u01/oracle/database/12.1/bin/tnslsnr: please wait...

	TNSLSNR for Linux: Version 12.1.0.2.0 - Production
	System parameter file is /u01/oracle/database/12.1/network/admin/listener.ora
	Log messages written to /u01/oracle/diag/tnslsnr/spain/listener/alert/log.xml
	Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=spain.localdomain)(PORT=1521)))

	Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
	STATUS of the LISTENER
	------------------------
	Alias                     LISTENER
	Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
	Start Date                10-AUG-2015 13:07:31
	Uptime                    0 days 0 hr. 0 min. 0 sec
	Trace Level               off
	Security                  ON: Local OS Authentication
	SNMP                      OFF
	Listener Parameter File   /u01/oracle/database/12.1/network/admin/listener.ora
	Listener Log File         /u01/oracle/diag/tnslsnr/spain/listener/alert/log.xml
	Listening Endpoints Summary...
	  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=spain.localdomain)(PORT=1521)))
	The listener supports no services
	The command completed successfully


<br/>


	$ vi tnsnames.ora


<br/>

	LONDON =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = england.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = london)
	    )
	  )


	LONDON_DB =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = spain.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = london)
	    )
	  )

<br/>

	$ tnsping london

	TNS Ping Utility for Linux: Version 12.1.0.2.0 - Production on 10-AUG-2015 13:36:05

	Copyright (c) 1997, 2014, Oracle.  All rights reserved.

	Used parameter files:


	Used TNSNAMES adapter to resolve the alias
	Attempting to contact (DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = england.localdomain)(PORT = 1521)) (CONNECT_DATA = (SERVER = DEDICATED) (SERVICE_NAME = london)))
	OK (30 msec)


<br/>

	$ tnsping london_db

	TNS Ping Utility for Linux: Version 12.1.0.2.0 - Production on 10-AUG-2015 13:38:29

	Copyright (c) 1997, 2014, Oracle.  All rights reserved.

	Used parameter files:


	Used TNSNAMES adapter to resolve the alias
	Attempting to contact (DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = spain.localdomain)(PORT = 1521)) (CONNECT_DATA = (SERVER = DEDICATED) (SERVICE_NAME = london)))
	OK (10 msec)



### Primary england


	$ cd /u01/oracle/database/12.1/network/admin

	$ vi tnsnames.ora


<br/>

	# Было определено

	LONDON =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = england.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = london)
	    )
	  )

	# Добавил

	LONDON_DB =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = spain.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = london)
	    )
	  )


<br/>


	$ tnsping london

	TNS Ping Utility for Linux: Version 12.1.0.2.0 - Production on 10-AUG-2015 13:57:19

	Copyright (c) 1997, 2014, Oracle.  All rights reserved.

	Used parameter files:


	Used TNSNAMES adapter to resolve the alias
	Attempting to contact (DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = england.localdomain)(PORT = 1521)) (CONNECT_DATA = (SERVER = DEDICATED) (SERVICE_NAME = london)))
	OK (30 msec)

<br/>

	$ tnsping london_db

	TNS Ping Utility for Linux: Version 12.1.0.2.0 - Production on 10-AUG-2015 13:57:39

	Copyright (c) 1997, 2014, Oracle.  All rights reserved.

	Used parameter files:


	Used TNSNAMES adapter to resolve the alias
	Attempting to contact (DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = spain.localdomain)(PORT = 1521)) (CONNECT_DATA = (SERVER = DEDICATED) (SERVICE_NAME = london)))
	OK (10 msec)


################################################
### Block 2 Oracle net configuration


### Standby (Spain)


	SQL> select status from v$instance;

	STATUS
	------------------------------------
	STARTED

<br/>

	SQL> select instance_name from v$instance;

	INSTANCE_NAME
	------------------------------------------------
	madrid


<br/>

	SQL> show parameter listener

	NAME				     TYPE
	------------------------------------ ---------------------------------
	VALUE
	------------------------------
	listener_networks		     string

	local_listener			     string

	remote_listener 		     string



Local_listener - отсутствует

	SQL> alter system set local_listener = '(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=tcp)(HOST=spain)(PORT=1521))))';

<br/>

	SQL> show parameter listener

	NAME				     TYPE
	------------------------------------ ---------------------------------
	VALUE
	------------------------------
	listener_networks		     string

	local_listener			     string
	(DESCRIPTION=(ADDRESS_LIST=(AD
	DRESS=(PROTOCOL=tcp)(HOST=spai
	n)(PORT=1521))))
	remote_listener 		     string



<br/>


	$ rman target sys/manager@london

	Recovery Manager: Release 12.1.0.2.0 - Production on Mon Aug 10 13:55:54 2015

	Copyright (c) 1982, 2014, Oracle and/or its affiliates.  All rights reserved.

	connected to target database: LONDON (DBID=3222809710)


!!!!!!!!!!!!!!1
	$ rman target sys/manager@london_db

<br/>

Обращаем внимание на DBID=3222809710



### Primary

	SQL> select name, dbid from v$database;

	NAME		DBID
	--------- ----------
	LONDON	  3222809710


### StandBy


	$ rman target sys/manager@london auxiliary sys/manager@london_db


	7.25
