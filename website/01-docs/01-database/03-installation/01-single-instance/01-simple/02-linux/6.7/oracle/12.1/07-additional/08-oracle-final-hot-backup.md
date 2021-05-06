---
layout: page
title: Инсталляция Oracle DataBase 12c в Oracle Linux 6.7 - Контрольный backup (горячий backup)
description: Инсталляция Oracle DataBase 12c в операционной системе Oracle Linux 6.7 - Контрольный backup (горячий backup)
keywords: Oracle DataBase 12c, Oracle Linux 6.7, Hot backup, Горячий backup
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/oracle-final-hot-backup/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Контрольный backup (горячий backup)

    $ mkdir -p /u02/oracle/oradata/12.1/${ORACLE_SID}/scripts

<br/>

    $ cd /u02/oracle/oradata/12.1/${ORACLE_SID}/scripts

<br/>

    $ vi rmanscript.rman

<br/>

    RUN {
    CONFIGURE DEVICE TYPE DISK BACKUP TYPE TO COMPRESSED BACKUPSET;
    BACKUP FULL DATABASE TAG "FULL_DATABASE" PLUS ARCHIVELOG TAG "FULL_DATABASE_ARCHIVELOGS";
    BACKUP CURRENT CONTROLFILE TAG "FULL_DATABASE_CONTROLFILE";
    BACKUP SPFILE TAG "FULL_DATABASE_SPFILE";
    }

Проверка синтаксиса созданного файла сценария

    $ rman CHECKSYNTAX @rmanscript.rman

Выполнение скрипта резервного копирования

    $ rman target / @rmanscript.rman

<br/>

### Посмотреть список бекапов

    RMAN> rman target /

<br/>

    RMAN> list backup of database summary;

<br/>

Следующей командой я сообщаю, что все бекапы кроме последного, следует поменить как obsolete.

    RMAN> CONFIGURE RETENTION POLICY TO REDUNDANCY 1;

Теперь прошу RMAN удалить устаревшие бекапы (без подтверждения).

    RMAN> delete noprompt obsolete;

<br/>

    RMAN> list backup of database summary;

<br/>

    RMAN>  quit
