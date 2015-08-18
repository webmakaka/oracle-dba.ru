---
layout: page
title: RMAN Catalog (Хранение бекапов базы в другой базе)
permalink: /docs/oracle-database/backup-and-restore/rman/catalog/
---


<br/>


1) Устанавливаю 2 сервера как <a href="/docs/oracle-database/installation/oracle-database-installation/single/asm/linux/6.7/oracle/12.1/">здесь</a>


    Типичный сервер баз данных oracle:  
    Hostname: moscow
    IP: 192.168.1.11  
    Instance Name: orcl12


<br/>

    Сервер хранения бекапов:  
    Hostname: piter  
    IP: 192.168.1.12  
    Instance Name: catalog



<br/>

### На moscow перевожу базу в режим работы ARCHIVELOG:

    SQL> shutdown immediate;
    SQL> startup mount;
    SQL> alter database archivelog;
    SQL> alter database open;

<br/>

### На piter создаю репозиторий для бекапов:

    $ sqlplus / as sysdba

<br/>

    SQL> CREATE TABLESPACE tools
    DATAFILE '+DATA' size 200M autoextend off
    EXTENT MANAGEMENT local
    SEGMENT SPACE MANAGEMENT auto;

<br/>

    SQL> CREATE USER rman IDENTIFIED BY rman123
    TEMPORARY TABLESPACE temp
    DEFAULT TABLESPACE tools
    QUOTA UNLIMITED on tools;

<br/>

    SQL> GRANT CONNECT, RESOURCE, RECOVERY_CATALOG_OWNER TO RMAN;


<br/>

    SQL> exit

<br/>

    $ rman catalog rman/rman123;

<br/>

    RMAN> create catalog;

 <br/>

    RMAN> exit;


<br/>

    $ sqlplus rman/rman123

<br/>

    SQL> select * from cat;

<br/>

    SQL> select * from rc_database;


<br/>

### Настройка tnsnames.ora на обоих серверах


	$ cd $ORACLE_HOME/network/admin

<br/>

	$ vi tnsnames.ora

<br/>

	***

    RMAN12 =
      (DESCRIPTION =
        (ADDRESS = (PROTOCOL = TCP)(HOST = piter.localdomain)(PORT = 1521))
        (CONNECT_DATA =
          (SERVER = DEDICATED)
          (SERVICE_NAME = catalog)
        )
      )

  <br/>

  ### Регистрация в каталоге


// Проверка подключения

    $ sqlplus system/manager@rman12
    $ sqlplus rman/rman123@rman12


    $ rman catalog rman/rman123@rman12 target /
    RMAN> register database;


/// Удалить регистрацию можно следующим образом

    RUN {
        SET DBID 3487575625;
        UNREGISTER DATABASE ORCL12 NOPROMPT;

    }

<br/>

### на piter

    $ sqlplus rman/rman123

<br/>


    SQL> select * from rc_database;

        DB_KEY  DBINC_KEY	    DBID NAME	  RESETLOGS_CHANGE# RESETLOGS_TIME
    ---------- ---------- ---------- -------- ----------------- -------------------
    FINAL_CHANGE#
    -------------
    	 1	    2 3487575625 ORCL12 	    1594143 16/08/2015 21:29:45




 <br/>

 Можно сделать экспорт схемы на сервере с каталогом, т.е. схемы со всеми бекапами.

 ### на piter

 $ expdb system/manager DIRECTORY=DATA_PUMP_DIR SCHEMAS=RMAN DUMPFILE=rman_dump.dmp LOGFILE=rman_log.log


 ### на moscow

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
    1    790      SYSTEM               YES     +DATA/ORCL12/DATAFILE/system.258.887923593
    3    700      SYSAUX               NO      +DATA/ORCL12/DATAFILE/sysaux.257.887923497
    4    135      UNDOTBS1             YES     +DATA/ORCL12/DATAFILE/undotbs1.260.887923711
    6    5        USERS                NO      +DATA/ORCL12/DATAFILE/users.259.887923707

    List of Temporary Files
    =======================
    File Size(MB) Tablespace           Maxsize(MB) Tempfile Name
    ---- -------- -------------------- ----------- --------------------
    1    197      TEMP                 32767       +DATA/ORCL12/TEMPFILE/temp.265.887923853


<br/>

<!--

    SQL> show parameter CONTROL_FILE_RECORD_KEEP_TIME;

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    control_file_record_keep_time	     integer	 7


<br/>

    RMAN> resync catalog;

-->

<br/>

### Поменять db_unique_name в RMAN каталоге (нужно, если поменялось db_unique_name инстанса)

Сначала нужно поменять уникальное имя инстанса базы.

    SQL> show parameter db_unique_name

<br/>

    $ rman target / catalog rman/rman123@rman12


</br>

    RMAN> LIST DB_UNIQUE_NAME OF DATABASE;


    List of Databases
    DB Key  DB Name  DB ID            Database Role    Db_unique_name
    ------- ------- ----------------- ---------------  ------------------
    1       ORCL12   3487575625       PRIMARY          ORCL12


// Если нужно поменять уникальное имя базы данных в rman каталоге.

    RMAN> CHANGE DB_UNIQUE_NAME FROM ORCL12 TO ORCL12C
