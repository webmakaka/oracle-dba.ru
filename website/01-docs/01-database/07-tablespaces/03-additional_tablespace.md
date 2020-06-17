---
layout: page
title: Расширение табличных пространств (создание дополнительных файлов для табличных пространств)
description: Расширение табличных пространств (создание дополнительных файлов для табличных пространств)
keywords: Oracle Database, Дополнительные файлы для табличных пространств
permalink: /docs/architecture/tablespaces/additional-tablespace/
---

# Расширение табличных пространств (создание дополнительных файлов для табличных пространств)

<br/>

    $ sqlplus / as sysdba

Посмотреть какие файлы базы данных используются базой данных и где они расположены:

    SQL> set linesize 200;
    SQL> set pagesize 0;
    SQL> col name format a40;

<br/>

    SQL> SELECT file#, name, status
    FROM v$datafile;

Создаю новое табличное пространство для индексов и данных:

    SQL> CREATE TABLESPACE "MY_DATA"
    DATAFILE '/u02/oradata/ora112/my_data01.dbf' SIZE 2G AUTOEXTEND OFF;

<br/>

    SQL> CREATE TABLESPACE "MY_INDEXES"
    DATAFILE '/u02/oradata/ora112/my_indexes01.dbf' SIZE 2G AUTOEXTEND OFF;

При необходимости, можно добавить дополнительное место для данных (когда будет такая необходимость) следующими командами:

    SQL> ALTER TABLESPACE "MY_DATA"
    ADD DATAFILE  '/u02/oradata/ora112/my_data02.dbf' SIZE 2G AUTOEXTEND OFF;

Для индексов:

    SQL> ALTER TABLESPACE “MY_INDEXES”
    ADD DATAFILE  '/u02/oradata/ora112/my_indexes02.dbf' SIZE 2G AUTOEXTEND OFF;

Иногда, нужно создать дополнительное табличное пространство для табличного пространства отмены (undo).

    SQL> create undo tablespace "UNDOTBS_01" datafile '/u02/oradata/ora112/undo01.dbf' size 1G autoextend off;
    SQL> ALTER SYSTEM SET UNDO_TABLESPACE = "undotbs_01";
    SQL> drop tablespace UNDOTBS1;

<br/>

    ALTER TABLESPACE "UNDOTBS_01" ADD DATAFILE '/u02/oradata/SID/undotbs02.dbf' SIZE 2G AUTOEXTEND OFF;

UNDO_RETENTION - (при включенном FLASHBACK) определяет минимальное время в секундах, за которое можно отменить (посмотреть) изменение в базе данных. При этом данные будут храниться в UNDO_TABLESPACE (необходимо обеспечить достаточный размер табличного пространства) и перезаписываться по мере необходимости, обеспечивая минимальное значение, указанное в UNDO_RETENTION. Не поддерживается для LOB.

Задаю параметр UNDO_RETENTION равный 30 минутам

    SQL> alter system set UNDO_RETENTION = 1800;
    SQL> alter tablespace UNDOTBS_01 RETENTION GUARANTEE;

<br/>

    SQL> show parameter UNDO_RETENTION

<br/>

    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    undo_retention                       integer     1800

Создать новое табличное пространство для временных данных.

    SQL>  CREATE TEMPORARY TABLESACE "MY_TEMP"
    TEMPFILE '/u02/oradata/ora112/my_temp01.dbf' SIZE 2G AUTOEXTEND OFF;

Добавить дополнительный файл для временных табличных пространств.

    SQL> ALTER TABLESPACE “MY_TEMP”
    ADD TEMPFILE '/u02/oradata/ora112/my_temp02.dbf' SIZE 2G AUTOEXTEND OFF;
