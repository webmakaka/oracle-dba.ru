---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /oracle_database_installation/linux/6.3/oracle/11.2/oracle-multiplex-archivelogs/
---

# <a href="/oracle_database_installation/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Мультиплексирование archivelog:


<br/>

Создание каталога для хранения файлов резервных копий и архивных журналов


	$ mkdir -p /u02/oradata/${ORACLE_SID}/archivelogs
	$ mkdir -p /u03/oradata/${ORACLE_SID}/archivelogs

<br/>

	$ sqlplus / as sysdba

Задать разделы для архивных журналов

	SQL>  ALTER SYSTEM SET LOG_ARCHIVE_DEST_1='location=/u02/oradata/ora112/archivelogs mandatory' scope=both;
	SQL>  ALTER SYSTEM SET LOG_ARCHIVE_DEST_2='location=/u03/oradata/ora112/archivelogs mandatory' scope=both;


Посмотреть текущие значения параметра LOG_ARCHIVE_DEST


	SQL> show parameter LOG_ARCHIVE_DEST;


Задать формат для файлов arhivelogs


	SQL>  ALTER SYSTEM SET LOG_ARCHIVE_FORMAT='%t_%s_%R.arc' scope=spfile;


<br/>

	SQL> quit
