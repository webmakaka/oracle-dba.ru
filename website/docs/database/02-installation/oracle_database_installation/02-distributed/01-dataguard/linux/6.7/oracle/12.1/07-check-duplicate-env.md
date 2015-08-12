---
layout: page
title:  Проверяем, что файловая система схожа на 2-х серверах
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/check-duplicate-env/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Проверяем, что файловая система схожа на 2-х серверах

Смысл шага в том, что если, например указан каталог в который нужно скопировать файлы, а на сервере такого каталога нет, процедура копирования завалится.

Может, например завалиться из-за отсутствия каталога /u01/oracle/admin/orcl/adump


### На Primary

	SQL> show parameter audit

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	audit_file_dest 		     string	 /u01/oracle/admin/orcl/adump
	audit_sys_operations		     boolean	 TRUE
	audit_syslog_level		     string
	audit_trail			     string	 DB
	unified_audit_sga_queue_size	     integer	 1048576


<br/>

### На Standby


	$ mkdir -p /u01/oracle/admin/orcl/adump
