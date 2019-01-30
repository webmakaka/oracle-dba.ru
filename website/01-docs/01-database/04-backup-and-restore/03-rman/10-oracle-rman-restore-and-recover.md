---
layout: page
title: Восстановление из резервной копий с помощью утилиты RMAN (Recovery Manager)
permalink: /database/backup-and-restore/rman/oracle-rman-restore-and-recover/
---

# Восстановление из резервной копий с помощью утилиты RMAN (Recovery Manager)

<br/>

### Получить информацию об имеющихся бекапах.

    set pagesize 200;

    SELECT start_time, end_time, status
    FROM v$rman_backup_job_details order by 1 desc;

<br/>

### Получить список файлов, необходимых для восстановления из бекапа.

    RMAN> RESTORE DATABASE PREVIEW SUMMARY;

<br/>

    Starting restore at 13.04.2012 18:48:51
    using channel ORA_DISK_1


    List of Backups
    ===============
    Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
    ------- -- -- - ----------- ------------------- ------- ------- ---------- ---
    214     B  F  A DISK        13.04.2012 18:46:40 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    213     B  F  A DISK        13.04.2012 18:45:57 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    210     B  F  A DISK        13.04.2012 18:45:21 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    211     B  F  A DISK        13.04.2012 18:45:23 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    212     B  F  A DISK        13.04.2012 18:45:24 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE

    List of Archived Log Copies for database with db_unique_name ORA112
    =====================================================================

    Key     Thrd Seq     S Low Time
    ------- ---- ------- - -------------------
    295     1    242     A 13.04.2012 18:45:06
            Name: /u02/oradata/ora112/archivelogs/1_242_0767676036.arc

    Media recovery start SCN is 8639788
    Recovery must be done beyond SCN 8639822 to clear datafile fuzziness
    Finished restore at 13.04.2012 18:48:51

<br/><br/>
**Команда:**<br/>

RESTORE DATABASE PREVIEW - представляет детальный отчет обо всех резервных копиях, которые потребуются для успешного выолпнения команды RESTORE.

    RMAN> RESTORE DATABASE PREVIEW;

<br/>

    Starting restore at 13.04.2012 18:51:29
    using channel ORA_DISK_1


    List of Backup Sets
    ===================


    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    214     Full    191.88M    DISK        00:00:40     13.04.2012 18:46:40
            BP Key: 226   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_BEFORE_UPGRADE
            Piece Name: /u03/oracle_backups/fra/ORA112/backupset/2012_04_13/o1_mf_nnndf_FULL_DATABASE_BEFORE_7rjh18jk_.bkp
      List of Datafiles in backup set 214
      File LV Type Ckp SCN    Ckp Time            Name
      ---- -- ---- ---------- ------------------- ----
      1       Full 8639822    13.04.2012 18:46:00 /u02/oradata/ora112/system01.dbf
      9       Full 8639822    13.04.2012 18:46:00 /u01/app/oracle/product/11.2/dbs/my_data04.dbf

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    213     Full    121.24M    DISK        00:00:32     13.04.2012 18:45:57
            BP Key: 225   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_BEFORE_UPGRADE
            Piece Name: /u03/oracle_backups/fra/ORA112/backupset/2012_04_13/o1_mf_nnndf_FULL_DATABASE_BEFORE_7rjh059r_.bkp
      List of Datafiles in backup set 213
      File LV Type Ckp SCN    Ckp Time            Name
      ---- -- ---- ---------- ------------------- ----
      2       Full 8639802    13.04.2012 18:45:25 /u02/oradata/ora112/sysaux01.dbf
      3       Full 8639802    13.04.2012 18:45:25 /u02/oradata/ora112/undotbs01.dbf
      4       Full 8639802    13.04.2012 18:45:25 /u02/oradata/ora112/users01.dbf
      8       Full 8639802    13.04.2012 18:45:25 /u01/app/oracle/product/11.2/dbs/my_data03.dbf
      14      Full 8639802    13.04.2012 18:45:25 /u02/oradata/ORA112/datafile/o1_mf_my_data_7oy0k0vr_.dbf

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    210     Full    1.02M      DISK        00:00:00     13.04.2012 18:45:21
            BP Key: 222   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_BEFORE_UPGRADE
            Piece Name: /u03/oracle_backups/fra/ORA112/backupset/2012_04_13/o1_mf_nnndf_FULL_DATABASE_BEFORE_7rjh01to_.bkp
      List of Datafiles in backup set 210
      File LV Type Ckp SCN    Ckp Time            Name
      ---- -- ---- ---------- ------------------- ----
      5       Full 8639798    13.04.2012 18:45:21 /u02/oradata/ora112/my_indexes01.dbf
      7       Full 8639798    13.04.2012 18:45:21 /u01/app/oracle/product/11.2/dbs/my_data02.dbf

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    211     Full    1.28M      DISK        00:00:01     13.04.2012 18:45:23
            BP Key: 223   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_BEFORE_UPGRADE
            Piece Name: /u03/oracle_backups/fra/ORA112/backupset/2012_04_13/o1_mf_nnndf_FULL_DATABASE_BEFORE_7rjh02yy_.bkp
      List of Datafiles in backup set 211
      File LV Type Ckp SCN    Ckp Time            Name
      ---- -- ---- ---------- ------------------- ----
      6       Full 8639799    13.04.2012 18:45:22 /u02/oradata/ora112/my_data01.dbf
      12      Full 8639799    13.04.2012 18:45:22 /u01/app/oracle/product/11.2/dbs/my_data07.dbf
      13      Full 8639799    13.04.2012 18:45:22 /u01/app/oracle/product/11.2/dbs/my_data08.dbf

    BS Key  Type LV Size       Device Type Elapsed Time Completion Time
    ------- ---- -- ---------- ----------- ------------ -------------------
    212     Full    1.02M      DISK        00:00:00     13.04.2012 18:45:24
            BP Key: 224   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_BEFORE_UPGRADE
            Piece Name: /u03/oracle_backups/fra/ORA112/backupset/2012_04_13/o1_mf_nnndf_FULL_DATABASE_BEFORE_7rjh044h_.bkp
      List of Datafiles in backup set 212
      File LV Type Ckp SCN    Ckp Time            Name
      ---- -- ---- ---------- ------------------- ----
      10      Full 8639800    13.04.2012 18:45:24 /u01/app/oracle/product/11.2/dbs/my_data05.dbf
      11      Full 8639800    13.04.2012 18:45:24 /u01/app/oracle/product/11.2/dbs/my_data06.dbf

    List of Archived Log Copies for database with db_unique_name ORA112
    =====================================================================

    Key     Thrd Seq     S Low Time
    ------- ---- ------- - -------------------
    295     1    242     A 13.04.2012 18:45:06
            Name: /u02/oradata/ora112/archivelogs/1_242_0767676036.arc

    Media recovery start SCN is 8639788
    Recovery must be done beyond SCN 8639822 to clear datafile fuzziness
    Finished restore at 13.04.2012 18:51:29

