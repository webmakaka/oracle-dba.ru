---
layout: page
title: Утилита RMAN (Recovery Manager)
permalink: /docs/architecture/backups/rman/video-course/
---

// Подключиться к консоли rman

    $rman target /

<br/>

    $ rman target sys/manager@service


// Писать output в файл

    $ rman target / Log /tmp/rman.log


// Писать output в консоль и в лог

    $ rman target / | tee /tmp/rman.log


$ export NLS_DATE_FORMAT='dd/mm/yyyy hh24:mi:ss'

// Посмотреть все параметры, установленные пользователем по умолчанию.

    RMAN> show all;

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

// Задать значение

    RMAN> CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 2 DAYS;

<br/>

    RMAN> show all;

    RMAN configuration parameters for database with db_unique_name MASTER are:
    CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 2 DAYS;
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
    CONFIGURE SNAPSHOT CONTROLFILE NAME TO '/u01/oracle/database/12.1/dbs/snapcf_orcl12.f'; # defaul

<br/>


// Сбросить

    RMAN> CONFIGURE RETENTION POLICY CLEAR;


Но все это, как мне видится нахер не нужно.
Нужно все параметры явно задавать в скриптах.
