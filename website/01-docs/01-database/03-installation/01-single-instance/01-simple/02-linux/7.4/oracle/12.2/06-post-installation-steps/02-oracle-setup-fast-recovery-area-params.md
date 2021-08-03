---
layout: page
title: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4 - Задание параметров FAST RECOVERY AREA
description: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4 - Задание параметров FAST RECOVERY AREA
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, fast recovery area, FRA
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/oracle-setup-fast-recovery-area-params/
---

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Задание параметров FAST RECOVERY AREA

<br/>

Fast Recovery Area (FRA) - это пространство для резервных копий базы данных и файлов архивных журналов (если включен рехим создания архивов redo журналов). Необходимо следить за тем, чтобы у базы данных оставалось место для записи в него своих данных. При необходимости, его можно увеличивать и/или очищать от устаревших данных. Чистить можно только средствами RMAN.

<br/>

    $ sqlplus / as sysdba

<br/>

    SQL> alter system set db_recovery_file_dest_size="20G";

<br/>

    SQL> alter system set db_recovery_file_dest="/u03/oracle/oradata/12.2/orcl12/backups";

<br/>

    SQL> show parameter db_recovery;

<br/>

    SQL> show parameter db_recovery;

    NAME				     TYPE	 VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest		     string	 /u03/oracle/oradata/12.2/orcl12/backups
    db_recovery_file_dest_size	     big integer 20G

<br/>

    SQL> exit
