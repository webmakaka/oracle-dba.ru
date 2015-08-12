---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/11/
---



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



	SQL> show parameter db_unique_name

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	db_unique_name			     string	 london



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
