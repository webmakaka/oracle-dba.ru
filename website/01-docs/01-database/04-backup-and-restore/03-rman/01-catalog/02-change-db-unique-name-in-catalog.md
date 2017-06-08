---
layout: page
title: Поменять db_unique_name в RMAN каталоге
permalink: /database/backup-and-restore/rman/change-db-unique-name-in-catalog/
---


# Поменять db_unique_name в RMAN каталоге (нужно, если поменялось db_unique_name инстанса)

Сначала нужно поменять уникальное имя инстанса базы.

    SQL> show parameter db_unique_name

<br/>

    $ rman target / catalog rman/rman123@rman12


</br>

    RMAN> LIST DB_UNIQUE_NAME OF DATABASE;


    List of Databases
    DB Key  DB Name  DB ID            Database Role    Db_unique_name
    ------- ------- ----------------- ---------------  ------------------
    1       ORCL12   3487575625       PRIMARY          ORCL12


// Если нужно поменять уникальное имя базы данных в rman каталоге.

    RMAN> CHANGE DB_UNIQUE_NAME FROM ORCL12 TO ORCL12C
