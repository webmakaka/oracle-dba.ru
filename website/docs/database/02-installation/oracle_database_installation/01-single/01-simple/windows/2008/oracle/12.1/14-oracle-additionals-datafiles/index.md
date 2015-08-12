---
layout: page
title: Инсталляция Oracle Database 12g Release 1 в Microsoft Windows 2008 Server
permalink: /oracle-database-installation/windows/2008/oracle/12.1/oracle-additionals-datafiles/
---

# <a href="/oracle-database-installation/windows/2008/oracle/12.1/">[Инсталляция Oracle Database 12g Release 1 в Microsoft Windows 2008 Server]</a>: Расширение табличных пространств (создание дополнительных файлов для табличных пространств)

<br/>

	sqlplus / as sysdba


Посмотреть какие файлы базы данных используются базой данных и где они расположены:

	SQL> set linesize 200;
	SQL> set pagesize 0;
	SQL> col name format a40;


<br/>

	SQL> SELECT file#, name, status
	FROM v$datafile;

<br/>

	SELECT file#, name, status
	FROM v$tempfile;

<br/>

### Создание нового табличное пространство для индексов и данных:

	SQL> CREATE TABLESPACE "MY_DATA"
	DATAFILE 'E:\app\oracle\oradata\ora121\data\my_data01.dbf' SIZE 2G AUTOEXTEND OFF;


При необходимости, можно добавить дополнительное место для данных (когда будет такая необходимость) следующими командами:

	SQL> ALTER TABLESPACE “MY_DATA”
	ADD DATAFILE  'E:\app\oracle\oradata\ora121\data\my_data02.dbf' SIZE 2G AUTOEXTEND OFF;


<br/>

	SQL> CREATE TABLESPACE "MY_INDEXES"
	DATAFILE 'E:\app\oracle\oradata\ora121\indexes\my_indexes01.dbf' SIZE 2G AUTOEXTEND OFF;

При необходимости, можно добавить дополнительное место для индексов (когда будет такая необходимость) следующими командами:

	SQL> ALTER TABLESPACE “MY_INDEXES”
	ADD DATAFILE  'E:\app\oracle\oradata\ora121\indexes\my_indexes02.dbf' SIZE 2G AUTOEXTEND OFF;

<br/>

### Создать дополнительное табличное пространство для табличного пространства отмены (undo).


	SQL> CREATE undo tablespace "UNDO" datafile 'E:\app\oracle\oradata\ora121\undo\undo01.dbf' size 1G autoextend off;


Определяю созданное табличное пространство, как пространство по умолчанию

	SQL> ALTER SYSTEM SET UNDO_TABLESPACE = "UNDO";


Удаляю старое табличное пространство

	SQL> drop tablespace UNDOTBS1;


Удалите старый файл табличного пространства (UNDOTBS01.DBF)

<br/>

### Создать новое табличное пространство для временных данных.


	SQL> CREATE TEMPORARY TABLESPACE "MY_TEMP" TEMPFILE 'E:\app\oracle\oradata\ora121\temp\my_temp01.dbf' SIZE 2G AUTOEXTEND OFF;


Добавить дополнительный файл для временных табличных пространств.


	SQL> ALTER TABLESPACE “MY_TEMP” ADD TEMPFILE 'E:\app\oracle\oradata\ora121\temp\my_temp02.dbf' SIZE 2G AUTOEXTEND OFF;

<br/>

	SQL> quit
