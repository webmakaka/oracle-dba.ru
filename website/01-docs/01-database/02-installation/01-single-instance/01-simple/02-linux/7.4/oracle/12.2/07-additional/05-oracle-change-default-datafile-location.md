---
layout: page
title: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Изменение расположения файлов данных
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Изменение расположения файлов данных
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, файлы данных
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-change-default-datafile-location/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Изменение расположения файлов данных


<strong>!!! Правильно располагать файлы данных и индексы на разных дисках. (Я поленился и не описал это)</strong>


Создаем каталоги:

	$ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/data
	$ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/indexes
	$ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/undo
	$ mkdir -p /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/temp

<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> select name from v$datafile;


<br/>

	NAME
	--------------------------------------------------------------------------------
    /u02/oracle/oradata/12.2/orcl/system01.dbf
    /u02/oracle/oradata/12.2/orcl/sysaux01.dbf
    /u02/oracle/oradata/12.2/orcl/undotbs01.dbf
    /u02/oracle/oradata/12.2/orcl/users01.dbf



<br/>

	SQL> shutdown immediate;


<br/>

    SQL> startup mount;


<br/>

	SQL> HOST mv /u02/oracle/oradata/12.2/orcl/system01.dbf /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/data/system01.dbf
	SQL> HOST mv /u02/oracle/oradata/12.2/orcl/sysaux01.dbf /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/data/sysaux01.dbf
	SQL> HOST mv /u02/oracle/oradata/12.2/orcl/users01.dbf /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/data/users01.dbf

	SQL> HOST mv /u02/oracle/oradata/12.2/orcl/undotbs01.dbf /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/undo/undotbs01.dbf

<br/>

	SQL> select name from v$tempfile;


<br/>

	NAME
	--------------------------------------------------------------------------------
	/u02/oracle/oradata/12.2/orcl/temp01.dbf


<br/>

	SQL> HOST mv /u02/oracle/oradata/12.2/orcl/temp01.dbf /u02/oracle/oradata/12.2/${ORACLE_SID}/DATAFILE/temp/temp01.dbf


<br/>


	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/12.2/orcl/system01.dbf' TO '/u02/oracle/oradata/12.2/orcl12/DATAFILE/data/system01.dbf';

	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/12.2/orcl/sysaux01.dbf' TO '/u02/oracle/oradata/12.2/orcl12/DATAFILE/data/sysaux01.dbf';

    SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/12.2/orcl/users01.dbf'  TO '/u02/oracle/oradata/12.2/orcl12/DATAFILE/data/users01.dbf';


<br/>

	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/12.2/orcl/undotbs01.dbf' TO '/u02/oracle/oradata/12.2/orcl12/DATAFILE/undo/undotbs01.dbf';

	SQL> ALTER DATABASE RENAME FILE '/u02/oracle/oradata/12.2/orcl/temp01.dbf' TO '/u02/oracle/oradata/12.2/orcl12/DATAFILE/temptemp01.dbf';


 <br/>

	SQL> alter database open;

<br/>

	SQL> quit
