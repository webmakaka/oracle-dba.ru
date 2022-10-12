---
layout: page
title: Создание standby redologs на primary
description: Создание standby redologs на primary
keywords: Oracle DataBase 12.1, Centos 6.7, DataGuard
permalink: /database/installation/distributed/dataguard/linux/6.7/oracle/12.1/standby-redologs-on-primary-instance/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание standby redologs на primary

<br/>

A standby redo log is required for the maximum protection and maximum availability modes and the LGWR ASYNC transport mode is recommended for all databases. Data Guard can recover and apply more redo data from a standby redo log than from archived redo log files alone.

Написано в статье на habrahabr

> Standby redo logs нужны только на standby базе для записи данных, сохраняемых в redo logs на основной базе. На основной базе они нам понадобятся, если мы будем переключать ее в режим standby и при этом использовать real-time apply redo. Файлы standby redo logs должны быть такого же размера как и online redo logs.

При этом в инструкциях обычно, делают на primary, а далее при создании дубликата они создаются и на Standby экземпляре. По-видимому для того, чтобы можно было без лишних манипуляций переключиться с одной базы на другую.

<br/>

### НА Primary

```
SQL> select max (bytes), count (1) from v$log;

MAX(BYTES)   COUNT(1)
---------- ----------
    52428800	    3
```

<br/>

```
$ cd ~
$ . asm.sh
```

<br/>

```
$ asmcmd
ASMCMD> mkdir +DATA/MASTER/STANDBYLOGS/
ASMCMD> mkdir +ARCH/MASTER/STANDBYLOGS/
ASMCMD> exit
```

<br/>

```
$ source ~/.bash_profile
```

<br/>

```
$ sqlplus / as sysdba
```

<br/>

```
$ alter system set standby_file_management=manual scope=both;
```

<br/>

Количество должно быть на 1 больше, чем в primary обычных редолог групп (смотри первый запрос).
ХЗ почему, потом покопаюсь, хотя врятли.

<!--

	SQL>
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 '+DATA/MASTER/STANDBYLOG/stby_4.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 '+DATA/MASTER/STANDBYLOG/stby_5.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 '+DATA/MASTER/STANDBYLOG/stby_6.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 '+DATA/MASTER/STANDBYLOG/stby_7.log' SIZE 52428800;

-->

```
SQL>
ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 ('+ARCH/MASTER/STANDBYLOGS/stby_4.log', '+DATA/MASTER/STANDBYLOG/stby_4.log') SIZE 52428800;
ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 ('+ARCH/MASTER/STANDBYLOGS/stby_5.log', '+DATA/MASTER/STANDBYLOG/stby_5.log') SIZE 52428800;
ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 ('+ARCH/MASTER/STANDBYLOGS/stby_6.log', '+DATA/MASTER/STANDBYLOG/stby_6.log') SIZE 52428800;
ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 ('+ARCH/MASTER/STANDBYLOGS/stby_7.log', '+DATA/MASTER/STANDBYLOG/stby_7.log') SIZE 52428800;
```

<br/>

```
SQL> alter system set standby_file_management=auto scope=both;
```

<br/>

// Какую-то полезную информацию можно посмотреть в представлении v\$standby_log.

```
show parameter standby_file_management

NAME				     TYPE	 VALUE
------------------------------------ ----------- ------------------------------
standby_file_management 	     string	 AUTO
```

<br/>

```
SQL> select group#,status,bytes/1024/1024 mb from v$standby_log;

    GROUP# STATUS	      MB
---------- ---------- ----------
        4 UNASSIGNED	      50
        5 UNASSIGNED	      50
        6 UNASSIGNED	      50
        7 UNASSIGNED	      50

SQL> select TYPE, MEMBER from v$logfile where TYPE='STANDBY';
```
