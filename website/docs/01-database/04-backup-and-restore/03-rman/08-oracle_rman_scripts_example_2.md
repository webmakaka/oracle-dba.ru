---
layout: page
title: Скрипт RMAN для создания бекапов. Пример 2. Бекап в каталог
permalink: /docs/oracle-database/backup-and-restore/rman/oracle_rman_scripts_example/example2/
---

### Скрипт RMAN для создания бекапов. Пример 2. Бекап в каталог:

База 12С. Работает в режиме работы ARCHIVELOG


	$ mkdir -p /tmp/backups/ORCL12/{DATAFILE,ARCHIVELOG,CONTROLFILE,PARAMETERFILE}

<br/>

	$ mkdir -p $ORACLE_HOME/scripts

<br/>


	$ cd $ORACLE_HOME/scripts

<br/>

	$ vi backup-to-folder-rman-script.rman

<br/>

	RUN {

	ALLOCATE CHANNEL c1 DEVICE TYPE DISK;

	BACKUP AS COMPRESSED BACKUPSET FULL DATABASE TAG "FULL_DATABASE_DATAFILES" FORMAT '/tmp/backups/ORCL12/DATAFILE/bkp_%D_%T_%s_%p_DATA';

	SQL 'ALTER SYSTEM ARCHIVE LOG CURRENT';

	BACKUP ARCHIVELOG ALL FORMAT '/tmp/backups/ORCL12/ARCHIVELOG/bkp_%D_%T_%s_%p_ARCHIVELOG' TAG "FULL_DATABASE_ARCHIVELOGS";

	BACKUP SPFILE FORMAT '/tmp/backups/ORCL12/PARAMETERFILE/bkp_%D_%T_%s_%p_PARAM' TAG "FULL_DATABASE_SPFILE";

	SQL CREATE PFILE = '/tmp/backups/ORCL12/PARAMETERFILE/pfile.txt' from SPFILE;

	BACKUP CURRENT CONTROLFILE FORMAT '/tmp/backups/ORCL12/CONTROLFILE/bkp_%D_%T_%s_%p_CONTROL' TAG "FULL_DATABASE_CONTROLFILE";

	SQL ALTER DATABASE BACKUP CONTROLFILE TO TRACE as '/tmp/backups/ORCL12/CONTROLFILE/controlfile.txt';

	RELEASE CHANNEL c1;

	}

%t = 4 bytes time stamp  
%s = backup set number  
%p = backup piece number  



Проверка синтаксиса созданного файла сценария

	$ rman CHECKSYNTAX @$ORACLE_HOME/scripts/backup-to-folder-rman-script.rman

Выполнение скрипта резервного копирования

	$ rman target / @$ORACLE_HOME/scripts/backup-to-folder-rman-script.rman

