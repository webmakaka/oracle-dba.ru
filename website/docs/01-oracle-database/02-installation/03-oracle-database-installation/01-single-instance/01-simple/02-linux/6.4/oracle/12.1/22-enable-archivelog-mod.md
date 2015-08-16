---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle-database-installation/linux/6.4/oracle/12.1/enable-archivelog-mod/
---

# <a href="/oracle-database-installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Включить режим работы ARCHIVELOG



При работе в ARCHIVELOG, после переключения redo-log журналов, копия журнала архивируется и сохраняется на диске. Это позволяет при необходимости откатить базу данных на определенный момент в прошлом (например на конкретное время). При работе в ARCHIVELOG, появляется возможность создавать резервные копии базы данных не останавливая базу данных (горячий бекап). При данном режиме работы, необходимо выделять дополнительные ресурсы сервера, т.е. отнимать ресурсы у других процессов. По умолчанию данная опция отключена.


	$ sqlplus / as sysdba

Узнать режим работы базы данных:

	SQL> select log_mode from v$database;

<br/>

	LOG_MODE
	------------
	NOARCHIVELOG



Влючить archivelog (если выключен)


	SQL> shutdown immediate;
        SQL> startup mount exclusive;
        SQL> alter database archivelog;
        SQL> alter database open;

<br/>

<br/>

	SQL> select log_mode from v$database;



<br/>

	LOG_MODE
	------------------------------------
	ARCHIVELOG


Получить дополнительную информацию можно следующей командой:


	SQL> ARCHIVE LOG LIST

<br/>

	Database log mode              Archive Mode
	Automatic archival             Enabled
	Archive destination            USE_DB_RECOVERY_FILE_DEST
	Oldest online log sequence     30
	Next log sequence to archive   32
	Current log sequence           32



<br/>

	SQL> quit
