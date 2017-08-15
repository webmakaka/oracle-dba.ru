---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Мультиплексирование archivelog
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-archivelogs-multiplexing/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Мультиплексирование archivelog



Создание каталога для хранения файлов резервных копий и архивных журналов

	$ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/ARCHIVELOG
	$ mkdir -p /u03/oracle/oradata/12.2/${ORACLE_SID}/ARCHIVELOG

<br/>

	$ sqlplus / as sysdba

Задать разделы для архивных журналов

	SQL> ALTER SYSTEM SET LOG_ARCHIVE_DEST_1='location=/u02/oracle/oradata/12.2/orcl12/ARCHIVELOG mandatory' scope=both;

	SQL> ALTER SYSTEM SET LOG_ARCHIVE_DEST_2='location=/u03/oracle/oradata/12.2/orcl12/ARCHIVELOG mandatory' scope=both;


Посмотреть текущие значения параметра LOG_ARCHIVE_DEST

	SQL> show parameter LOG_ARCHIVE_DEST;


Задать формат для файлов arhivelogs


	SQL> ALTER SYSTEM SET LOG_ARCHIVE_FORMAT='%t_%s_%R.arc' scope=spfile;

<br/>

	SQL> quit
