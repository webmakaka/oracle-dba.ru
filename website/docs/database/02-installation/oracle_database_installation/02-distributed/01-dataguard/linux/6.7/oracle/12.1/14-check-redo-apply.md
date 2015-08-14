---
layout: page
title:  Проверка применения redo
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-redo-apply/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Проверка применения redo



### Standby


Для начала посмотрим, что у нас за состояние instance

	SQL> select name,open_mode,log_mode from v$database;

	NAME	  OPEN_MODE	       LOG_MODE
	--------- -------------------- ------------
	ORCL12	  MOUNTED	       ARCHIVELOG


Далее выполняем на primary и standby, запрос который нам покажет количество архивлогов на узлах:

	SQL> select max(sequence#) from v$archived_log;

<br/>

Потом на primary, выполняем несколько раз команду:

	SQL> ALTER SYSTEM SWITCH LOGFILE


И сморим значения на узлах:

	SQL> select max(sequence#) from v$archived_log;




<br/>

	SQL> select recovery_mode from v$archive_dest_status;

	RECOVERY_MODE
	-----------------------
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE




Переводим нашу standby базу в режим Real-time apply redo:

	SQL> alter database recover managed standby database using current logfile disconnect;



Смотрим, что получилось:


	SQL> select recovery_mode from v$archive_dest_status;

	RECOVERY_MODE
	-----------------------
	MANAGED REAL TIME APPLY
	MANAGED REAL TIME APPLY
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE
	IDLE



<br/>

Если мы не хотим использовать режим Real-time apply redo, а хотим дожидаться когда будет закончено формирование очередного архивного журнала на основном сервере и он будет передан на standby для применения сохраненных в нем транзакций, то нам необходимо переводить нашу standby базу в режим redo apply командой:

	SQL> alter database recover managed standby database disconnect;

Если что-то пошло не так, то для решения проблемы в первую очередь необходимо остановить «накатку» логов:

	SQL> alter database recover managed standby database cancel;



<br/>

### Ошибка:


	SQL> alter database open;
	alter database open
	*
	ERROR at line 1:
	ORA-10456: cannot open standby database; media recovery session may be in
	progress


<br/>



	SQL> alter database recover managed standby database cancel;

<br/>

	SQL> alter database open;

<br/>

	SQL> alter database recover managed standby database using current logfile disconnect;



<br/>

### Какие-то запросы:


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
	1 BAD PARAM MOUNTED-STANDBY ARCH	IDLE
	MAXIMUM PERFORMANCE	      0 	 0	       0

	2 VALID     MOUNTED-STANDBY ARCH	IDLE
	MAXIMUM PERFORMANCE	      0 	 0	       0

	32 VALID     UNKNOWN	     ARCH	IDLE
	MAXIMUM PERFORMANCE	      0 	 0	       0



<br/>

	select * from v$recovery_progress;

<br/>

	SELECT to_char(COMPLETION_TIME,'dd-mon-yyyy hh24:mi:ss') FROM V$ARCHIVED_LOG WHERE APPLIED='YES';
	select timestamp, facility, dest_id, message_num, error_code, message from v$dataguard_status order by timestamp;

<br/>


	SQL> SELECT PROCESS, STATUS, THREAD#, SEQUENCE#, BLOCK#, BLOCKS FROM V$MANAGED_STANDBY;

	PROCESS   STATUS	  THREAD#  SEQUENCE#	 BLOCK#     BLOCKS
	--------- ------------ ---------- ---------- ---------- ----------
	ARCH	  CONNECTED		0	   0	      0 	 0
	ARCH	  CONNECTED		0	   0	      0 	 0
	ARCH	  CONNECTED		0	   0	      0 	 0
	ARCH	  CONNECTED		0	   0	      0 	 0
	ARCH	  CONNECTED		0	   0	      0 	 0
	MRP0	  WAIT_FOR_LOG		1	  36	      0 	 0

	6 rows selected.



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
