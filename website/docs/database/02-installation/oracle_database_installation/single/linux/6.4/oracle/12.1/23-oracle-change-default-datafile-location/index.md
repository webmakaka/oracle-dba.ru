---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle_database_installation/linux/6.4/oracle/12.1/oracle-change-default-datafile-location/
---

# <a href="/oracle_database_installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Изменение расположения файлов данных


<strong>!!! Правильно располагать файлы данных и индексы на разных дисках. (Я поленился и не описал это)</strong>


Создаем каталоги:

	$ mkdir -p /u02/oracle/oradata/orcl/data
	$ mkdir -p /u02/oracle/oradata/orcl/indexes
	$ mkdir -p /u02/oracle/oradata/orcl/undo
	$ mkdir -p /u02/oracle/oradata/orcl/temp

<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> select name from v$datafile;


<br/>

	NAME
	--------------------------------------------------------------------------------
	/u02/oracle/oradata/orcl/system01.dbf
	/u02/oracle/oradata/orcl/sysaux01.dbf
	/u02/oracle/oradata/orcl/undotbs01.dbf
	/u02/oracle/oradata/orcl/users01.dbf


<br/>

	SQL> shutdown immediate;


<br/>

    SQL> startup mount;


<br/>

	SQL> HOST mv /u02/oracle/oradata/orcl/system01.dbf /u02/oracle/oradata/orcl/data/system01.dbf
	SQL> HOST mv /u02/oracle/oradata/orcl/sysaux01.dbf /u02/oracle/oradata/orcl/data/sysaux01.dbf
	SQL> HOST mv /u02/oracle/oradata/orcl/users01.dbf /u02/oracle/oradata/orcl/data/users01.dbf
	SQL> HOST mv /u02/oracle/oradata/orcl/undotbs01.dbf /u02/oracle/oradata/orcl/undo/undotbs01.dbf

<br/>

	SQL> select name from v$tempfile;


<br/>

	NAME
	--------------------------------------------------------------------------------
	/u02/oracle/oradata/orcl/temp01.dbf


<br/>

	SQL> HOST mv /u02/oracle/oradata/orcl/temp01.dbf /u02/oracle/oradata/orcl/temp/temp01.dbf


<br/>


	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/orcl/system01.dbf' TO '/u02/oracle/oradata/orcl/data/system01.dbf';

	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/orcl/sysaux01.dbf' TO '/u02/oracle/oradata/orcl/data/sysaux01.dbf';

    SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/orcl/users01.dbf'  TO '/u02/oracle/oradata/orcl/data/users01.dbf';

	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/orcl/undotbs01.dbf' TO '/u02/oracle/oradata/orcl/undo/undotbs01.dbf';

	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/orcl/temp01.dbf' TO '/u02/oracle/oradata/orcl/temp/temp01.dbf';


 <br/>

	SQL> alter database open;

<br/>

	SQL> quit
