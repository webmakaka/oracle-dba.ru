---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-multiplex-archivelogs/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Мультиплексирование archivelog



Создание каталога для хранения файлов резервных копий и архивных журналов

	$ mkdir -p /u02/oracle/oradata/${ORACLE_SID}/archives
	$ mkdir -p /u03/oracle/oradata/${ORACLE_SID}/archives

<br/>

	$ sqlplus / as sysdba

Задать разделы для архивных журналов

	SQL>  ALTER SYSTEM SET LOG_ARCHIVE_DEST_1='location=/u02/oracle/oradata/orcl/archives mandatory' scope=both;

	SQL>  ALTER SYSTEM SET LOG_ARCHIVE_DEST_2='location=/u03/oracle/oradata/orcl/archives mandatory' scope=both;


Посмотреть текущие значения параметра LOG_ARCHIVE_DEST

	SQL> show parameter LOG_ARCHIVE_DEST;


Задать формат для файлов arhivelogs


	SQL> ALTER SYSTEM SET LOG_ARCHIVE_FORMAT='%t_%s_%R.arc' scope=spfile;


<br/>

	SQL> quit
