---
layout: page
title: Создание резервных копий с помощью утилиты RMAN (Recovery Manager)
permalink: /docs/oracle-database/backup-and-restore/rman/oracle-rman-backup/
---

<h2>Создание резервных копий с помощью утилиты RMAN (Recovery Manager)</h2><br/>


<br/>
<h3>Бекапы могут храниться в backup set (по умолчанию) и image copies:</h3>

<ul>
<li>backup set  - данные хранятся в формате понятном только для RMAN.  В Backup set состоит из  Backup piece, каждый из которых может представлять из себя копию файла данных или копию управляющего файла, или копию архивлогов. </li>
<li>image copies - отличаются от копий, создаваемых, например с помощью команды cp, лишь тем, что информация о них заносится в управляющий файл или каталог восстановления.</li>
</ul>


Команда:<br/>

    RMAN> BACKUP AS BACKUPSET DATABASE;

Создаст резернвую копию как backup set


Команда:<br/>

    RMAN> BACKUP AS COPY DATABASE;

Создаст резернвую копию как image copies

<br/><br/>

Команда:

    RMAN> LIST BACKUP

Предоставит информацию о имеющихся backup set

<br/><br/>

Команда:

    RMAN> LIST COPY

Предоставит информацию о имеющихся image copies


<br/><br/>
<h3>Бекапы могут иметь статус:</h3>

<ul>
	<li>EXPIRED (Истекшие) - RMAN маркирует бекапы и копии данных как expired в случае, если при запуске CROSSCHECK (проверка бекапов) будут найдены ссылки на отсутсвующие или недоступные файлы.</li>
	<li>OBSOLETE (Устаревшие) - резервная копия считается устаревшей, если она уже больше не требуется для восстановления базы данных согласно используемой политике сохранности (retention policy).</li>
</ul>

<br/>
<h3>Получить информацию о файлах, которые нуждаются в бекапе</h3>

    RMAN> REPORT NEED BACKUP;

<br/>
<h3>Создать backup, явно указав расположение backup:</h3>

    RMAN> BACKUP AS BACKUPSET DATABASE FORMAT '/tmp/%U';
    RMAN> BACKUP AS COPY DATABASE FORMAT '/tmp/%U';

<br/>
<h3>Создать резервную копию архивных журналов:</h3>

Архивлоги можно как влкючать в backup так и не включать.
<br/>
Можно выполнить отдельно резервное копирование архивлогов.
<br/>

    RMAN> BACKUP ARCHIVELOG ALL TAG "ARCHIVELOG_BACKUP";

<br/><br/>

TAG "ARCHIVELOG_BACKUP" - определяет имя для создаваетого бекапа архивлогов как  "ARCHIVELOG_BACKUP".
<br/>

Если ввести команду:

    RMAN> LIST BACKUPSET TAG "ARCHIVELOG_BACKUP";


