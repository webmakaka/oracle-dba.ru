---
layout: page
title: Создание инкрементальной копии базы данных с помощью RMAN
permalink: /database/backup-and-restore/rman/incremental-backup/
---

# Создание инкрементальной копии базы данных с помощью RMAN:


    RUN {
    CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;
    BACKUP INCREMENTAL LEVEL 0 DATABASE PLUS ARCHIVELOG TAG "LEVEL 0";
    BACKUP CURRENT CONTROLFILE SPFILE;
    }

<br/>

    BACKUP INCREMENTAL LEVEL 1 DATABASE PLUS ARCHIVELOG TAG "LEVEL 1";


Создать кумулятивный (включает в себя измениния отраженные в инкрементальных бекапах ) бекап с уровнем 1

    RMAN> backup incremental level 1 cumulative database;




// Сброс базы данных до инкарнации 3

    RMAN> reset database to incarnation 3;
