---
layout: page
title: Создание копии базы данных Oracle из бекапа с помощью RMAN на том же сервере
description: Создание копии базы данных Oracle из бекапа с помощью RMAN на том же сервере
keywords: Oracle Database, RMAN, Создание копии
permalink: /database/backup-and-restore/rman/duplicate-database/
---

# Создание копии базы данных Oracle из бекапа с помощью RMAN на том же сервере

<br/>

### Имеется 1 сервер Oracle 12c, установленный как <a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">здесь</a>

<br/>

### Создаю password file для нового instance COPY12

    $ cd $ORACLE_HOME/dbs/
    $ cp orapworcl12 orapwcopy12

<br/>

### Прописываю параметры подключения к создаваемому instance COPY12

    $ cd /u01/oracle/database/12.1/network/admin/

<br/>

    $ vi tnsnames.ora

<br/>

```
COPY12 =
    (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = moscow.localdomain)(PORT = 1521))
    (CONNECT_DATA =
        (SERVER = DEDICATED)
        (SERVICE_NAME = copy12)
    )
    )
```

<br/>

### Стартую instance COPY12 в режиме nomount

    $ export ORACLE_SID=COPY12

<br/>

    $ cd /u01/oracle/database/12.1/dbs/

<br/>

    $ vi init${ORACLE_SID}.ora

    db_name=copy12
    COMPATIBLE=12.1.0.2.0

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> startup nomount pfile=$ORACLE_HOME/dbs/init${ORACLE_SID}.ora

<br/>

    SQL> select status from v$instance;

    STATUS
    ------------------------------------
    STARTED

<br/>

    $ ps -ef | grep copy12
    oracle12 25954     1  0 09:31 ?        00:00:00 ora_pmon_copy12
    oracle12 25956     1  0 09:31 ?        00:00:00 ora_psp0_copy12
    oracle12 25958     1  3 09:31 ?        00:00:01 ora_vktm_copy12
    oracle12 25962     1  0 09:31 ?        00:00:00 ora_gen0_copy12
    oracle12 25964     1  0 09:31 ?        00:00:00 ora_mman_copy12
    oracle12 25968     1  0 09:31 ?        00:00:00 ora_diag_copy12
    oracle12 25970     1  0 09:31 ?        00:00:00 ora_dbrm_copy12
    oracle12 25972     1  0 09:31 ?        00:00:00 ora_vkrm_copy12
    oracle12 25974     1  0 09:31 ?        00:00:00 ora_dia0_copy12
    oracle12 25976     1  0 09:31 ?        00:00:00 ora_dbw0_copy12
    oracle12 25978     1  0 09:31 ?        00:00:00 ora_lgwr_copy12
    oracle12 25980     1  0 09:31 ?        00:00:00 ora_ckpt_copy12
    oracle12 25982     1  0 09:31 ?        00:00:00 ora_smon_copy12
    oracle12 25984     1  0 09:31 ?        00:00:00 ora_reco_copy12
    oracle12 25986     1  0 09:31 ?        00:00:00 ora_lreg_copy12
    oracle12 25988     1  0 09:31 ?        00:00:00 ora_pxmn_copy12
    oracle12 25990     1  0 09:31 ?        00:00:00 ora_mmon_copy12
    oracle12 25992     1  0 09:31 ?        00:00:00 ora_mmnl_copy12
    oracle12 26005 15234  0 09:31 pts/0    00:00:00 grep copy12

<br/>

### Настройка Listener для создания нового сервиса COPY12

<!--
	$ cd $ORACLE_HOME/network/admin

-->

    $ cd $GRID_HOME/network/admin

<br/>

    $ cp listener.ora listener.ora.bkp

<br/>

    $ vi listener.ora

<br/>

    LISTENER =
    (ADDRESS_LIST=
    		(ADDRESS=(PROTOCOL=tcp)(HOST=moscow.localdomain)(PORT=1521))
    		(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))

    SID_LIST_LISTENER=
    			(SID_LIST=
    					(SID_DESC=
        					(GLOBAL_DBNAME=ORCL12)
        					(ORACLE_HOME=/u01/oracle/database/12.1)
        					(SID_NAME=orcl12)
    					)
                        (SID_DESC=
                            (GLOBAL_DBNAME=COPY12)
                            (ORACLE_HOME=/u01/oracle/database/12.1)
                            (SID_NAME=copy12)
                        )
    			)

    ENABLE_GLOBAL_DYNAMIC_ENDPOINT_LISTENER=ON
    VALID_NODE_CHECKING_REGISTRATION_LISTENER=SUBNET