Можно быстро найти бекап по имени.
<br/>
<br/>


    List of Backup Sets
    ===================


    BS Key  Size       Device Type Elapsed Time Completion Time
    ------- ---------- ----------- ------------ -------------------
    217     162.37M    DISK        00:00:36     16.04.2012 12:57:41
            BP Key: 229   Status: AVAILABLE  Compressed: YES  Tag: ARCHIVELOG_BACKUP
            Piece Name: /u03/oracle_backups/fra/ORA112/backupset/2012_04_16/o1_mf_annnn_ARCHIVELOG_BACKUP_7rqqq1tl_.bkp

      List of Archived Logs in backup set 217
      Thrd Seq     Low SCN    Low Time            Next SCN   Next Time
      ---- ------- ---------- ------------------- ---------- ---------
      1    216     8545527    11.04.2012 22:01:01 8593981    12.04.2012 20:22:54
      1    217     8593981    12.04.2012 20:22:54 8613050    13.04.2012 04:23:11
      1    218     8613050    13.04.2012 04:23:11 8625132    13.04.2012 11:18:51
      1    219     8625132    13.04.2012 11:18:51 8625196    13.04.2012 11:21:03
      1    220     8625196    13.04.2012 11:21:03 8631647    13.04.2012 14:55:06
      1    221     8631647    13.04.2012 14:55:06 8631674    13.04.2012 14:55:21
      1    222     8631674    13.04.2012 14:55:21 8631745    13.04.2012 14:57:29
      1    223     8631745    13.04.2012 14:57:29 8631799    13.04.2012 14:59:10
      1    224     8631799    13.04.2012 14:59:10 8631966    13.04.2012 15:00:39
      1    225     8631966    13.04.2012 15:00:39 8632827    13.04.2012 15:21:02
      1    226     8632827    13.04.2012 15:21:02 8632880    13.04.2012 15:22:44
      1    227     8632880    13.04.2012 15:22:44 8635557    13.04.2012 16:47:23
      1    228     8635557    13.04.2012 16:47:23 8635605    13.04.2012 16:49:04
      1    229     8635605    13.04.2012 16:49:04 8637304    13.04.2012 17:31:20
      1    230     8637304    13.04.2012 17:31:20 8637363    13.04.2012 17:33:02
      1    231     8637363    13.04.2012 17:33:02 8638314    13.04.2012 18:01:14
      1    232     8638314    13.04.2012 18:01:14 8638384    13.04.2012 18:03:06
      1    233     8638384    13.04.2012 18:03:06 8638470    13.04.2012 18:05:15
      1    234     8638470    13.04.2012 18:05:15 8638540    13.04.2012 18:06:57
      1    235     8638540    13.04.2012 18:06:57 8639146    13.04.2012 18:27:51
      1    236     8639146    13.04.2012 18:27:51 8639204    13.04.2012 18:29:33
      1    237     8639204    13.04.2012 18:29:33 8639566    13.04.2012 18:39:55
      1    238     8639566    13.04.2012 18:39:55 8639637    13.04.2012 18:41:36
      1    239     8639637    13.04.2012 18:41:36 8639730    13.04.2012 18:43:30
      1    240     8639730    13.04.2012 18:43:30 8639757    13.04.2012 18:44:14
      1    241     8639757    13.04.2012 18:44:14 8639788    13.04.2012 18:45:06
      1    242     8639788    13.04.2012 18:45:06 8639850    13.04.2012 18:46:47
      1    243     8639850    13.04.2012 18:46:47 8661907    14.04.2012 04:24:15
      1    244     8661907    14.04.2012 04:24:15 8710176    15.04.2012 04:25:00
      1    245     8710176    15.04.2012 04:25:00 8734000    15.04.2012 14:01:51
      1    246     8734000    15.04.2012 14:01:51 8771516    16.04.2012 10:10:40
      1    247     8771516    16.04.2012 10:10:40 8776238    16.04.2012 12:57:02



<br/>
<h3>Создать копию текущего CONTROLFILE</h3>

    RMAN> BACKUP CURRENT CONTROLFILE TAG "CONTROLFILE";


<br/>
<h3>Создать копию SPFILE</h3>

    RMAN> BACKUP SPFILE TAG "SPFILE";

<br/>
<h3>Создание полного бекапа:</h3>

Полный бекап (FULL BACKUP) - включает все файлы данных, управляющий файл (control file) и файл серверных параметров (sp file).

<br/>
<br/>

    RMAN> BACKUP FULL DATABASE TAG "FULL_DATABASE_BACKUP" PLUS ARCHIVELOG TAG "FULL_ARCHIVELOGS_BACKUP";

<br/><br/>

    RMAN> LIST BACKUP SUMMARY;

<br/><br/>


    List of Backups
    ===============
    Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
    ------- -- -- - ----------- ------------------- ------- ------- ---------- ---
    200     B  A  A DISK        13.04.2012 18:40:03 1       1       YES        FULL_ARCHIVELOGS_BACKUP
    201     B  F  A DISK        13.04.2012 18:40:10 1       1       YES        FULL_DATABASE_BACKUP
    202     B  F  A DISK        13.04.2012 18:40:12 1       1       YES        FULL_DATABASE_BACKUP
    203     B  F  A DISK        13.04.2012 18:40:13 1       1       YES        FULL_DATABASE_BACKUP
    204     B  F  A DISK        13.04.2012 18:40:46 1       1       YES        FULL_DATABASE_BACKUP
    205     B  F  A DISK        13.04.2012 18:41:28 1       1       YES        FULL_DATABASE_BACKUP
    206     B  F  A DISK        13.04.2012 18:41:35 1       1       YES        FULL_DATABASE_BACKUP
    207     B  A  A DISK        13.04.2012 18:41:37 1       1       YES        FULL_ARCHIVELOGS_BACKUP


<br/><br/>

Key - Уникальный ключ идентификации. <br/>
TY - Тип бекапа: backup set (B) или copy (P).<br/>
LV - F - file; A - Archivelogs.<br/>
S - Статус бекапа: A (available), U (unavailable), or X (all backup pieces in set expired). Refer to the CHANGE, CROSSCHECK, and DELETE commands for an explanation of each status.

    RMAN> BACKUP FULL DATABASE TAG "FULL_DATABASE_BEFORE_UPGRADE" PLUS ARCHIVELOG TAG "FULL_ARCHIVELOGS_BEFORE_UPGRADE";

