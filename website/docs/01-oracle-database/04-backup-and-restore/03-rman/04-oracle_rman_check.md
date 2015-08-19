---
layout: page
title: Проверки с помощью RMAN
permalink: /docs/oracle-database/backup-and-restore/rman/oracle-rman-check/
---

<h2>Проверки с помощью RMAN</h2><br/>




// Команды для проверки

    RMAN> CROSSCHECK backup;
    RMAN> CROSSCHECK copy;
    RMAN> CROSSCHECK backup of database;
    RMAN> CROSSCHECK backup of controlfile;
    RMAN> CROSSCHECK archivelog all;



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
