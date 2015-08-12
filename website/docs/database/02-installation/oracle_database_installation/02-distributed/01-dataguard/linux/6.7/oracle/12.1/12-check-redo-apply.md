---
layout: page
title:  Проверка применения redo
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-redo-apply/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Проверка применения redo



	SQL> show parameter dump

background_dump_dest - расположение alert log файла


### НА Primary и Standby

	$ cd /u01/oracle/diag/rdbms/orcl12/orcl12/trace

Удаляю содержимое alert лога

	$ cat /dev/null > alert_orcl12.log


### НА Primary

	SQL> alter system switch logfile;

### НА Secondary


	SQL> select status from v$instance;

	STATUS
	------------------------------------
	MOUNTED

	SQL> alter database open;


	$ tail -f /u01/oracle/diag/rdbms/orcl12/orcl12/trace/alert_orcl12.log



### НА Primary


	SQL> create user user1 identified by pass1;
	SQL> alter system switch logfile;


### НА Secondary

	$ tail -f /u01/oracle/diag/rdbms/orcl12/orcl12/trace/alert_orcl.log
