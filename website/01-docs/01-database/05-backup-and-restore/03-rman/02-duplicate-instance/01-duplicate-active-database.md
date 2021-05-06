---
layout: page
title: Создание копии активной базы данных Oracle с помощью RMAN
description: Создание копии активной базы данных Oracle с помощью RMAN
keywords: Oracle Database, RMAN, Создание копии активной базы данных
permalink: /database/backup-and-restore/rman/duplicate-instance/duplicate-active-database/
---

# Создание копии активной базы данных Oracle с помощью RMAN

Тоже самое, что и в <a href="/database/backup-and-restore/rman/duplicate-instance/duplicate-database-from-backup/">предыдущем документе</a>, тоже самое, что и при dataguard.

Только RMAN script другой.

    $ rman target sys/manager@ORCL12 nocatalog
    RMAN> connect auxiliary sys/manager@copy12

<br/>

    RMAN> RUN{
        allocate channel dupli1 type disk;
        allocate auxiliary channel1 dupli2 type disk;
        duplicate target database to copy12 from active database nofilenamecheck;
    }
