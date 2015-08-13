---
layout: page
title:  Проверка применения redo
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-redo-apply/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Проверка применения redo



	SQL> show parameter dump

background_dump_dest - расположение alert log файла


### НА Primary и Standby

	$ cd /u01/oracle/diag/rdbms/master/master/trace/



Удаляю содержимое alert лога

	$ cp alert_master.log alert_master.log.bkp
	$ cat /dev/null > alert_master.log




	$ cd /u01/oracle/diag/rdbms/slave/slave/trace
	$ cp alert_slave.log alert_slave.log.bkp
	$ cat /dev/null > alert_slave.log


### НА Primary


	SQL> create user user1 identified by pass1;
	SQL> alter system switch logfile;


	$ tail -f /u01/oracle/diag/rdbms/master/master/trace/alert_master.log


	Thread 1 advanced to log sequence 13 (LGWR switch)
	  Current log# 1 seq# 13 mem# 0: +DATA/ORCL12/ONLINELOG/group_1.262.887538219
	  Current log# 1 seq# 13 mem# 1: +ARCH/ORCL12/ONLINELOG/group_1.257.887538223
	Wed Aug 12 13:34:17 2015
	Archived Log entry 4 added for thread 1 sequence 12 ID 0xcfda0b26 dest 1:

### НА Secondary

	$ tail -f /u01/oracle/diag/rdbms/slave/slave/trace/alert_slave.log


Мда. Ничего не заработало!!!
