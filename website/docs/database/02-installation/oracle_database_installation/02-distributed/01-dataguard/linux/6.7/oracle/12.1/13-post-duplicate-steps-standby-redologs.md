---
layout: page
title:  Создание standby redologs
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-standby-redologs/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание standby redologs



### НА Standby

Повторяем тоже самое на standby

	$ cd ~
	$ . asm.sh


<br/>

	$ asmcmd
	ASMCMD> mkdir +DATA/SLAVE/
	ASMCMD> mkdir +DATA/SLAVE/STANDBYLOG/
	ASMCMD> exit

<br/>

	$ source ~/.bash_profile


<br/>


	$ sqlplus / as sysdba

<br/>

	SQL> alter system set standby_file_management=manual scope=both;


Количество должно быть на 1 больше, чем в primary обычных редолог групп (смотри первый запрос). ХЗ почему, потом покопаюсь, хотя врятли.


	SQL>
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 '+DATA/SLAVE/STANDBYLOG/stby_4.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 '+DATA/SLAVE/STANDBYLOG/stby_5.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 '+DATA/SLAVE/STANDBYLOG/stby_6.log' SIZE 52428800;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 '+DATA/SLAVE/STANDBYLOG/stby_7.log' SIZE 52428800;

<br/>

	SQL> alter system set standby_file_management=auto scope=both;
