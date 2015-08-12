---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /oracle-database-installation/linux/6.3/oracle/11.2/oracle-cold-backup/
---

# <a href="/oracle-database-installation/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Создание резервной копии созданной базы данных (холодный backup):


<br/>

	$ sqlplus / as sysdba

<br/>


	SQL> alter system set db_recovery_file_dest_size = 25G;

<br/>


	SQL> alter system set db_recovery_file_dest="/u03/orabackups/";


<br/>


	SQL> shutdown immediate;
	SQL> startup mount;
	SQL> quit

<br/>

	$ rman target /

<br/>

	RMAN> backup full database noexclude include current controlfile spfile TAG "FULL_COLD_BACKUP";

<br/>

	RMAN> sql 'alter database open';

<br/>

	// Посмотреть, какие бекапы имеются
	RMAN> list backup summary;

<br/>

	RMAN> quit
