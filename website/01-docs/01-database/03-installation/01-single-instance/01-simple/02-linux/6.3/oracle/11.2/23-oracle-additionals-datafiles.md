---
layout: page
title: Инсталляция Oracle DataBase 11.2.0.3.2 в Oracle Linux 6.3 - Расширение табличных пространств (создание дополнительных файлов для табличных пространств)
description: Инсталляция Oracle DataBase 11.2.0.3.2 в операционной системе Oracle Linux 6.3 - Расширение табличных пространств (создание дополнительных файлов для табличных пространств)
keywords: Oracle DataBase 11.2, Oracle Linux 6.3, Создание файлов для табличных пространств
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/oracle-additionals-datafiles/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Расширение табличных пространств (создание дополнительных файлов для табличных пространств)

<br/>

    $ sqlplus / as sysdba

Посмотреть какие файлы базы данных используются базой данных и где они расположены:

    SQL> set linesize 200;
    SQL> set pagesize 0;
    SQL> col name format a40;
    SQL> SELECT file#, name, status
    FROM v$datafile;

1. Создание нового табличное пространство для индексов и данных:


    SQL> CREATE TABLESPACE "MY_DATA"
    DATAFILE '/u02/oradata/ora112/my_data01.dbf' SIZE 2G AUTOEXTEND OFF;

При необходимости, можно добавить дополнительное место для данных (когда будет такая необходимость) следующими командами:

    SQL> ALTER TABLESPACE “MY_DATA”
    ADD DATAFILE  '/u02/oradata/ora112/my_data02.dbf' SIZE 2G AUTOEXTEND OFF;

<br/>

    SQL> CREATE TABLESPACE "MY_INDEXES"
    DATAFILE '/u02/oradata/ora112/my_indexes01.dbf' SIZE 2G AUTOEXTEND OFF;

При необходимости, можно добавить дополнительное место для индексов (когда будет такая необходимость) следующими командами:

<br/>

    SQL> ALTER TABLESPACE “MY_INDEXES”
    ADD DATAFILE  '/u02/oradata/ora112/my_indexes02.dbf' SIZE 2G AUTOEXTEND OFF;

<br/><br/>

<hr/>
<br/><br/>

2. Иногда, нужно создать дополнительное табличное пространство для табличного пространства отмены (undo).


    SQL> CREATE undo tablespace "UNDO" datafile '/u02/oradata/ora112/undo01.dbf' size 1G autoextend off;

Определяю созданное табличное пространство, как пространство по умолчанию

    SQL> ALTER SYSTEM SET UNDO_TABLESPACE = "UNDO";

Удаляю старое табличное пространство

    SQL> drop tablespace UNDOTBS1;

<br/><br/>

<hr/>
<br/><br/>

3. Создать новое табличное пространство для временных данных.


    SQL> CREATE TEMPORARY TABLESPACE "MY_TEMP"
    TEMPFILE '/u02/oradata/ora112/my_temp01.dbf' SIZE 2G AUTOEXTEND OFF;

Добавить дополнительный файл для временных табличных пространств.

    SQL> ALTER TABLESPACE “MY_TEMP”
    ADD TEMPFILE '/u02/oradata/ora112/my_temp02.dbf' SIZE 2G AUTOEXTEND OFF;

<br/>

    SQL> quit

<br/><br/>
<br/><br/>

<div style="padding:10px; border:thin solid black;">

    <h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
