---
layout: page
title: Стартую instance на standby
description: Стартую instance на standby
keywords: Oracle DataBase 12.1, Centos 6.7, DataGuard
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/startup-instance-on-standby/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Стартую instance на standby

### Standby

    $ cd $ORACLE_HOME/dbs

Создаю pfile с единственным описанием - имя базы данных

    $ echo DB_NAME=${ORACLE_SID} > init${ORACLE_SID}.ora

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> startup nomount pfile=$ORACLE_HOME/dbs/init${ORACLE_SID}.ora

<br/>

    SQL> select status from v$instance;

    STATUS
    ------------------------------------
    STARTED
