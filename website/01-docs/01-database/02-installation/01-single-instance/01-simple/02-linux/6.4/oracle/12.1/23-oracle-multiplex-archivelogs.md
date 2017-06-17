---
layout: page
title: Oracle DataBase 12c - Linux - Мультиплексирование archivelog
permalink: /database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-multiplex-archivelogs/
---

# <a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Мультиплексирование archivelog



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



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
