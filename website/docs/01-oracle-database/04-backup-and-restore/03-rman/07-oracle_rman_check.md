---
layout: page
title: Проверки с помощью RMAN
permalink: /docs/oracle-database/backup-and-restore/rman/oracle-rman-check/
---

### Проверки с помощью RMAN


You can get detailed information using PREVIEW like which files the backup set contains, which archivelogs will be used, etc...

    RMAN> RESTORE DATABASE PREVIEW;
    RMAN> RESTORE ARCHIVELOG ALL PREVIEW;

With VALIDATE you can be sure that you will be able to use that backup to restore your database as it reads all the files.

    RMAN> RESTORE DATABASE VALIDATE;
    RMAN> RESTORE ARCHIVELOG ALL VALIDATE;

<br/>

### Using RESTORE... PREVIEW

    RESTORE DATABASE PREVIEW;
    RESTORE TABLESPACE users PREVIEW;
    RESTORE DATAFILE 3 PREVIEW;
    RESTORE ARCHIVELOG FROM LOGSEQ 200 PREVIEW;
    RESTORE ARCHIVELOG FROM TIME 'SYSDATE-7' PREVIEW;
    RESTORE ARCHIVELOG FROM SCN 234546 PREVIEW;


<br/>

### Using RESTORE... PREVIEW SUMMARY


    RESTORE DATABASE PREVIEW SUMMARY;
    RESTORE TABLESPACE users PREVIEW SUMMARY;
    RESTORE DATAFILE 3 PREVIEW SUMMARY;
    RESTORE ARCHIVELOG FROM LOGSEQ 200 PREVIEW SUMMARY;
    RESTORE ARCHIVELOG FROM TIME 'SYSDATE-7' PREVIEW SUMMARY;
    RESTORE ARCHIVELOG FROM SCN 234546 PREVIEW SUMMARY;


<br/>

### CROSSCHECK

    RMAN> CROSSCHECK backup;
    RMAN> CROSSCHECK copy;
    RMAN> CROSSCHECK archivelog all;
    RMAN> CROSSCHECK backup of controlfile;
    RMAN> CROSSCHECK backup of database;



<br/>

<strong>Проверка базы с помощью утилиты RMAN:</strong>

    RMAN> VALIDATE DATABASE;


<br/>
<h3>Проверка файлов, хранящихся в FRA:</h3>

    RMAN> VALIDATE RECOVERY AREA;


RMAN читает все блоки и проверяет их на поврежденность. <br/>
Если находятся поврежденные блоки, то информация о них попадает в V$DATABASE_BLOCK_CORRUPTION<br/>

    RMAN> BACKUP VALIDATE DATABASE;
    RMAN> BACKUP VALIDATE DATABASE ARCHIVELOG ALL;
