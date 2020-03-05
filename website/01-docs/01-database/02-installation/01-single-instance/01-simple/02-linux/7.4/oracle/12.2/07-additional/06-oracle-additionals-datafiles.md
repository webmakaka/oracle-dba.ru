---
layout: page
title: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Расширение табличных пространств (создание дополнительных файлов для табличных пространств)
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Расширение табличных пространств (создание дополнительных файлов для табличных пространств)
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, tablespaces
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-additionals-datafiles/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Расширение табличных пространств (создание дополнительных файлов для табличных пространств)


<br/>

	$ sqlplus / as sysdba


Посмотреть какие файлы базы данных используются базой данных и где они расположены:


	SQL> set linesize 200;
	SQL> set pagesize 0;
	SQL> col name format a40;
	SQL> SELECT file#, name, status
	FROM v$datafile;


<br/>

**1) Создание нового табличное пространство для индексов и данных:**


	SQL> CREATE TABLESPACE "MY_DATA"
	DATAFILE '/u02/oracle/oradata/12.2/orcl12/DATAFILE/data/my_data01.dbf' SIZE 2G AUTOEXTEND OFF;


При необходимости, можно добавить дополнительное место для данных (когда будет такая необходимость) следующими командами:


	SQL> ALTER TABLESPACE “MY_DATA”
	ADD DATAFILE  '/u02/oracle/oradata/12.2/orcl12/DATAFILE/data/my_data02.dbf' SIZE 2G AUTOEXTEND OFF;

<br/>

	SQL> CREATE TABLESPACE "MY_INDEXES"
	DATAFILE '/u02/oracle/oradata/12.2/orcl12/DATAFILE/indexes/my_indexes01.dbf' SIZE 2G AUTOEXTEND OFF;


При необходимости, можно добавить дополнительное место для индексов (когда будет такая необходимость) следующими командами:


<br/>

	SQL> ALTER TABLESPACE “MY_INDEXES”
	ADD DATAFILE  '/u02/oracle/oradata/12.2/orcl12/DATAFILE/indexes/my_indexes02.dbf' SIZE 2G AUTOEXTEND OFF;


<br/>

**2) Иногда, нужно создать дополнительное табличное пространство для табличного пространства отмены (undo).**


	SQL> CREATE undo tablespace "UNDO" datafile '/u02/oracle/oradata/12.2/orcl12/DATAFILE/undo/undo01.dbf' size 1G autoextend off;


Определяю созданное табличное пространство, как пространство по умолчанию

	SQL> ALTER SYSTEM SET UNDO_TABLESPACE = "UNDO";



Удаляю старое табличное пространство


	SQL> drop tablespace UNDOTBS1;


<br/>

**3) Создать новое табличное пространство для временных данных.**


	SQL> CREATE TEMPORARY TABLESPACE "MY_TEMP"
	TEMPFILE '/u02/oracle/oradata/12.2/orcl12/DATAFILE/temp/my_temp01.dbf' SIZE 2G AUTOEXTEND OFF;


Добавить дополнительный файл для временных табличных пространств.


	SQL> ALTER TABLESPACE “MY_TEMP”
	ADD TEMPFILE '/u02/oracle/oradata/12.2/orcl12/DATAFILE/temp/my_temp02.dbf' SIZE 2G AUTOEXTEND OFF;


<br/>

	SQL> quit
