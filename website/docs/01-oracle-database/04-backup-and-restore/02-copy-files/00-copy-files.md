---
layout: page
title: Пример резервного копирования базы Oracle средствами операционной системы (холодный бекап, NOARCHIVELOG)
permalink: /docs/oracle-database/backup-and-restore/copy/
---


### Пример резервного копирования базы Oracle средствами операционной системы (холодный бекап, NOARCHIVELOG)





**Пока не рекомендуется использовать! Нужно поднять базу из скопированных файлов на каком-нибудь другом сервере**


Посмотрю, где лежит spfile

    SQL> show parameter spfile;

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    spfile				     string	 +DATA/ORCL12/PARAMETERFILE/spf
                             ile.266.887924261

<br/>

    SQL> archive log list;
    Database log mode	       Archive Mode
    Automatic archival	       Enabled
    Archive destination	       USE_DB_RECOVERY_FILE_DEST
    Oldest online log sequence     9
    Next log sequence to archive   11
    Current log sequence	       11

<br/>

    SQL> shutdown immediate;
    SQL> startup mount;
    SQL> alter database noarchivelog;
    SQL> alter database open;

<br/>

    SQL> archive log list;
    Database log mode	       No Archive Mode
    Automatic archival	       Disabled
    Archive destination	       USE_DB_RECOVERY_FILE_DEST
    Oldest online log sequence     9
    Current log sequence	       11


<br/>

    [oracle12@moscow backups]$ rman target /

    RMAN> report schema;

    using target database control file instead of recovery catalog
    Report of database schema for database with db_unique_name ORCL12

    List of Permanent Datafiles
    ===========================
    File Size(MB) Tablespace           RB segs Datafile Name
    ---- -------- -------------------- ------- ------------------------
    1    810      SYSTEM               YES     +DATA/ORCL12/DATAFILE/system.258.887923593
    3    750      SYSAUX               NO      +DATA/ORCL12/DATAFILE/sysaux.257.887923497
    4    135      UNDOTBS1             YES     +DATA/ORCL12/DATAFILE/undotbs1.260.887923711
    6    5        USERS                NO      +DATA/ORCL12/DATAFILE/users.259.887923707

    List of Temporary Files
    =======================
    File Size(MB) Tablespace           Maxsize(MB) Tempfile Name
    ---- -------- -------------------- ----------- --------------------
    1    197      TEMP                 32767       +DATA/ORCL12/TEMPFILE/temp.265.887923853


Вот все файлы данных, кроме временных копируем на раздел для бекапов:


<br/>

### Создание консистентного бекапа.

    SQL> shutdown immediate;

<br/>


    # mkdir -p /backups/ORCL12/DATAFILE/
    # mkdir -p /backups/ORCL12/CONTROLFILE/
    # mkdir -p /backups/ORCL12/PARAMETERFILE/
    # chown -R oracle12 /backups/

    # su - oracle12

    $ export ORACLE_HOME=$GRID_HOME
    $ export ORACLE_SID=+ASM

    $ asmcmd

    ASMCMD> cd +DATA/ORCL12/DATAFILE

<br/>

    ASMCMD> ls
    SYSAUX.257.887923497
    SYSTEM.258.887923593
    UNDOTBS1.260.887923711
    USERS.259.887923707

<br/>

     ASMCMD> cp +DATA/ORCL12/DATAFILE/SYSAUX.257.887923497 /backups/ORCL12/DATAFILE/

     ASMCMD> cp +DATA/ORCL12/DATAFILE/SYSTEM.258.887923593 /backups/ORCL12/DATAFILE/

     ASMCMD> cp +DATA/ORCL12/DATAFILE/UNDOTBS1.260.887923711 /backups/ORCL12/DATAFILE/

     ASMCMD> cp +DATA/ORCL12/DATAFILE/USERS.259.887923707 /backups/ORCL12/DATAFILE/

<br/>


    ASMCMD> ls +DATA/ORCL12/CONTROLFILE/
    Current.261.887923781

<br/>

    ASMCMD> cp +DATA/ORCL12/CONTROLFILE/Current.261.887923781 /backups/ORCL12/CONTROLFILE/


<br/>


    ASMCMD> ls +DATA/ORCL12/PARAMETERFILE/
    spfile.266.887924261


<br/>

    ASMCMD> cp +DATA/ORCL12/PARAMETERFILE/spfile.266.887924261 /backups/ORCL12/PARAMETERFILE/


Восстановление опишу позднее.
Нужно будет создавать TEMP Datafile с таблиыным пространством TEMP, редологи.
