---
layout: page
title: Oracle DataBase 12c - Linux - Изменение расположения файлов данных
permalink: /database/installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-change-default-datafile-location/
---

# <a href="/database/installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Изменение расположения файлов данных


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



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
