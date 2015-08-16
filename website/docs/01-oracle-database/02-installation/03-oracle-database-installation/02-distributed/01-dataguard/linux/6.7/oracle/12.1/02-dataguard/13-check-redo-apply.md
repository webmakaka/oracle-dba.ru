---
layout: page
title:  Проверка применения redo
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/dataguard/linux/6.7/oracle/12.1/check-redo-apply/
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

### Open Standby Database Read Only

	SQL> shutdown immediate;
	SQL> startup mount;
	SQL> alter database open read only;


<br/>

	SQL> select name, open_mode, log_mode, database_role from v$database;

	NAME	  OPEN_MODE	       LOG_MODE     DATABASE_ROLE
	--------- -------------------- ------------ ----------------
	ORCL12	  READ ONLY WITH APPLY ARCHIVELOG   PHYSICAL STANDBY




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
