---
layout: page
title: Создание Snapshot StandBy (Сервер отчетов) в операционной системе Windows
description: Создание Snapshot StandBy (Сервер отчетов) в операционной системе Windows
keywords: Oracle DataBase, Windows, DataGuard, Snapshot StandBy
permalink: /database/installation/distributed/dataguard/windows/oracle/
---

# Создание Snapshot StandBy (Сервер отчетов)

<br/>

### Beta версия докумена. Необходимо проверить на реальных серверах! Если кто будет делать по этой версии документа, отпишитесь, что да как, где, что поправить.

<br/>

Создаем БД на том же сервере (можно как выше, но можно и проще):

Останавливаем StandBy Fbid

Копируем данные в REPORT

<br/>

Смотрим

```
SELECT NAME FROM V$DATAFILE;
```

<br/>

Если отличаются пути, то правим

<br/>

```
SQL> alter database rename file 'D:\ORADATA\FBID\AFWW.DBF' to 'd:\oradata\report\afww.dbf'
```

<br/>

**initREPORT.ora**

<br/>

```
report.__db_cache_size=2399141888
report.__java_pool_size=16777216
report.__large_pool_size=16777216
report.__oracle_base='c:\app\oracle'#ORACLE_BASE set from environment
report.__pga_aggregate_target=2483027968
report.__sga_target=6106906624
report.__shared_io_pool_size=0
report.__shared_pool_size=3623878656
report.__streams_pool_size=0
*._dbms_sql_security_level=384
*._optimizer_null_aware_antijoin=FALSE
*._pga_max_size=536870912
*.audit_file_dest='C:\APP\ORACLE\ADMIN\REPORT\ADUMP'
*.audit_trail='DB'
*.compatible='11.2.0.0.0'
*.control_files='D:\ORADATA\REPORT\CONTROL01.DBF','D:\ORADATA\REPORT\CONTROL02.DBF','D:\ORADATA\REPORT\CONTROL03.DBF'
*.db_block_size=8192
*.db_domain=''
*.db_name='fbid'
*.db_unique_name='report'
*.db_recovery_file_dest='d:\oradata\report\fast_recovery_area'
*.db_recovery_file_dest_size=397284474880
*.diagnostic_dest='C:\APP\ORACLE'
*.dispatchers='(PROTOCOL=TCP) (SERVICE=reportXDB)'
*.event=''
#*.fal_client='FBID'
#*.fal_server='FBID_PR'
*.job_queue_processes=30
#*.log_archive_dest_2='service=FBID_ST lgwr async NOAFFIRM optional reopen=180 valid_for=(online_logfiles, primary_role)'
#*.log_archive_dest_state_2='ENABLE'
#*.log_archive_min_succeed_dest=1
*.log_archive_dest_1='location=D:\oradata\report\fast_recovery_area\report\ARCHIVELOG'
#*.log_archive_dest_state_1='ENABLE' #
*.LOG_ARCHIVE_FORMAT='log_%t_%s_%r.dbf'
*.memory_target=32G  #8G#2181038080
*.nls_language='RUSSIAN'
*.nls_territory='RUSSIA'
*.open_cursors=2000
*.pga_aggregate_target=536870912
*.processes=1000
*.remote_login_passwordfile='EXCLUSIVE'
*.sec_case_sensitive_logon=FALSE
*.session_cached_cursors=200
*.undo_tablespace='UNDOTBS1'
*.utl_file_dir='D:\oradata\utl_dir\fbid','D:\oradata\utl_dir\fbid\GC','D:\oradata\utl_dir\fbid\TMP'
*.db_file_name_convert='d:\oradata\fbid','d:\oradata\report'
*.log_file_name_convert='d:\oradata\fbid','d:\oradata\report'
```

<br/>

### Запуск StandBy

```
Startup nomount
Alter database mount standby database exclusive;
```

<br/>

Меняем путь к архивлогам, указывая путь к логам существующего StandBy:

