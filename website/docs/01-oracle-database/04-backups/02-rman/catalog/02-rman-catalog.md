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


### На piter создаю репозиторий:

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



### Настройка tnsnames.ora на piter


	$ cd $ORACLE_HOME/network/admin

<br/>

	$ vi tnsnames.ora

<br/>

	***

	RMAN12G =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = moscow.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = catalog)
	    )
	  )

<br/>

    $ lsnrclt restart


Продолжение следует...
