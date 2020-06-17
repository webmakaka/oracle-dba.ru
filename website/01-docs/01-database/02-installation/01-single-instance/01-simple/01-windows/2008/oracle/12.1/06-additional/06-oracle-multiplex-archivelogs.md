---
layout: page
title: Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server - Мультиплексирование archivelog
description: Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server - Мультиплексирование archivelog
keywords: Oracle DataBase, Installation, Windows 2008, Мультиплексирование archivelog
permalink: /database/installation/single-instance/simple/windows/2008/oracle/12.1/oracle-multiplex-archivelogs/
---

# <a href="/database/installation/single-instance/simple/windows/2008/oracle/12.1/">[Инсталляция Oracle Database 12c Release 1 в Microsoft Windows 2008 Server]</a>: Мультиплексирование archivelog

<br/>

Создание каталога для хранения файлов резервных копий и архивных журналов

    $ md e:\app\oracle\oradata\ora121\archives
    $ md f:\app\oracle\oradata\ora121\archives

<br/>

    sqlplus / as sysdba

<br/>

Задать разделы для архивных журналов

    SQL>  ALTER SYSTEM SET LOG_ARCHIVE_DEST_1='location=e:\app\oracle\oradata\ora121\archives mandatory' scope=both;
    SQL>  ALTER SYSTEM SET LOG_ARCHIVE_DEST_2='location=f:\app\oracle\oradata\ora121\archives mandatory' scope=both;

Посмотреть текущие значения параметра LOG_ARCHIVE_DEST

    SQL> show parameter LOG_ARCHIVE_DEST;

Задать формат для файлов arhivelogs

    SQL>  ALTER SYSTEM SET LOG_ARCHIVE_FORMAT='%t_%s_%R.arc' scope=spfile;

<br/>

    SQL> shutdown immediate;
    SQL> startup;
    SQL> quit
