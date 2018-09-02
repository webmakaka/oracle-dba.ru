---
layout: page
title: Скрипт RMAN для создания бекапов. Пример 1. Бекап в FRA
permalink: /database/backup-and-restore/rman/oracle_rman_scripts_example/example1/
---

# Скрипт RMAN для создания бекапов.

### Пример 1. Бекап в FRA

<br/>

**База в режиме работы ARCHIVELOG**

<br/>

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

<br/>
<br/>

### ALTER SYSTEM SWITCH LOGFILE vs ALTER SYSTEM ARCHIVE LOG CURRENT

В чём состоит разница между командами ALTER SYSTEM SWITCH LOGFILE и ALTER SYSTEM ARCHIVE LOG CURRENT?

На первый взгляд, эти команды выполняют одно и то же:

1. Вызывают событие checkpoint
2. Процесс LGWR перестаёт писать в текущий лог и начинает писать в следующий
3. Процесс ARCH архивирует старый лог

Но делают они это немного по-разному.

**ALTER SYSTEM SWITCH LOGFILE** -
Работает асинхронно, и возвращает управление вызвавшей сессии до того, как ARCH заархивирует лог. В случае, если используется RAC, переключит лог только на текущем экземпляре.

**ALTER SYSTEM ARCHIVE LOG CURRENT** -
Дожидается завершения архивирования и возвращает управление только когда все 3 пункта выполнены. Если используется RAC, то переключит и заархивирует логи на всех экземплярах.

Основная опасность при использовании ALTER SYSTEM SWITCH LOGFILE в скриптах (в первую очередь это относится к скриптам резервного копирования с помощью RMAN) - вероятность того, что в силу асинхронности этой команды управление будет передано скрипту сразу и скрипт будет выполняться дальше, хотя архивирование ещё не завершено. Таким образом, безопаснее всегда использовать ALTER SYSTEM ARCHIVE LOG CURRENT.

https://dba-notes.org/2011/11/18/alter-system-switch-logfile-vs-alter-system-archive-log-current/
