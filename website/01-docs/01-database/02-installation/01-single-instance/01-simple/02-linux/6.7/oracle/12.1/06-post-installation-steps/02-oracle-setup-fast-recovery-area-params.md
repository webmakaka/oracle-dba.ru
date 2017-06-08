---
layout: page
title: Oracle DataBase 12c - Linux - Задание параметров FAST RECOVERY AREA
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/oracle-setup-fast-recovery-area-params/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Задание параметров FAST RECOVERY AREA


<br/>

Fast Recovery Area (FRA) - это пространство для резервных копий базы данных и файлов архивных журналов (если включен рехим создания архивов redo журналов). Необходимо следить за тем, чтобы у базы данных оставалось место для записи в него своих данных. При необходимости, его можно увеличивать и/или очищать от устаревших данных. Чистить можно только средствами RMAN.

<br/>

	$ sqlplus / as sysdba


<br/>


	SQL> alter system set db_recovery_file_dest_size="20G";

<br/>

	SQL> alter system set db_recovery_file_dest="/u03/oracle/oradata/12.1/orcl12/backups";

<br/>

	SQL> show parameter db_recovery;

<br/>

	SQL> show parameter db_recovery;

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	db_recovery_file_dest		     string	 /u03/oracle/oradata/12.1/orcl12/backups
	db_recovery_file_dest_size	     big integer 20G
