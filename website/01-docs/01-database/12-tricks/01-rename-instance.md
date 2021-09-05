---
layout: page
title: Переименование instance Oracle 11 в linux
description: Переименование instance Oracle 11 в linux
keywords: Oracle Database, Переименование instance
permalink: /database/tricks/rename-oracle-instance/
---

# Переименование instance Oracle 11 в linux

**Переименую базу в primary (исключительно для удобства) на сервере**

1.  $ rman target /
    RMAN> backup full database noexclude include current controlfile spfile;
    RMAN> quit;

2.  $ sqlplus / as sysdba
    SQL> shutdown immediate;
    SQL> startup mount;

<br/>

    SQL> create pfile='/u01/app/oracle/product/11.2/dbs/initprimary.ora' from spfile;

    SQL> quit

<br/>

    $ nid TARGET=sys/master dbname=primary SETNAME=Y logfile=/u01/oradata/nid.log

<br/>

    $ cat /u01/oradata/nid.log

<br/>

    DBNEWID: Release 11.2.0.2.0 - Production on Fri May 6 20:54:10 2011

    Copyright (c) 1982, 2009, Oracle and/or its affiliates.  All rights reserved.

    Connected to database ORA112 (DBID=272513945)

    Connected to server version 11.2.0

    Control Files in database:
        /u02/oradata/ora112/control01.ctl
        /u03/oradata/ora112/control01.ctl

    Changing database name from ORA112 to PRIMARY
        Control File /u02/oradata/ora112/control01.ctl - modified
        Control File /u03/oradata/ora112/control01.ctl - modified
        Datafile /u02/oradata/ora112/system01.db - wrote new name
        Datafile /u02/oradata/ora112/sysaux01.db - wrote new name
        Datafile /u02/oradata/ora112/undotbs01.db - wrote new name
        Datafile /u02/oradata/ora112/users01.db - wrote new name
        Datafile /u02/oradata/ora112/temp01.db - wrote new name
        Control File /u02/oradata/ora112/control01.ctl - wrote new name
        Control File /u03/oradata/ora112/control01.ctl - wrote new name
        Instance shut down

    Database name changed to PRIMARY.
    Modify parameter file and generate a new password file before restarting.
    Succesfully changed database name.
    DBNEWID - Completed succesfully.
    [oracle11@oracle11 ~]$ cd /u01/app/oracle/product/11.2/dbs/
    [oracle11@oracle11 dbs]$ orapwd file=orapwprimary password=master entries=1

<br/>

    vi /u01/app/oracle/product/11.2/dbs/initprimary.ora

<br/>

    *.db_name='primary'

<br/>

    $ vi ~/.bash_profile

    ORACLE_SID=primary
    ORACLE_UNQNAME=primary

<br/>

    $ source ~/.bash_profile

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> startup


    SQL> create spfile from pfile='/u01/app/oracle/product/11.2/dbs/initprimary.ora';


    SQL> select name from v$database;

    NAME
    ---------
    PRIMARY


    SQL> shutdown immediate;
    SQL> startup;

Необходимо, чтобы сервер был стартован из spfile

    SELECT DECODE(value, NULL, 'PFILE', 'SPFILE') "Init File Type"
    FROM sys.v_$parameter WHERE name = 'spfile';


    Init F
    ------
    SPFILE

<br/>

    # vi /etc/oratab
    primary:/u01/app/oracle/product/11.2:Y