```
alter system set log_archive_dest_1='location=D:\oradata\fbid\fast_recovery_area\FBID\ARCHIVELOG' scope=memory;

// «бесконечная» накатка
recover managed standby database disconnect from session;

// до определенного времени
SQL> recover automatic standby database parallel 16 until time '2014-04-14:18:00:00';
```

<br/>

После доката логов переход в режим Snapshot, указывает путь к архивным файлам

```
alter system set log_archive_dest_1='location=D:\oradata\report\fast_recovery_area\report\ARCHIVELOG' scope=memory;

alter database flashback off;

alter database flashback on;

create restore point FBID guarantee flashback database;
```

<br/>

```
Restore point created.
```

<br/>

```
alter database activate standby database;
alter database open;
```

<br/>

### тест

```
select flashback_on from v$database;
```

Переход в режим докатки архивных логов:

```
SQL> startup mount force;
ORACLE instance started.
```

<br/>

```
Total System Global Area 6.8413E+10 bytes
Fixed Size                  2272320 bytes
Variable Size            6.5767E+10 bytes
Database Buffers         2550136832 bytes
Redo Buffers               93585408 bytes
Database mounted.
```

<br>

```
SQL> flashback database to restore point FBID;
```

<br/>

```
Flashback complete.
```

<br/>

```
SQL> alter database convert to physical standby;
```

<br/>

```
Database altered.
```

<br/>

```
SQL> startup mount force;
```

<br/>

```
ORACLE instance started.
Total System Global Area 6.8413E+10 bytes
Fixed Size                  2272320 bytes
Variable Size            6.5767E+10 bytes
Database Buffers         2550136832 bytes
Redo Buffers               93585408 bytes
Database mounted.
```

<br/>

```
SQL> drop restore point FBID;
```

<br/>

```
Restore point dropped.
```

<br/>

```
SQL> alter system set log_archive_dest_1='location=D:\oradata\fbid\fast_recovery_area\FBID\ARCHIVELOG' scope=memory;
```

<br/>

```
System altered.
```

<br/>

```
SQL> recover automatic standby database parallel 16 until time '2014-04-15:10:00:00';
```

<br/>

```
Media recovery complete.
```

<br/>

```
SQL> alter system set log_archive_dest_1='location=D:\oradata\report\fast_recove
ry_area\report\ARCHIVELOG' scope=memory;
```

<br/>

```
System altered.
```

<br/>

### Цикл обратно в открытый режим

```
SQL> alter database flashback off;
```

<br/>

```
Database altered.
```

<br/>

```
SQL> alter database flashback on;
```

<br/>

```
Database altered.
```

<br/>

```
SQL> create restore point FBID guarantee flashback database;
```

<br/>

```
Restore point created.
```

<br/>

```
SQL> alter database activate standby database;
```

<br/>

```
Database altered.
```

<br/>

```
SQL> alter database open;
```

<br/>

```
Database altered.
```

<br/>

### Скрипты для работы SnapshotStandBy

Запускаются от локального админа с правами ora_dba

// активатиция физического StandBy восстановление базы с помощью последних архивных логов на момент времени  
**to_PhStBy.bat**

<br/>

```
set oracle_sid=report
set ddate=%date:.=-%:5:00:00
ECHO OFF
echo recover automatic standby database parallel 16 until time '%date:~6%-%date:~3,-5%-%date:~0,-8%:5:00:00'; > D:\oradata\REPORT\fast_recovery_area\recover.sql
rem sqlplus /nolog
@D:\oradata\REPORT\fast_recovery_area\to_PhStBy.sql
```

<br/>

**to_PhStBy.sql**

```
set serveroutput on
set lines 200
spool D:\oradata\REPORT\fast_recovery_area\to_PhStBy.log

conn sys/sys as sysdba

startup mount force

conn sys/sys as sysdba

flashback database to restore point FBID;

alter database convert to physical standby;

startup mount force;

drop restore point FBID;

alter system set log_archive_dest_1='location=D:\oradata\fbid\fast_recovery_area\FBID\ARCHIVELOG' scope=memory;

@D:\oradata\report\fast_recovery_area\recover.sql

alter system set log_archive_dest_1='location=D:\oradata\report\fast_recovery_area\report\ARCHIVELOG' scope=memory;

spool off

exit;

```

