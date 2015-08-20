---
layout: page
title: Проверки с помощью RMAN
permalink: /docs/oracle-database/backup-and-restore/rman/oracle-rman-check/
---

### Проверки с помощью RMAN


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
