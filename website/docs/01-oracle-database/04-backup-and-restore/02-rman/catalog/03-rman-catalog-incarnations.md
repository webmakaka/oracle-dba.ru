---
layout: page
title: Пример с инкарнациями
permalink: /docs/oracle-database/backup-and-restore/rman/rman-incarnations-sample/
---




### Инкарнации базы данных


    $ rman target / catalog rman/rman123@rman12


Новая инкарнация создается при неполном восстновлении базы, когда база открывается с опцией resetlogs. Т.е. данные из redologs удаляются. Вроде как у базы, начинается новая жизнь. Историю жизней базы, можно посмотреть следующими способами.


    RMAN> LIST INCARNATION OF DATABASE;


    List of Database Incarnations
    DB Key  Inc Key DB Name  DB ID            STATUS  Reset SCN  Reset Time
    ------- ------- -------- ---------------- --- ---------- ----------
    1       16      ORCL12   3487575625       PARENT  1          07/07/2014 05:38:47
    1       2       ORCL12   3487575625       CURRENT 1594143    16/08/2015 21:29:45


<br/>

        SQL> select incarnation#, resetlogs_change# from v$database_incarnation;

        INCARNATION# RESETLOGS_CHANGE#
        ------------ -----------------
        	   1		     1
        	   2	       1594143


Вообщем смысл инкарнаций в том, что база откатывается на какое-то состояние в прошлом и уже с этого состояния идет новая жизнь. Как снапшоты на виртуалках, когда то к одному состоянию откатился, потом к другому. В результате получается какое-то дерево с разными ветками. Насколько это часто используется в базах? нечасто. Ну вот сами подумайте, как можно на production базе делать какие-то откаты и работать с какой-то точки? Должны быть серьезные причины для этого. Видел один или два раза давно как потерян был архив лог а база требовала восстановления. Вот откатывали на состояние предшествующее этому архивлогу и делали инкарнацию. Но, как мне видится, это все были костыли из за того, что не подготовили сервер с доп избыточностью. И делали это исколючительно для того, чтобы не потерять всю базу.


<br/>

    RMAN> backup database;


<br/>

    SQL> create table test as select * from all_objects;

<br/>

    SQL> select count(1) from test;

      COUNT(1)
    ----------
         89402


<br/>

     SQL> select current_scn from v$database;

     CURRENT_SCN
     -----------
         1891044


<br/>

    SQL> delete from test;

<br/>

    SQL> commit;

<br/>

    SQL> select current_scn from v$database;

    CURRENT_SCN
    -----------
        1891093


<br/>

    SQL> drop table test;

<br/>

    SQL> select current_scn from v$database;

    CURRENT_SCN
    -----------
    1891136

<br/>

    SQL> alter system switch logfile;

<br/>

    SQL> select incarnation#, resetlogs_change# from v$database_incarnation;

    INCARNATION# RESETLOGS_CHANGE#
    ------------ -----------------
       1		     1
       2	       1594143


<br/>

Восстановление к определенному scn в прошлом

    SQL> shutdow immediate;
    SQL> startup mount;

<br/>

    $ rman target / catalog rman/rman123@rman12

<br/>

    Восстановление на момент предшествующий удалению таблицы test.
    Т.е. должна быть восстановлена таблица, но данных в ней не должно быть.

    RUN {
        set until scn=1891093;
        restore database;
        recover database;
    }

<br/>

    SQL> select status from v$instance;

    STATUS
    ------------
    MOUNTED


<br/>


    SQL> alter database open resetlogs;

<br/>

    SQL> desc test;
     Name					   Null?    Type
     ----------------------------------------- -------- ----------------------------
     OWNER					   NOT NULL VARCHAR2(128)
     OBJECT_NAME				   NOT NULL VARCHAR2(128)
     SUBOBJECT_NAME 				    VARCHAR2(128)
     OBJECT_ID				   NOT NULL NUMBER
     DATA_OBJECT_ID 				    NUMBER
     OBJECT_TYPE					    VARCHAR2(23)
     CREATED				   NOT NULL DATE
     LAST_DDL_TIME				   NOT NULL DATE
     TIMESTAMP					    VARCHAR2(19)
     STATUS 					    VARCHAR2(7)
     TEMPORARY					    VARCHAR2(1)
     GENERATED					    VARCHAR2(1)
     SECONDARY					    VARCHAR2(1)
     NAMESPACE				   NOT NULL NUMBER
     EDITION_NAME					    VARCHAR2(128)
     SHARING					    VARCHAR2(13)
     EDITIONABLE					    VARCHAR2(1)
     ORACLE_MAINTAINED				    VARCHAR2(1)


<br/>


    SQL> select count(1) from test;

      COUNT(1)
    ----------
    	 0


<br/>


Теперь откатываемся на момент предшествующий удалению данных из таблицы.


    RUN {
        set until scn=1891044;
        restore database;
        recover database;
    }

<br/>

    executing command: SET until clause
    new incarnation of database registered in recovery catalog
    starting full resync of recovery catalog
    full resync complete

    Starting restore at 18/08/2015 08:31:19
    RMAN-00571: ===========================================================
    RMAN-00569: =============== ERROR MESSAGE STACK FOLLOWS ===============
    RMAN-00571: ===========================================================
    RMAN-03002: failure of restore command at 08/18/2015 08:31:19
    RMAN-06004: ORACLE error from recovery catalog database: RMAN-20208: UNTIL CHANGE is before RESETLOGS change


<br/>


    RMAN> LIST INCARNATION OF DATABASE;


    List of Database Incarnations
    DB Key  Inc Key DB Name  DB ID            STATUS  Reset SCN  Reset Time
    ------- ------- -------- ---------------- --- ---------- ----------
    1       16      ORCL12   3487575625       PARENT  1          07/07/2014 05:38:47
    1       2       ORCL12   3487575625       PARENT  1594143    16/08/2015 21:29:45
    1       255     ORCL12   3487575625       CURRENT 1891094    18/08/2015 08:26:32


<br/>


// пример который должен быть выполнен

    RMAN> reset database to incarnation "Inc Key";

// выполняю

    RMAN> reset database to incarnation 2;


<br/>

Повторяю попытку.

    RUN {
        set until scn=1891044;
        restore database;
        recover database;
    }

<br/>

    SQL> alter database open resetlogs;

<br/>

    SQL> slect count(1) from test;

<br/>

    SQL> select count(1) from test;

      COUNT(1)
    ----------
         89402

<br/>

     RMAN> LIST INCARNATION OF DATABASE;

     new incarnation of database registered in recovery catalog
     starting full resync of recovery catalog
     full resync complete

     List of Database Incarnations
     DB Key  Inc Key DB Name  DB ID            STATUS  Reset SCN  Reset Time
     ------- ------- -------- ---------------- --- ---------- ----------
     1       16      ORCL12   3487575625       PARENT  1          07/07/2014 05:38:47
     1       2       ORCL12   3487575625       PARENT  1594143    16/08/2015 21:29:45
     1       335     ORCL12   3487575625       CURRENT 1891045    18/08/2015 08:38:31
     1       255     ORCL12   3487575625       ORPHAN  1891094    18/08/2015 08:26:32
