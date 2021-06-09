---
layout: page
title: Создание каталогов на standby, котырые есть на primary
description: Создание каталогов на standby, котырые есть на primary
keywords: Oracle DataBase 12.1, Centos 6.7, DataGuard
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/create-foder-structure-like-on-primary/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание каталогов на standby, котырые есть на primary

Смысл шага в том, что если, например указан каталог в который нужно скопировать файлы, а на сервере такого каталога нет, процедура копирования сломается.

У меня пока валился только из-за отсутствия каталога /u01/oracle/admin/orcl12/adump

### На Primary

    SQL> show parameter audit

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    audit_file_dest 		     string	 /u01/oracle/admin/orcl12/adump
    audit_sys_operations		     boolean	 TRUE
    audit_syslog_level		     string
    audit_trail			     string	 DB
    unified_audit_sga_queue_size	     integer	 1048576

<br/>

### На Standby

    $ mkdir -p /u01/oracle/admin/orcl12/adump
