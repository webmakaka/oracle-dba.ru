---
layout: page
title: Утилита RMAN (Recovery Manager)
permalink: /database/backup-and-restore/rman/about-oracle-rman/
---


## Утилита RMAN (Recovery Manager)

<br/>

<strong>RMAN</strong> - (утилита для резервного копирования и восстановление данных).

Команда <strong>Restore </strong> выполняет восстановление файлов из бекапа. Данные восстанавливаются на момент создания бекапа.

Команда <strong>Recover </strong>- примененяет к восстановленной из бекапа базе данных сохраненные архивные журналы,
чтобы база данных была актуальна на какой-то более приемлемый момент времени, нежели чем на момент создания бекапа. Если архивных журналов нет, то и применять нечего.


<br/>

// Подключиться к консоли rman

    $rman target /

// Подключиться к консоли с параметрами

    $ rman target sys/manager@service


// Писать output в файл

    $ rman target / Log /tmp/rman.log


// Писать output в консоль и в лог

    $ rman target / | tee /tmp/rman.log


// Показывает с какими файлами данных можно выполнять резервные копии. Т.е. того инстанса к которому подключились.

<br/>

    RMAN> report schema;

<br/>

    Report of database schema for database with db_unique_name ORA112

    List of Permanent Datafiles
    ===========================
    File Size(MB) Tablespace           RB segs Datafile Name
    ---- -------- -------------------- ------- ------------------------
    1    780      SYSTEM               ***     /u02/oradata/ora112/system01.dbf
    2    850      SYSAUX               ***     /u02/oradata/ora112/sysaux01.dbf
    3    75       UNDOTBS1             ***     /u02/oradata/ora112/undotbs01.dbf
    4    5        USERS                ***     /u02/oradata/ora112/users01.dbf
    5    2048     MY_INDEXES           ***     /u02/oradata/ora112/my_indexes01.dbf
    6    2048     MY_DATA              ***     /u02/oradata/ora112/my_data01.dbf
    7    2048     MY_DATA              ***     /u01/app/oracle/product/11.2/dbs/my_data02.dbf
    8    1024     MY_DATA              ***     /u01/app/oracle/product/11.2/dbs/my_data03.dbf
    9    1024     MY_DATA2             ***     /u01/app/oracle/product/11.2/dbs/my_data04.dbf
    10   1024     MY_DATA              ***     /u01/app/oracle/product/11.2/dbs/my_data05.dbf
    11   1024     MY_DATA              ***     /u01/app/oracle/product/11.2/dbs/my_data06.dbf
    12   1024     MY_DATA              ***     /u01/app/oracle/product/11.2/dbs/my_data07.dbf
    13   1024     MY_DATA              ***     /u01/app/oracle/product/11.2/dbs/my_data08.dbf
    14   10       MY_DATA              ***     /u02/oradata/ORA112/datafile/o1_mf_my_data_7oy0k0vr_.dbf

    List of Temporary Files
    =======================
    File Size(MB) Tablespace           Maxsize(MB) Tempfile Name
    ---- -------- -------------------- ----------- --------------------
    1    537      TEMP                 32767       /u02/oradata/ora112/temp01.dbf
    2    2048     MY_TEMP              2048        /u02/oradata/ora112/my_temp01.dbf





// Посмотреть значения параметров бекапа, установленных по умолчанию.

    RMAN> show all;

<br/>

    RMAN configuration parameters for database with db_unique_name MASTER are:
    CONFIGURE RETENTION POLICY TO REDUNDANCY 1; # default
    CONFIGURE BACKUP OPTIMIZATION ON;
    CONFIGURE DEFAULT DEVICE TYPE TO DISK; # default
    CONFIGURE CONTROLFILE AUTOBACKUP OFF; # default
    CONFIGURE CONTROLFILE AUTOBACKUP FORMAT FOR DEVICE TYPE DISK TO '%F'; # default
    CONFIGURE DEVICE TYPE DISK PARALLELISM 1 BACKUP TYPE TO BACKUPSET; # default
    CONFIGURE DATAFILE BACKUP COPIES FOR DEVICE TYPE DISK TO 1; # default
    CONFIGURE ARCHIVELOG BACKUP COPIES FOR DEVICE TYPE DISK TO 1; # default
    CONFIGURE CHANNEL DEVICE TYPE DISK FORMAT   '+ARCH/%d_DB_%u_%s_%p';
    CONFIGURE MAXSETSIZE TO UNLIMITED; # default
    CONFIGURE ENCRYPTION FOR DATABASE OFF; # default
    CONFIGURE ENCRYPTION ALGORITHM 'AES128'; # default
    CONFIGURE COMPRESSION ALGORITHM 'BASIC' AS OF RELEASE 'DEFAULT' OPTIMIZE FOR LOAD TRUE ; # default
    CONFIGURE RMAN OUTPUT TO KEEP FOR 7 DAYS; # default
    CONFIGURE ARCHIVELOG DELETION POLICY TO NONE;
    CONFIGURE SNAPSHOT CONTROLFILE NAME TO '/u01/oracle/database/12.1/dbs/snapcf_orcl12.f'; # default


<br/>

// Задать значение (просто пример)

    RMAN> CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 2 DAYS;

<br/>

    RMAN> show all;

    RMAN configuration parameters for database with db_unique_name MASTER are:
    CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 2 DAYS;
    ***

<br/>


// Сбросить

    RMAN> CONFIGURE RETENTION POLICY CLEAR;


Но все это, как мне видится не особо и нужно.
Параметры бекапа следует явно задавать в скриптах.


### В 11 версии работа еще больше упростилась.

    RMAN> list failure;
    RMAN> advise failure;
    RMAN> repair failure;
