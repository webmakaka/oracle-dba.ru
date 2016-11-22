---
layout: page
title: Создание копии активной базы данных с помощью RMAN
permalink: /database/backup-and-restore/rman/duplicate-active-database/
---

### Создание копии активной базы данных с помощью RMAN:

Тоже самое, что и в предыдущем документе, тоже самое, что и при dataguard.

Только RMAN script другой.

    $ rman target sys/manager@ORCL12 nocatalog
    RMAN> connect auxiliary sys/manager@copy12

<br/>

    RMAN> RUN{
        allocate channel dupli1 type disk;
        allocate auxiliary channel1 dupli2 type disk;
        duplicate target database to copy12 from active database nofilenamecheck;
    }
