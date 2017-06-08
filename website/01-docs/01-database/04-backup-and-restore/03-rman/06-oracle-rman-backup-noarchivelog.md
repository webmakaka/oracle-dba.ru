---
layout: page
title: Создание резервных копий с помощью утилиты RMAN (NOARCHIVELOG)
permalink: /database/backup-and-restore/rman/oracle-rman-backup-noarchivelog/
---

# Создание резервных копий с помощью утилиты RMAN (NOARCHIVELOG)

<br/>

    $ rman target /

<br/>

    RMAN> shutdown immediate;  
    RMAN> startup mount;

<br/>

    RMAN> BACKUP DATABASE TAG "FULL_DATABASE_DATAFILES";
    RMAN> BACKUP CURRENT CONTROLFILE TAG "FULL_DATABASE_CONTROLFILE";
    RMAN> BACKUP SPFILE TAG "FULL_DATABASE_SPFILE";

<br/>

    RMAN> DELETE NOPROMPT OBSOLETE;

<br/>

    RMAN> ALTER DATABASE OPEN;

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

<br/>

# Понадобилось восстановить базу из холодного бекапа. Не ту, что описывалась выше. И да, на тестовом окружении.


    $ rman target /
    RMAN> shutdown immediate;
    RMAN> startup mount
    RMAN> restore database;

<br/>

    RMAN> alter database open;

    RMAN-00571: ===========================================================
    RMAN-00569: =============== ERROR MESSAGE STACK FOLLOWS ===============
    RMAN-00571: ===========================================================
    RMAN-03002: failure of sql statement command at 09/20/2015 08:55:12
    ORA-01113: file 1 needs media recovery
    ORA-01110: data file 1: '/u02/oracle/oradata/12.1/orcl12/DATAFILE/data/system01.dbf'


<br/>

И тут я приуныл.  
Вот как так, какой нах recovery если бекап то холодный.

<br/>

Проблема решилась следующим способом.


    RMAN> list backup;


    List of Backup Sets
    ===================


    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    1       Full    700.53M    DISK        00:00:43     15/09/2015 22:34:18
            BP Key: 1   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_DATAFILES
            Piece Name: /u03/oracle/oradata/12.1/orcl12/backups/ORCL12/backupset/2015_09_15/o1_mf_nnndf_FULL_DATABASE_DATAFI_bzko7zd1_.bkp
      List of Datafiles in backup set 1
      File LV Type Ckp SCN    Ckp Time            Name
      ---- -- ---- ---------- ------------------- ----
      1       Full 350780     15/09/2015 22:32:19 /u02/oracle/oradata/12.1/orcl12/DATAFILE/data/system01.dbf
      2       Full 350780     15/09/2015 22:32:19 /u02/oracle/oradata/12.1/orcl12/DATAFILE/data/sysaux01.dbf
      3       Full 350780     15/09/2015 22:32:19 /u02/oracle/oradata/12.1/orcl12/undotbs01.dbf
      4       Full 350780     15/09/2015 22:32:19 /u02/oracle/oradata/12.1/orcl12/DATAFILE/undo/undotbs01.dbf

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    2       Full    9.64M      DISK        00:00:02     15/09/2015 22:34:22
            BP Key: 2   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_DATAFILES
            Piece Name: /u03/oracle/oradata/12.1/orcl12/backups/ORCL12/backupset/2015_09_15/o1_mf_ncsnf_FULL_DATABASE_DATAFI_bzko9g0f_.bkp
      SPFILE Included: Modification time: 15/09/2015 22:33:11
      SPFILE db_unique_name: ORCL12
      Control File Included: Ckp SCN: 350780       Ckp time: 15/09/2015 22:32:19

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    3       Full    9.61M      DISK        00:00:01     15/09/2015 22:34:36
            BP Key: 3   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_CONTROLFILE
            Piece Name: /u03/oracle/oradata/12.1/orcl12/backups/ORCL12/backupset/2015_09_15/o1_mf_ncnnf_FULL_DATABASE_CONTRO_bzko9wwl_.bkp
      Control File Included: Ckp SCN: 350780       Ckp time: 15/09/2015 22:32:19

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    4       Full    80.00K     DISK        00:00:00     15/09/2015 22:34:43
            BP Key: 4   Status: AVAILABLE  Compressed: NO  Tag: FULL_DATABASE_SPFILE
            Piece Name: /u03/oracle/oradata/12.1/orcl12/backups/ORCL12/backupset/2015_09_15/o1_mf_nnsnf_FULL_DATABASE_SPFILE_bzkob3rw_.bkp
      SPFILE Included: Modification time: 15/09/2015 22:33:11
      SPFILE db_unique_name: ORCL12

<br/>

    RMAN> shutdown immediate;

    RMAN> startup nomount;


Не знаю, может быть даже можно было просто восстановить, без явного указания ссылки где брать controlfile.

    RMAN> restore controlfile from '/u03/oracle/oradata/12.1/orcl12/backups/ORCL12/backupset/2015_09_15/o1_mf_ncnnf_FULL_DATABASE_CONTRO_bzko9wwl_.bkp';

<br/>

    RMAN> startup mount;

<br/>

    RMAN> alter database open resetlogs;

<br/>

    RMAN>  select status from v$instance;

    STATUS
    ------------
    OPEN