<br/>

    $ lsnrctl reload;

<br/>

    $ lsnrctl services

    ***

    Service "COPY12" has 2 instance(s).
      Instance "copy12", status UNKNOWN, has 1 handler(s) for this service...
        Handler(s):
          "DEDICATED" established:0 refused:0
             LOCAL SERVER
      Instance "copy12", status BLOCKED, has 1 handler(s) for this service...
        Handler(s):
          "DEDICATED" established:0 refused:0 state:ready
             LOCAL SERVER
    Service "ORCL12" has 2 instance(s).
      Instance "orcl12", status UNKNOWN, has 1 handler(s) for this service...
        Handler(s):
          "DEDICATED" established:0 refused:0
             LOCAL SERVER
      Instance "orcl12", status READY, has 1 handler(s) for this service...
        Handler(s):
          "DEDICATED" established:0 refused:0 state:ready
             LOCAL SERVER
    ***

<br/>

    $ lsnrctl status;

    ***

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                17-AUG-2015 06:02:18
    Uptime                    3 days 3 hr. 45 min. 59 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Parameter File   /u01/oracle/grid/12.1/network/admin/listener.ora
    Listener Log File         /u01/oracle/diag/tnslsnr/moscow/listener/alert/log.xml
    Listening Endpoints Summary...
      (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=moscow.localdomain)(PORT=1521)))
      (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1521)))
      (DESCRIPTION=(ADDRESS=(PROTOCOL=tcps)(HOST=moscow.localdomain)(PORT=5500))(Security=(my_wallet_directory=/u01/oracle/admin/orcl12/xdb_wallet))(Presentation=HTTP)(Session=RAW))
    Services Summary...
    Service "+ASM" has 1 instance(s).
      Instance "+ASM", status READY, has 1 handler(s) for this service...
    Service "COPY12" has 2 instance(s).
      Instance "copy12", status UNKNOWN, has 1 handler(s) for this service...
      Instance "copy12", status BLOCKED, has 1 handler(s) for this service...
    Service "ORCL12" has 2 instance(s).
      Instance "orcl12", status UNKNOWN, has 1 handler(s) for this service...
      Instance "orcl12", status READY, has 1 handler(s) for this service...
    Service "orcl12XDB" has 1 instance(s).
      Instance "orcl12", status READY, has 1 handler(s) for this service...
    The command completed successfully

<br/>

### Подготовка RMAN скрипта для создания копии сервера

<br/>

```
$ export ORACLE_SID=orcl12
```

<br/>

```
$ echo $ORACLE_SID
orcl12
```

Значения размера файлов журналов, которые нужно будет указать в скрипте.

    SQL> select max (bytes), count (1) from v$log;

    MAX(BYTES)   COUNT(1)
    ---------- ----------
     52428800	    3

<br/>

    $ rman target /

Если используется Oracle Catalog

    $ rman target / catalog rman/rman123@rman12

<br/>

    RMAN> report schema;

    starting full resync of recovery catalog
    full resync complete
    Report of database schema for database with db_unique_name ORCL12

    List of Permanent Datafiles
    ===========================
    File Size(MB) Tablespace           RB segs Datafile Name
    ---- -------- -------------------- ------- ------------------------
    1    810      SYSTEM               YES     +DATA/ORCL12/DATAFILE/system.258.887923593
    3    780      SYSAUX               NO      +DATA/ORCL12/DATAFILE/sysaux.257.887923497
    4    135      UNDOTBS1             YES     +DATA/ORCL12/DATAFILE/undotbs1.260.887923711
    6    5        USERS                NO      +DATA/ORCL12/DATAFILE/users.259.887923707

    List of Temporary Files
    =======================
    File Size(MB) Tablespace           Maxsize(MB) Tempfile Name
    ---- -------- -------------------- ----------- --------------------
    1    197      TEMP                 32767       +DATA/ORCL12/TEMPFILE/temp.265.887923853