<br/>

	SQL> select max(sequence#) from v$archived_log;

	MAX(SEQUENCE#)
	--------------
		    35

<br/>

	$ cd /tmp/backups/
	$ tar -cvzpf ORCL12.tar.gz ./ORCL12


<br/>

### Восстановление из бекапа

Я сначала попытался восстановить базу с другим именем инстанса. У меня ничего не получилось.
Я не смог выполнить ALTER DATABASE BACKUP CONTROLFILE TO TRACE as '/tmp/controlfile';

	$ ssh oracle12@piter "mkdir -p /tmp/backups/"
	$ scp ORCL12.tar.gz oracle12@192.168.1.12:/tmp/backups


Восстанавливаю на другом сервере с тем же инстансом:

	$ cd /tmp/backups/
	$ tar -xvzpf ORCL12.tar.gz ./
	./ORCL12/
	./ORCL12/DATAFILE/
	./ORCL12/DATAFILE/bkp_21_20150821_2_1_DATA
	./ORCL12/DATAFILE/bkp_21_20150821_1_1_DATA
	./ORCL12/PARAMETERFILE/
	./ORCL12/PARAMETERFILE/bkp_21_20150821_5_1_PARAM
	./ORCL12/CONTROLFILE/
	./ORCL12/CONTROLFILE/bkp_21_20150821_4_1_CONTROL
	./ORCL12/ARCHIVELOG/
	./ORCL12/ARCHIVELOG/bkp_21_20150821_3_1_ARCHIVELOG



<br/>

	$ export ORACLE_SID=ORCL12
    $ rman target / nocatalog


<br/>

	RMAN> startup nomount;

	startup failed: ORA-01078: failure in processing system parameters
	LRM-00109: could not open parameter file '/u01/oracle/database/12.1/dbs/initORCL12.ora'

	starting Oracle instance without parameter file for retrieval of spfile
	Oracle instance started

	Total System Global Area    1073741824 bytes

	Fixed Size                     2932632 bytes
	Variable Size                281018472 bytes
	Database Buffers             784334848 bytes
	Redo Buffers                   5455872 bytes




<br/>

	RMAN> restore spfile to pfile '/tmp/initorcl12.ora' from '/tmp/backups/ORCL12/PARAMETERFILE/bkp_21_20150821_5_1_PARAM';

<br/>

	$ cat /tmp/initorcl12.ora
	ORCL12.__data_transfer_cache_size=0
	ORCL12.__db_cache_size=822083584
	ORCL12.__java_pool_size=16777216
	ORCL12.__large_pool_size=33554432
	ORCL12.__oracle_base='/u01/oracle'#ORACLE_BASE set from environment
	ORCL12.__pga_aggregate_target=402653184
	ORCL12.__sga_target=1207959552
	ORCL12.__shared_io_pool_size=50331648
	ORCL12.__shared_pool_size=268435456
	ORCL12.__streams_pool_size=0
	*.audit_file_dest='/u01/oracle/admin/ORCL12/adump'
	*.audit_trail='db'
	*.compatible='12.1.0.2.0'
	*.control_files='+DATA/ORCL12/CONTROLFILE/current.261.888345847','+ARCH/ORCL12/CONTROLFILE/current.256.888345849'
	*.db_block_size=8192
	*.db_create_file_dest='+DATA'
	*.db_domain=''
	*.db_name='ORCL12'
	*.db_recovery_file_dest='+ARCH'
	*.db_recovery_file_dest_size=4560m
	*.diagnostic_dest='/u01/oracle'
	*.dispatchers='(PROTOCOL=TCP) (SERVICE=ORCL12XDB)'
	*.open_cursors=300
	*.pga_aggregate_target=382m
	*.processes=300
	*.remote_login_passwordfile='EXCLUSIVE'
	*.sga_target=1148m
	*.undo_tablespace='UNDOTBS1'


Вообщем обязательно нужно создать каталог для audit_file_dest

	$ mkdir -p /u01/oracle/admin/ORCL12/adump


Если ничего не меняется в конфигах (мой вариант), то можно воспользоваться командой:

    RMAN> restore spfile from '/tmp/backups/ORCL12/PARAMETERFILE/bkp_21_20150821_5_1_PARAM';

Если меяется то:

	RMAN> startup nomount pfile='/tmp/initorcl12.ora'



Восстановили spfile.


    RMAN> shutdown immediate;
    RMAN> startup nomount;


	RMAN> restore controlfile from '/tmp/backups/ORCL12/CONTROLFILE/bkp_21_20150821_4_1_CONTROL';

    RMAN> shutdown immediate;
	RMAN> startup mount;


Если расположение файлов, которые требуются для восстановления базы нужно явно указать. Это можно сделать следующими командами:

	RMAN> catalog start with '/tmp/wtf/ORCL12/DATAFILE';
	RMAN> catalog start with '/tmp/wtf/ORCL12/ARCHIVELOG';

Чтобы удалить EXPIRED данные

	RMAN> DELETE EXPIRED BACKUP;

<br/>

	RMAN> LIST BACKUP;


	List of Backup Sets
	===================


	BS Key  Type LV Size       Device Type Elapsed Time Completion Time
	------- ---- -- ---------- ----------- ------------ ---------------
	1       Full    336.77M    DISK        00:01:31     21-AUG-15
	        BP Key: 1   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_DATAFILES
	        Piece Name: /tmp/backups/ORCL12/DATAFILE/bkp_21_20150821_1_1_DATA
	  List of Datafiles in backup set 1
	  File LV Type Ckp SCN    Ckp Time  Name
	  ---- -- ---- ---------- --------- ----
	  1       Full 1679187    21-AUG-15 +DATA/ORCL12/DATAFILE/system.258.888345709
	  3       Full 1679187    21-AUG-15 +DATA/ORCL12/DATAFILE/sysaux.257.888345623
	  4       Full 1679187    21-AUG-15 +DATA/ORCL12/DATAFILE/undotbs1.260.888345795
	  6       Full 1679187    21-AUG-15 +DATA/ORCL12/DATAFILE/users.259.888345795

	BS Key  Type LV Size       Device Type Elapsed Time Completion Time
	------- ---- -- ---------- ----------- ------------ ---------------
	2       Full    1.03M      DISK        00:00:03     21-AUG-15
	        BP Key: 2   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_DATAFILES
	        Piece Name: /tmp/backups/ORCL12/DATAFILE/bkp_21_20150821_2_1_DATA
	  SPFILE Included: Modification time: 21-AUG-15
	  SPFILE db_unique_name: ORCL12
	  Control File Included: Ckp SCN: 1679322      Ckp time: 21-AUG-15

	BS Key  Size       Device Type Elapsed Time Completion Time
	------- ---------- ----------- ------------ ---------------
	3       1.20M      DISK        00:00:00     21-AUG-15
	        BP Key: 3   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_ARCHIVELOGS
	        Piece Name: /tmp/backups/ORCL12/ARCHIVELOG/bkp_21_20150821_3_1_ARCHIVELOG

	  List of Archived Logs in backup set 3
	  Thrd Seq     Low SCN    Low Time  Next SCN   Next Time
	  ---- ------- ---------- --------- ---------- ---------
	  1    22      1677757    21-AUG-15 1678819    21-AUG-15
	  1    23      1678819    21-AUG-15 1678838    21-AUG-15
	  1    24      1678838    21-AUG-15 1678908    21-AUG-15
	  1    25      1678908    21-AUG-15 1679140    21-AUG-15
	  1    26      1679140    21-AUG-15 1679143    21-AUG-15
	  1    27      1679143    21-AUG-15 1679146    21-AUG-15
	  1    28      1679146    21-AUG-15 1679149    21-AUG-15
	  1    29      1679149    21-AUG-15 1679152    21-AUG-15
	  1    30      1679152    21-AUG-15 1679155    21-AUG-15
	  1    31      1679155    21-AUG-15 1679158    21-AUG-15
	  1    32      1679158    21-AUG-15 1679161    21-AUG-15
	  1    33      1679161    21-AUG-15 1679164    21-AUG-15
	  1    34      1679164    21-AUG-15 1679341    21-AUG-15
	  1    35      1679341    21-AUG-15 1679349    21-AUG-15


<br/>

	RMAN> list backup of archivelog all;


	List of Backup Sets
	===================


	BS Key  Size       Device Type Elapsed Time Completion Time
	------- ---------- ----------- ------------ ---------------
	3       1.20M      DISK        00:00:00     21-AUG-15
	        BP Key: 3   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_ARCHIVELOGS
	        Piece Name: /tmp/backups/ORCL12/ARCHIVELOG/bkp_21_20150821_3_1_ARCHIVELOG

	  List of Archived Logs in backup set 3
	  Thrd Seq     Low SCN    Low Time  Next SCN   Next Time
	  ---- ------- ---------- --------- ---------- ---------
	  1    22      1677757    21-AUG-15 1678819    21-AUG-15
	  1    23      1678819    21-AUG-15 1678838    21-AUG-15
	  1    24      1678838    21-AUG-15 1678908    21-AUG-15
	  1    25      1678908    21-AUG-15 1679140    21-AUG-15
	  1    26      1679140    21-AUG-15 1679143    21-AUG-15
	  1    27      1679143    21-AUG-15 1679146    21-AUG-15
	  1    28      1679146    21-AUG-15 1679149    21-AUG-15
	  1    29      1679149    21-AUG-15 1679152    21-AUG-15
	  1    30      1679152    21-AUG-15 1679155    21-AUG-15
	  1    31      1679155    21-AUG-15 1679158    21-AUG-15
	  1    32      1679158    21-AUG-15 1679161    21-AUG-15
	  1    33      1679161    21-AUG-15 1679164    21-AUG-15
	  1    34      1679164    21-AUG-15 1679341    21-AUG-15
	  1    35      1679341    21-AUG-15 1679349    21-AUG-15


<br/>


Нужно, чтобы статус был AVAILABLE


	RMAN> RESTORE DATABASE VALIDATE;
	RMAN> RESTORE ARCHIVELOG ALL VALIDATE;

<br/>

	RMAN> restore database;

	Starting restore at 21-AUG-15
	using channel ORA_DISK_1

	channel ORA_DISK_1: starting datafile backup set restore
	channel ORA_DISK_1: specifying datafile(s) to restore from backup set
	channel ORA_DISK_1: restoring datafile 00001 to +DATA/ORCL12/DATAFILE/system.258.888345709
	channel ORA_DISK_1: restoring datafile 00003 to +DATA/ORCL12/DATAFILE/sysaux.257.888345623
	channel ORA_DISK_1: restoring datafile 00004 to +DATA/ORCL12/DATAFILE/undotbs1.260.888345795
	channel ORA_DISK_1: restoring datafile 00006 to +DATA/ORCL12/DATAFILE/users.259.888345795
	channel ORA_DISK_1: reading from backup piece /tmp/backups/ORCL12/DATAFILE/bkp_21_20150821_1_1_DATA
	channel ORA_DISK_1: piece handle=/tmp/backups/ORCL12/DATAFILE/bkp_21_20150821_1_1_DATA tag=FULL_DATABASE_DATAFILES
	channel ORA_DISK_1: restored backup piece 1
	channel ORA_DISK_1: restore complete, elapsed time: 00:02:45
	Finished restore at 21-AUG-15



sequence = max secuence + 1

	RMAN> run {
	set until sequence 36;
	recover database;
	}

<br/>

	RMAN> alter database open resetlogs;

<br/>

	SQL> select max(sequence#) from v$archived_log;

	MAX(SEQUENCE#)
	--------------
		    35


После рекомендуется сделать полный бекап.


<br/>

### PS. Если нужно переименовывать


	run {
		SET NEWNAME FOR DATABASE   TO  '/u01/app/oracle/oradata/orcl/%b';
		SET NEWNAME FOR tempfile  1 TO  '/u01/app/oracle/oradata/orcl/%b';
		restore database;
		switch datafile all;
		switch tempfile all;
	}


см.

http://gavinsoorma.com/2013/02/restoring-a-asm-backup-to-non-asm-and-restoring-from-rac-to-single-instance/

http://docs.oracle.com/cd/B12037_01/server.101/b10735/recov.htm
