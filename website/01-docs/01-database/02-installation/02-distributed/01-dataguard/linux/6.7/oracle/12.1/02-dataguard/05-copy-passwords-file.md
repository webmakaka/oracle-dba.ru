---
layout: page
title: Копирование файла паролей с primary на standby
description: Копирование файла паролей с primary на standby
keywords: Oracle DataBase 12.1, Centos 6.7, DataGuard
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/copy-passwords-file/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Копирование файла паролей с primary на standby

### На Primary

**Passwordfile**

    SQL> show parameter remote_login_passwordfile

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    remote_login_passwordfile	     string	 EXCLUSIVE

<br/>

    SQL> select * from v$pwfile_users;

    USERNAME		       SYSDB SYSOP SYSAS SYSBA SYSDG SYSKM     CON_ID
    ------------------------------ ----- ----- ----- ----- ----- ----- ----------
    SYS			       TRUE  TRUE  FALSE FALSE FALSE FALSE	    0
    SYSDG			       FALSE FALSE FALSE FALSE TRUE  FALSE	    0
    SYSBACKUP		       FALSE FALSE FALSE TRUE  FALSE FALSE	    0
    SYSKM			       FALSE FALSE FALSE FALSE FALSE TRUE	    0

<br/>

    $ chmod 4640 $ORACLE_HOME/dbs/orapw${ORACLE_SID}

<br/>

// Файл паролей можно создать следующей командой. Entries - ограничить максимальное количество подключений к базе (если ничего не путаю). Я не создавал новый файл паролей.

    $ orapwd fiel=$ORACLE_HOME/dbs/orapw${ORACLE_SID} password=oracle12 entries=5

Копирую файл паролей

    $ scp $ORACLE_HOME/dbs/orapw${ORACLE_SID} oracle12@piter:$ORACLE_HOME/dbs/

<br/>

### Standby

    $ chmod 4640 $ORACLE_HOME/dbs/orapw${ORACLE_SID}
