---
layout: page
title: Скрипт RMAN для создания бекапов. Пример 1. Бекап в FRA
permalink: /docs/oracle-database/backup-and-restore/rman/oracle_rman_scripts_example/example1/
---

### Скрипт RMAN для создания бекапов. Пример 1. Бекап в FRA

База в режиме работы ARCHIVELOG

<br/>

	$ mkdir -p $ORACLE_HOME/scripts

<br/>

	$ cd $ORACLE_HOME/scripts

<br/>

	$ vi backup-rman-script.rman


<br/>

	RUN {

	ALLOCATE CHANNEL c1 DEVICE TYPE DISK;

	CONFIGURE RETENTION POLICY TO REDUNDANCY 1;
	CONFIGURE BACKUP OPTIMIZATION ON;
	CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;

	BACKUP FULL DATABASE TAG "FULL_DATABASE_DATAFILES";

	SQL 'ALTER SYSTEM ARCHIVE LOG CURRENT';

	BACKUP ARCHIVELOG ALL TAG "FULL_DATABASE_ARCHIVELOGS";

	BACKUP CURRENT CONTROLFILE TAG "FULL_DATABASE_CONTROLFILE";

	BACKUP SPFILE TAG "FULL_DATABASE_SPFILE";

	DELETE NOPROMPT OBSOLETE;


	CONFIGURE RETENTION POLICY CLEAR;
	CONFIGURE BACKUP OPTIMIZATION CLEAR;
	CONFIGURE DEVICE TYPE DISK CLEAR;

	RELEASE CHANNEL c1;

	}

Проверка синтаксиса созданного файла сценария

	$ rman CHECKSYNTAX @backup-rman-script.rman

Выполнение скрипта резервного копирования

	$ rman target / @backup-rman-script.rman

Если используется Oracle Catalog, команда может выглядеть следующим образом

    $ rman target / catalog rman/rman123@rman12 @backup-rman-script.rman

<br/>

    RMAN> LIST BACKUPSET TAG="FULL_DATABASE_DATAFILES";

<br/>

    RMAN> LIST BACKUP SUMMARY;


    List of Backups
    ===============
    Key     TY LV S Device Type Completion Time     #Pieces #Copies Compressed Tag
    ------- -- -- - ----------- ------------------- ------- ------- ---------- ---
    48      B  F  A DISK        19/08/2015 15:34:49 1       1       YES        FULL_DATABASE_DATAFILES
    50      B  A  A DISK        19/08/2015 15:35:03 1       1       YES        FULL_DATABASE_ARCHIVELOGS
    51      B  F  A DISK        19/08/2015 15:35:07 1       1       YES        FULL_DATABASE_CONTROLFILE
    52      B  F  A DISK        19/08/2015 15:35:08 1       1       YES        FULL_DATABASE_SPFILE

<br/>

    RMAN> list backupset summary;
