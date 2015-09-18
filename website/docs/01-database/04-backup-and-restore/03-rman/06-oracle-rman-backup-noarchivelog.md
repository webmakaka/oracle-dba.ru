---
layout: page
title: Создание резервных копий с помощью утилиты RMAN (NOARCHIVELOG)
permalink: /docs/oracle-database/backup-and-restore/rman/oracle-rman-backup-noarchivelog/
---



### Создание резервных копий с помощью утилиты RMAN (NOARCHIVELOG)

<br/>

    $ rman target /

<br/>

    RMAN> shutdown immediate;  
    RMAN> startup mount;

<br/>

    RMAN> BACKUP DATABASE TAG "FULL_DATABASE_DATAFILES";

<br/>

    RMAN> BACKUP CURRENT CONTROLFILE TAG "FULL_DATABASE_CONTROLFILE";

<br/>

    RMAN> BACKUP SPFILE TAG "FULL_DATABASE_SPFILE";

<br/>

    RMAN> DELETE NOPROMPT OBSOLETE;

<br/>

    RMAN> alter database open;

<br/>
<br/>

    RMAN> list backup;

<br/>

    List of Backup Sets
    ===================


    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ ---------------
    1       Full    1.27G      DISK        00:03:02     22-AUG-15
            BP Key: 1   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_DATAFILES
            Piece Name: +ARCH/ORCL12/BACKUPSET/2015_08_22/nnndf0_full_database_datafiles_0.260.888436705
      List of Datafiles in backup set 1
      File LV Type Ckp SCN    Ckp Time  Name
      ---- -- ---- ---------- --------- ----
      1       Full 1678308    22-AUG-15 +DATA/ORCL12/DATAFILE/system.258.888429421
      3       Full 1678308    22-AUG-15 +DATA/ORCL12/DATAFILE/sysaux.257.888429347
      4       Full 1678308    22-AUG-15 +DATA/ORCL12/DATAFILE/undotbs1.260.888429497
      6       Full 1678308    22-AUG-15 +DATA/ORCL12/DATAFILE/users.259.888429497

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ ---------------
    3       Full    9.61M      DISK        00:00:04     22-AUG-15
            BP Key: 3   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_CONTROLFILE
            Piece Name: +ARCH/ORCL12/BACKUPSET/2015_08_22/ncnnf0_full_database_controlfile_0.262.888436943
      Control File Included: Ckp SCN: 1678308      Ckp time: 22-AUG-15

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ ---------------
    4       Full    80.00K     DISK        00:00:01     22-AUG-15
            BP Key: 4   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_SPFILE
            Piece Name: +ARCH/ORCL12/BACKUPSET/2015_08_22/nnsnf0_full_database_spfile_0.263.888436995
      SPFILE Included: Modification time: 22-AUG-15
      SPFILE db_unique_name: ORCL12