<br/>

    set lin 180
    col MEMBER for a60
    col status for a8

    select a.GROUP#, a.THREAD#, a.BYTES/1024/1024 as MB, a.status, b.member
    from v$log a, v$logfile b
    where a.GROUP#=b.GROUP#;

<br/>

    GROUP#    THREAD#	      MB STATUS   MEMBER
    ---------- ---------- ---------- -------- ------------------------------------------------------------
     3	    1	      50 CURRENT  +DATA/ORCL12/ONLINELOG/group_3.264.888049601
     3	    1	      50 CURRENT  +ARCH/ORCL12/ONLINELOG/group_3.259.888049605
     2	    1	      50 INACTIVE +DATA/ORCL12/ONLINELOG/group_2.263.888049597
     2	    1	      50 INACTIVE +ARCH/ORCL12/ONLINELOG/group_2.258.888049599
     1	    1	      50 INACTIVE +DATA/ORCL12/ONLINELOG/group_1.262.888049593
     1	    1	      50 INACTIVE +ARCH/ORCL12/ONLINELOG/group_1.257.888049595

<br/>

**Создание каталогов в ASM**

    $ cd ~/ . asm.sh

    $ asmcmd

    $ cd DATA

    ASMCMD> mkdir COPY12
    ASMCMD> cd COPY12
    ASMCMD> mkdir DATAFILE
    ASMCMD> mkdir TEMPFILE
    ASMCMD> mkdir ONLINELOG
    ASMCMD> cd ../../

    ASMCMD> cd ARCH
    ASMCMD> mkdir COPY12
    ASMCMD> cd COPY12
    ASMCMD> mkdir ONLINELOG
    ASMCMD> mkdir ARCHIVELOG

    ASMCMD> exit

<br/>

    $ source ~/.bash_profile

<br/>

    $ cd $ORACLE_HOME/scripts

<br/>

    $ vi duplicate-rman-script.rman

Данные задаются в соответствии запроса report shema;
Идентификатор файлов данных (1,3,4....) см. в report shema;

    RUN {
        set NEWNAME for DATAFILE 1 to '+DATA/COPY12/DATAFILE/system.258.887923593';
        set NEWNAME for DATAFILE 3 to '+DATA/COPY12/DATAFILE/sysaux.257.887923497';
        set NEWNAME for DATAFILE 4 to '+DATA/COPY12/DATAFILE/undotbs1.260.887923711';
        set NEWNAME for DATAFILE 6 to '+DATA/COPY12/DATAFILE/users.259.887923707';
        set NEWNAME for TEMPFILE 1 to '+DATA/COPY12/TEMPFILE/temp.265.887923853';

        DUPLICATE TARGET DATABASE TO COPY12
        # SKIP TABLESPACE DATA
        LOGFILE
    GROUP 1 ('+ARCH/COPY12/ONLINELOG/group_1.257.888049595', '+DATA/COPY12/ONLINELOG/group_1.262.888049593') SIZE 52428800 REUSE,

    GROUP 2 ('+ARCH/COPY12/ONLINELOG/group_2.258.888049599', '+DATA/COPY12/ONLINELOG/group_2.263.888049597') SIZE 52428800 REUSE,

    GROUP 3 ('+ARCH/COPY12/ONLINELOG/group_3.259.888049605', '+DATA/COPY12/ONLINELOG/group_3.264.888049601') SIZE 52428800 REUSE;

    }

Проверка синтаксиса созданного файла сценария

    $ rman CHECKSYNTAX @duplicate-rman-script.rman

Выполнение скрипта резервного копирования

    $ rman target sys/manager@orcl12 auxiliary sys/manager@copy12 @duplicate-rman-script.rman

Если используется Oracle Catalog, команда может выглядеть следующим образом

    $ rman catalog rman/rman123@rman12

    $ connect target sys/manager
    $ connect auxiliary sys/manager@copy12

    $ @duplicate-rman-script.rman

Завершилось без ошибок (с 3-го раза).

<br/>

### Проверяем результаты копирования

    $ export ORACLE_SID=COPY12

<br/>

    SQL> select instance_name from v$instance;

    INSTANCE_NAME
    ----------------
    copy12

<br/>

    SQL> select status from v$instance;

    STATUS
    ------------
    OPEN
