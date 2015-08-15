---
layout: page
title:  Создание standby redologs на primary
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/standby-redologs-on-primary-instance/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание standby redologs на primary


A standby redo log is required for the maximum protection and maximum availability modes and the LGWR ASYNC transport mode is recommended for all databases. Data Guard can recover and apply more redo data from a standby redo log than from archived redo log files alone.


Написано в статье на habrahabr

> Standby redo logs нужны только на standby базе для записи данных, сохраняемых в redo logs на основной базе. На основной базе они нам понадобятся, если мы будем переключать ее в режим standby и при этом использовать real-time apply redo. Файлы standby redo logs должны быть такого же размера как и online redo logs.


При этом в других инструкциях, как раз делают на primary.<br/>
Я давно делал по инструкции на сайте oracle на primary. В последний раз использовал документ, человека который по всей видимости читал профессиональную литературу.


<br/>

### НА Primary


	SQL> select max (bytes), count (1) from v$log;

	MAX(BYTES)   COUNT(1)
	---------- ----------
	  52428800	    3


<br/>

	$ cd ~
	$ . asm.sh

<br/>

	$ asmcmd
	ASMCMD> mkdir +DATA/MASTER/STANDBYLOG/
	ASMCMD> exit


<br/>


	$ source ~/.bash_profile

<br/>

	$ sqlplus / as sysdba

<br/>

	$ alter system set standby_file_management=manual scope=both;

<br/>

Количество должно быть на 1 больше, чем в primary обычных редолог групп (смотри первый запрос).
ХЗ почему, потом покопаюсь, хотя врятли.

	SQL>
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 '+DATA/MASTER/STANDBYLOG/stby_4.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 '+DATA/MASTER/STANDBYLOG/stby_5.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 '+DATA/MASTER/STANDBYLOG/stby_6.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 '+DATA/MASTER/STANDBYLOG/stby_7.log' SIZE 52428800;

<br/>

	SQL> alter system set standby_file_management=auto scope=both;


<br/>


// Какую-то полезную информацию можно посмотреть в представлении v$standby_log.


	SQL> select LAST_CHANGE#, STATUS from V$STANDBY_LOG;

	LAST_CHANGE# STATUS
	------------ ----------
		     UNASSIGNED
		     UNASSIGNED
		     UNASSIGNED
		     UNASSIGNED