<br/>

    RMAN> LIST BACKUP SUMMARY;

<br/>


    List of Backups
    ===============
    Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
    ------- -- -- - ----------- ------------------- ------- ------- ---------- ---
    200     B  A  A DISK        13.04.2012 18:40:03 1       1       YES        FULL_ARCHIVELOGS_BACKUP
    201     B  F  A DISK        13.04.2012 18:40:10 1       1       YES        FULL_DATABASE_BACKUP
    202     B  F  A DISK        13.04.2012 18:40:12 1       1       YES        FULL_DATABASE_BACKUP
    203     B  F  A DISK        13.04.2012 18:40:13 1       1       YES        FULL_DATABASE_BACKUP
    204     B  F  A DISK        13.04.2012 18:40:46 1       1       YES        FULL_DATABASE_BACKUP
    205     B  F  A DISK        13.04.2012 18:41:28 1       1       YES        FULL_DATABASE_BACKUP
    206     B  F  A DISK        13.04.2012 18:41:35 1       1       YES        FULL_DATABASE_BACKUP
    207     B  A  A DISK        13.04.2012 18:41:37 1       1       YES        FULL_ARCHIVELOGS_BACKUP
    208     B  A  A DISK        13.04.2012 18:44:23 1       1       YES        FULL_ARCHIVELOGS_BEFORE_UPGRADE
    209     B  A  A DISK        13.04.2012 18:45:14 1       1       YES        FULL_ARCHIVELOGS_BEFORE_UPGRADE
    210     B  F  A DISK        13.04.2012 18:45:21 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    211     B  F  A DISK        13.04.2012 18:45:23 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    212     B  F  A DISK        13.04.2012 18:45:24 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    213     B  F  A DISK        13.04.2012 18:45:57 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    214     B  F  A DISK        13.04.2012 18:46:40 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    215     B  F  A DISK        13.04.2012 18:46:46 1       1       YES        FULL_DATABASE_BEFORE_UPGRADE
    216     B  A  A DISK        13.04.2012 18:46:48 1       1       YES        FULL_ARCHIVELOGS_BEFORE_UPGRADE

<br/>

Получить информацю о созданном бекапе.

    RMAN> LIST BACKUP TAG "FULL_DATABASE_BEFORE_UPGRADE";

<br/>

    List of Backup Sets
    ===================


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
    215     Full    1.09M      DISK        00:00:01     13.04.2012 18:46:46
            BP Key: 227   Status: AVAILABLE  Compressed: YES  Tag: FULL_DATABASE_BEFORE_UPGRADE
            Piece Name: /u03/oracle_backups/fra/ORA112/backupset/2012_04_13/o1_mf_ncsnf_FULL_DATABASE_BEFORE_7rjh2ppm_.bkp
      SPFILE Included: Modification time: 12.04.2012 20:22:52
      SPFILE db_unique_name: ORA112
      Control File Included: Ckp SCN: 8639845      Ckp time: 13.04.2012 18:46:45


<br/>
<h3>Создание сразу нескольких копий:</h3>
RMAN> BACKUP AS BACKUPSET COPIES 2 DATABASE FORMAT '/tmp/1/%U' , '/tmp/2/%U';


<br/>
<h3>Создание инкрементальной копии базы данных:</h3>


    RUN {
    CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;
    BACKUP INCREMENTAL LEVEL 0 TAG "LEVEL 0" DATABASE PLUS ARCHIVELOG;
    BACKUP CURRENT CONTROLFILE SPFILE;
    }

<br/>

    BACKUP INCREMENTAL LEVEL 1 TAG "LEVEL 1" DATABASE PLUS ARCHIVELOG;



Создать кумулятивный (включает в себя измениния отраженные в инкрементальных бекапах ) бекап с уровнем 1

    RMAN> backup incremental level 1 cumulative database;



<br/>
<h3>Получить данные по результам выполнения команд резервного копирования:</h3>




    SQL> set pagesize 0;
    SQL> select start_time as "Data", status as "Result" from v$rman_backup_job_details order by 1 desc;
    16.04.2012 12:57:02 FAILED
    13.04.2012 17:16:30 FAILED
    13.04.2012 17:09:45 COMPLETED
    13.04.2012 17:05:32 COMPLETED
    13.04.2012 17:03:20 COMPLETED
    13.04.2012 17:01:37 COMPLETED
    13.04.2012 14:55:06 FAILED
    13.04.2012 14:31:26 FAILED
    13.04.2012 13:43:18 FAILED
    13.04.2012 11:07:47 FAILED
    09.04.2012 21:17:13 COMPLETED
    09.04.2012 21:02:48 COMPLETED

    12 rows selected.
