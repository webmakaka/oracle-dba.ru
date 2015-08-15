---
layout: page
title:  Запросы для получения данных о работе DataGuard
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/queries/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Запросы для получения данных о работе DataGuard



	SQL> select name, db_unique_name, database_role, protection_mode from v$database;

	NAME	  DB_UNIQUE_NAME		 DATABASE_ROLE	  PROTECTION_MODE
	--------- ------------------------------ ---------------- --------------------
	ORCL12	  slave 			 PHYSICAL STANDBY MAXIMUM PERFORMANCE


<br/>

	SQL> SELECT name, value, datum_time, time_computed FROM V$DATAGUARD_STATS;

<br/>


	SQL> SELECT to_char(COMPLETION_TIME,'dd-mon-yyyy hh24:mi:ss') FROM V$ARCHIVED_LOG WHERE APPLIED='YES';

	TO_CHAR(COMPLETION_TIME,'DD-M
	-----------------------------
	13-aug-2015 19:47:34
	13-aug-2015 19:47:35


<br/>

	SQL> select switchover_status from v$database;

	SWITCHOVER_STATUS
	--------------------
	NOT ALLOWED

<br/>

	select     ds.dest_id id
	,     ad.status
	,     ds.database_mode db_mode
	,     ad.archiver type
	,     ds.recovery_mode
	,     ds.protection_mode
	,     ds.standby_logfile_count "SRLs"
	,     ds.standby_logfile_active active
	,     ds.archived_seq#
	from     v$archive_dest_status     ds
	,     v$archive_dest          ad
	where     ds.dest_id = ad.dest_id
	and     ad.status != 'INACTIVE'
	order by
	     ds.dest_id;

<br/>


	ID STATUS    DB_MODE	     TYPE	RECOVERY_MODE
	---------- --------- --------------- ---------- -----------------------
	PROTECTION_MODE 	   SRLs     ACTIVE ARCHIVED_SEQ#
	-------------------- ---------- ---------- -------------
	1 VALID     OPEN_READ-ONLY  ARCH	MANAGED REAL TIME APPLY
	MAXIMUM PERFORMANCE	      0 	 0	      50

	2 DEFERRED  UNKNOWN	     LGWR	IDLE
	MAXIMUM PERFORMANCE	      0 	 0	       0

	32 VALID     UNKNOWN	     ARCH	IDLE
	MAXIMUM PERFORMANCE	      0 	 0	      50




<br/>

	select * from v$recovery_progress;

<br/>

	SELECT to_char(COMPLETION_TIME,'dd-mon-yyyy hh24:mi:ss') FROM V$ARCHIVED_LOG WHERE APPLIED='YES';
	select timestamp, facility, dest_id, message_num, error_code, message from v$dataguard_status order by timestamp;

<br/>


	SQL> SELECT PROCESS, STATUS, THREAD#, SEQUENCE#, BLOCK#, BLOCKS FROM V$MANAGED_STANDBY;

	PROCESS   STATUS	  THREAD#  SEQUENCE#	 BLOCK#     BLOCKS
	--------- ------------ ---------- ---------- ---------- ----------
	ARCH	  CLOSING		1	  49	      1 	 2
	ARCH	  CONNECTED		0	   0	      0 	 0
	ARCH	  CONNECTED		0	   0	      0 	 0
	ARCH	  CLOSING		1	  50	      1 	26
	MRP0	  APPLYING_LOG		1	  51	   2486     102400
	RFS	  IDLE			0	   0	      0 	 0
	RFS	  IDLE			1	  51	   2486 	 1
	RFS	  IDLE			0	   0	      0 	 0

	8 rows selected.




<br/>

	SQL>  select * from v$archive_gap;

	no rows selected


<br/>

	SQL> select message from v$dataguard_status;

	MESSAGE
	--------------------------------------------------------------------------------
	ARC0: Archival started
	ARC1: Archival started
	ARC2: Archival started
	ARC3: Archival started
	ARC1: Becoming the 'no FAL' ARCH
	ARC2: Becoming the heartbeat ARCH
	ARC2: Becoming the active heartbeat ARCH
	ARC4: Archival started
	Error 12154 received logging on to the standby
	FAL[client, ARC0]: Error 12154 connecting to master for fetching gap sequence
	Managed Standby Recovery not using Real Time Apply

	MESSAGE
	--------------------------------------------------------------------------------
	Attempt to start background Managed Standby Recovery process
	MRP0: Background Managed Standby Recovery process started
	Managed Standby Recovery starting Real Time Apply
	Media Recovery Waiting for thread 1 sequence 36

	15 rows selected.


<br/>

	SQL> SELECT THREAD#, SEQUENCE#, APPLIED FROM V$ARCHIVED_LOG;

	   THREAD#  SEQUENCE# APPLIED
	---------- ---------- ---------
		 1	   34 YES
		 1	   35 YES



<br/>


	SQL> SELECT RECOVERY_MODE FROM V$ARCHIVE_DEST_STATUS WHERE DEST_ID=2;

	RECOVERY_MODE
	-----------------------
	IDLE