<br/>

// активатиция SnapShot StandBy c FlashBack  
**to_PhStBy.bat**

<br/>

```
set oracle_sid=report
sqlplus /nolog @D:\oradata\REPORT\fast_recovery_area\to_SnStBy.sql
exit
```

<br/>

**to_PhStBy.sql**

```
set serveroutput on
set lines 200
spool D:\oradata\REPORT\fast_recovery_area\to_SnStBy.log
conn sys/sys as sysdba
alter database flashback off;
alter database flashback on;
create restore point FBID guarantee flashback database;
alter database activate standby database;
alter database open;
spool off

exit;
```

<br/>

### Примечание:

При неочередном бэкапе пром базы необходимо скопировать архивлог для последующего восстановления при необходимости (с другим SID): (скрипт RestTest10Arch.sql)

```
host ocopy D:\ORADATA\FBID\FAST_RECOVERY_AREA\FBID\ARCHIVELOG\LOG_1_44833_797622543.DBF \\S00000DPM001\ORACLE\FBID\ARCH\LOG_1_44833_797622543.DBF
```

<br/>

// на момент окончания бэкапа (докатка).  
**t.bat:**

<br/>

```
set oracle_sid=fbid

sqlplus system/system @D:\oradata\fbid\fast_recovery_area\t.sql

sqlplus system/system @D:\oradata\fbid\fast_recovery_area\a.sql

c:\blat\blat -body "@" -subject *ORA*ArchNeedCopy_FBID -to gvi@fbid.ru
```

<br/>

**t.sql:**

```
set lines 512
set pagesize 0 trimout on trimspool on verify off echo off feedback off
set serveroutput on

alter system archive log current;

spool D:\oradata\fbid\fast_recovery_area\a.sql

select 'host ocopy '||(select name from v$archived_log where
sequence# >=(select min(sequence#) from v$log_history where first_time>trunc(sysdate)+4/24+15/24/60)
and
sequence#<(
select min(sequence#) from v$log_history where  first_time>=(select completion_time from V$BACKUP_SET_DETAILS where controlfile_included='NO' and completion_time>trunc(sysdate) and
session_recid=(
select session_recid from V$RMAN_BACKUP_SUBJOB_DETAILS where  session_recid=(
select session_recid from V$BACKUP_SET_DETAILS where controlfile_included='NO' and completion_time>trunc(sysdate)
having bs_key=max(bs_key) group by session_recid,bs_key
) and status='COMPLETED' and input_type='DB FULL'
)
having bs_key=max(bs_key) group by completion_time,bs_key)
)
and dest_id=1)||' \\S00000DPM001\ORACLE\FBID\ARCH\'||
(select substr(name,instr(name,'\',-1)+1) from v$archived_log where
sequence# >=(select min(sequence#) from v$log_history where first_time>trunc(sysdate)+4/24+15/24/60)
and
sequence#<(
select min(sequence#) from v$log_history where  first_time>=(select completion_time from V$BACKUP_SET_DETAILS where controlfile_included='NO' and completion_time>trunc(sysdate) and
session_recid=(
select session_recid from V$RMAN_BACKUP_SUBJOB_DETAILS where  session_recid=(
select session_recid from V$BACKUP_SET_DETAILS where controlfile_included='NO' and completion_time>trunc(sysdate)
having bs_key=max(bs_key) group by session_recid,bs_key
) and status='COMPLETED' and input_type='DB FULL'
)
having bs_key=max(bs_key) group by completion_time,bs_key)
)
and dest_id=1) aa from dual;
select 'exit' from dual;
spool off
exit

```

<br/>

**a.sql:**

```
host ocopy D:\ORADATA\FBID\FAST_RECOVERY_AREA\FBID\ARCHIVELOG\LOG_1_44833_797622543.DBF \\S00000DPM001\ORACLE\FBID\ARCH\LOG_1_44833_797622543.DBF
exit
```

<br/>

## РАЗВЕРНУТО

**goto_PhSTby.bat**

