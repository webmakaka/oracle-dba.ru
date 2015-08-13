---
layout: page
title:  Создание rman скрипта для дупликата и его выполнение
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-script-for-duplicate-instance/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание rman скрипта для дупликата и его выполнение



### На Primary

<br/>

	$ cd /tmp/

<br/>

	$ vi rmanscript.rman


<br/>


The following example illustrates how to use DUPLICATE for active duplication. This example requires the NOFILENAMECHECK option because the primary database files have the same names as the standby database files. The SET clauses for SPFILE are required for log shipping to work properly. The db_unique_name must be set to ensure that the catalog and Data Guard can identify this database as being different from the primary.


DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET "db_unique_name"="slave" COMMENT "Is a duplicate"
    SET LOG_ARCHIVE_DEST_2="service=slave ASYNC REGISTER
     VALID_FOR=(online_logfile,primary_role)"
	SET FAL_SERVER="master" COMMENT "Is primary"
    SET FAL_CLIENT="slave" COMMENT "Is standby"
  NOFILENAMECHECK;


RMAN automatically copies the server parameter file to the standby host, starts the auxiliary instance with the server parameter file, restores a backup control file, and copies all necessary database files and archived redo logs over the network to the standby host. RMAN recovers the standby database, but does not place it in manual or managed recovery mode.

DORECOVER option to recover the database after standby creation



run {
	allocate channel prmy1 type disk;
	allocate auxiliary channel stby type disk;
	DUPLICATE TARGET DATABASE
	  FOR STANDBY
	  FROM ACTIVE DATABASE
	  DORECOVER
	  SPFILE
	    SET "db_unique_name"="slave" COMMENT "Is a duplicate"
	    SET LOG_ARCHIVE_DEST_2="service=slave ASYNC REGISTER
	     VALID_FOR=(online_logfile,primary_role)"
		SET FAL_SERVER="master" COMMENT "Is primary"
	    SET FAL_CLIENT="slave" COMMENT "Is standby"
		set standby_file_management='AUTO'
	  NOFILENAMECHECK;
}


==========================================================
==========================================================


run {
	allocate channel prmy1 type disk;
	allocate auxiliary channel stby type disk;
	duplicate target database for standby from active database spfile
		set db_unique_name='slave';
	}


	run {
	    allocate channel prmy1 type disk;
		allocate auxiliary channel stby type disk;
		duplicate target database for standby from active database spfile
			set db_unique_name='standby'
			set control_files='+DATA/standby/controlfile/control01.ctl'
			set log_archive_max_processes='5'
			set fal_server='orcl12'
			set standby_file_management='AUTO'
			set log_archive_config='dg_config=(orcl12,standby)'
			set log_archive_dest_1='LOCATION=+ARCH'
			set log_archive_dest_2='service=orcl12 LGWR ASYNC NOAFFIRM valid_for=(ONLINE_LOGFILE,PRIMARY_ROLE) db_unique_name=orcl12';
	     }


<br/>

fal_server - fetch archive log

<br/>

	$ rman CHECKSYNTAX @rmanscript.rman

	***
	The cmdfile has no syntax errors

Поехали:

	$ rman target sys/manager@primary auxiliary sys/manager@standby @rmanscript.rman

<br/>

	***
	Finished Duplicate Db at 12-AUG-15
	released channel: prmy1
	released channel: stby

	Recovery Manager complete.


<!--

SQL>  select to_char(CURRENT_SCN) CURRENT_SCN FROM V$DATABASE;

-->

http://docs.oracle.com/cd/B28359_01/server.111/b28294/rcmbackp.htm
