---
layout: page
title: Создание инкрементальной копии базы данных с помощью RMAN
permalink: /docs/oracle-database/backup-and-restore/rman/incremental-backup/
---

<br/>
<h3>Создание инкрементальной копии базы данных с помощью RMAN:</h3>


    RUN {
    CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;
    BACKUP INCREMENTAL LEVEL 0 TAG "LEVEL 0" DATABASE PLUS ARCHIVELOG;
    BACKUP CURRENT CONTROLFILE SPFILE;
    }

<br/>

    BACKUP INCREMENTAL LEVEL 1 TAG "LEVEL 1" DATABASE PLUS ARCHIVELOG;



Создать кумулятивный (включает в себя измениния отраженные в инкрементальных бекапах ) бекап с уровнем 1

    RMAN> backup incremental level 1 cumulative database;