```
set oracle_sid=XXXX
rem set ddate=%date:.=-%:5:00:00

ECHO ON

rem del /Q /F D:\oradata\XXXX\fast_recovery_area\recover.sql

rem echo recover automatic standby database parallel 16 until time '%date:~6%-%date:~3,-5%-%date:~0,-8%:3:00:00'; > D:\oradata\REPORT\fast_recovery_area\recover.sql

sqlplus /nolog @D:\oradata\XXXX\fast_recovery_area\goto_PhStBy.sql

exit
```

<br/>

**goto_PhStBy.sql**

```
set serveroutput on
set lines 200
spool D:\oradata\REPORT\fast_recovery_area\to_PhStBy.log

conn sys/sys as sysdba

startup mount force

conn sys/sys as sysdba

flashback database to restore point XXXX;

alter database convert to physical standby;

startup mount force;

drop restore point FBID;

alter system set log_archive_dest_1='location=c:\oradata\XXXX\fast_recovery_area\FBID\ARCHIVELOG' scope=memory;

--column u_time new_value u_t
--select to_char(sysdate,'YYYY-MM-DD:HH24:MM:SS') u_time from dual;
--recover automatic standby database parallel 16 until time '&u_t'
--alter system set log_archive_dest_1='location=D:\oradata\report\fast_recovery_area\report\ARCHIVELOG' scope=memory;

recover managed standby database disconnect from session;
--run StandBy
spool off

exit;
```

<br/>

**open_test_FlashBack.bat**

```
set oracle_sid=fbid
sqlplus /nolog @D:\oradata\XXX\fast_recovery_area\open_test_FB.sql
rem exit

open_test_SnStby.bat

set serveroutput on
set lines 200
spool D:\oradata\XXXX\fast_recovery_area\to_FB.log
conn sys/sys as sysdba
Startup nomount
Alter database mount standby database exclusive;
alter database flashback off;
alter database flashback on;
create restore point FBID guarantee flashback database;
alter database activate standby database;
alter database open;
spool off

exit;
```

<br/>

**purge.rman**

```
run {
    crosscheck backup of database completed before "SYSDATE-2";
    crosscheck backup of controlfile completed before "SYSDATE-2";
    crosscheck backup of archivelog  from time  "SYSDATE-2";
    delete noprompt expired backup of controlfile completed before "SYSDATE-2";
    delete noprompt expired backup of database completed before "SYSDATE-2";
    delete noprompt expired backup completed before "SYSDATE-2";
    delete noprompt expired archivelog  from time  "SYSDATE-2";
    delete noprompt backup of archivelog  from time  "SYSDATE-2";
    delete noprompt force archivelog all completed before 'SYSDATE-2';
    report obsolete;
    DELETE NOPROMPT OBSOLETE RECOVERY WINDOW OF 2 DAYS;
}
```

<br/>

**purgeAl.bat**

```
set ORACLE_SID=XXXX

rman target sys/sys nocatalog cmdfile=d:\oradata\XXXX\fast_recovery_area\purgeAL.rman log d:\oradata\fbid\fast_recovery_area\purgeAL.log

rem del /Q /F \\S00000DPM01\ORACLE\XXXX\DB\RestTest10Arch.sql
rem del /Q /F D:\oradata\fbid\fast_recovery_area\RestTest10Arch.sql
rem del /Q /F \\S00000DPM01\ORACLE\XXXX\DB\RestTest10Rec.sql
```

<br/>

**purgeAL.rman**

```
run {
    delete noprompt force archivelog all completed before 'SYSDATE-2';
}
```

<br/>

**to_SnStby.bat**

```
set oracle_sid=report
sqlplus /nolog @D:\oradata\REPORT\fast_recovery_area\to_SnStBy.sql
exit

to_SnStby.sql
set serveroutput on
set lines 200
spool D:\oradata\REPORT\fast_recovery_area\to_SnStBy.log
conn sys/sys as sysdba
alter database flashback off;
alter database flashback on;
create restore point FBID guarantee flashback database;
alter database activate standby database;
alter database open;
spool off

exit;
```
