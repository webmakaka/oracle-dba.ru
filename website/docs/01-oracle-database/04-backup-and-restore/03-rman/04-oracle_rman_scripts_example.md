---
layout: page
title: Скрипт RMAN для создания бекапов
permalink: /docs/oracle-database/backup-and-restore/rman/oracle_rman_scripts_example/
---

### Скрипт RMAN для создания бекапов



    run {
        CONFIGURE CHANNEL DEVICE TYPE DISK FORMAT '/tmp/backups/ORCL12_bkp_%t%s%p';
        CONFIGURE CONTROLFILE AUTOBACKUP FORMAT FOR DEVICE TYPE DISK TO  '/tmp/backups/ORCL12_cf_%F';
        backup database plus archivelog;
    }


%t = 4 bytes time stamp
%s = backup set number
%p = backup piece number



    RUN{
        CONFIGURE CONTROLFILE AUTOBACKUP ON;
        SET COMMAND ID TO 'DUDAS_ONLINE_BACKUPFULL';
        ALLOCATE CHANNEL c1 DEVICE TYPE DISK;
        BACKUP AS COMPRESSED BACKUPSET FULL DATABASE TAG DUDAS_FULL FORMAT '/tmp/backups/ORCL12/bkp_%D_%T_%S_P_FULL';
        SQL 'ALTER SYSTEM ARCHIVE LOG CURRENT';
        BACKUP TAG DUDAS_ARCHIVE FORMAT '/tmp/backups/ORCL12/bkp_%D_%T_%S_%P_ARCHIVELOG' ARCHIVELOG ALL DELETE ALL INPUT;
        BACKUP TAG DUDAS_CONTROL CURRENT CONTROLFILE FORMAT '/tmp/backups/ORCL12/bkp_%D_%T_%S_%P_CONTROL';
        RELEASE CHANNEL C1;
    }