<br/><br/>

<strong>Применение команды RESTORE..VALIDATE</strong>

Утилита RMAN проверит, сможет ли она восстановить данные из бекапа.<br/>
Реального восстановления при этом не происходит.

    RMAN> RESTORE DATABASE VALIDATE;
    RMAN> RESTORE DATABASE VALIDATE CHECK LOGICAL;

<br/>

### Полное восстановление

    RMAN> restore database;
    RMAN> recover database;

<br/>

### Восстановление только табличного пространства system на время последнего бекапа

    RMAN> run{restore tablespace system; recover database;}

<br/>

### Неполное восстановление из последнего бекапа на 15 минут назад

```shell
RMAN> run{
shutdown immediate;
startup mount;
set until time "sysdate-15/(24*60)";
-- set until time "to_date('2010-06-01 12:50:30', 'yyyy-mm-dd hh24:mi:ss')";
-- set until scn=1891093;
restore database;
recover database;
alter database open resetlogs;}
```

<br/>

При выполнении неполного восстановления, необходимо открывать базу данных командой:

    RMAN> ALTER DATABASE OPEN RESETLOGS;

При выполнении resetlogs, меняется инкарнация базы данных.

// Восстановливать до того места, где возникает ошибка (например, отстутсвует архивный журнал или он испорчен).

    RMAN> recover database until cancel;

<!--

<br/>

### В случае потери всего, включая файлы данных, spfile, но при бекапах. (Пока не тестировалось на реальных базах. Пока просто для информации.)


    $ export ORACLE_SID=ORCL12
    $ rman target / nocatalog

<br/>

    RMAN> startup force nomount;

<br/>

    RMAN> list backupset;

<br/>

    RMAN> restore spfile to pfile '/tmp/initora12.ora' from '+ARCH/ORCL12/BACKUPSET/2015_08_19/nnsnf0_full_database_spfile_0.289.888163613';

<br/>

    RMAN> restore spfile from '+ARCH/ORCL12/BACKUPSET/2015_08_19/nnsnf0_full_database_spfile_0.289.888163613';

<br/>

Восстановили spfile.

    SQL> shutdown immediate;
    SQL> startup nomount;

<br/>

    $ rmant rarget / nocatalog
    RMAN> restore controlfile from '+ARCH/ORCL12/BACKUPSET/2015_08_19/nnsnf0_full_database_spfile_0.289.888163613';

<br/>

    SQL> alter database mount;



База в состоянии: Mounted

    RMAN> crosscheck backup;

    RMAN> catalog start with '+ARCH/ORCL12/BACKUPSET/2015_08_19/';

    RMAN> crosscheck archivelog all;


// Если нужно восстановить в каталог в котором были файлы данных

    RMAN> restore database;
    RMAN> recover database;



// Если нужно восстановить в каталог отличный от того, который был.

    RMAN> RUN {
        set newname for datafile 1 to '...../system*.dbf';
        set newname for datafile 2 to '...../sysadux*.dbf';
        set newname for datafile 3 to '...../undo*.dbf';
        set newname for datafile 4 to '...../user*.dbf';

        restore datafile 1,2,3,4;
        switch datafile all;
        recover datafile 1,2,3,4;
    }

<br/>

    RMAN> alter database open resetlogs;

-->
