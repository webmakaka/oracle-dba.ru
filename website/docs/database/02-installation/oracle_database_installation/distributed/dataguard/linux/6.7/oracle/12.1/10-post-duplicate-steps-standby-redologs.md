---
layout: page
title:  Создание standby redologs
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-standby-redologs/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание standby redologs



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
	ASMCMD> mkdir +DATA/ORCL/STANDBYLOG/
	ASMCMD> exit


<br/>


	$ source ~/.bash_profile

	$ sqlplus / as sysdba

	$ alter system set standby_file_management=manual scope=both;

Количество должно быть на 1 больше, чем в primary обычных логфайлов.


	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 '+DATA/ORCL/STANDBYLOG/stby_4.log' SIZE 52428800;
	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 '+DATA/ORCL/STANDBYLOG/stby_5.log' SIZE 52428800;
	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 '+DATA/ORCL/STANDBYLOG/stby_6.log' SIZE 52428800;
	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 '+DATA/ORCL/STANDBYLOG/stby_7.log' SIZE 52428800;

<br/>

	SQL> alter system set standby_file_management=auto scope=both;


<br/>

### НА Standby

	$ cd ~
	$ . asm.sh


<br/>

	$ asmcmd
	ASMCMD> mkdir +DATA/STANDBY/STANDBYLOG/
	ASMCMD> exit

<br/>

	$ source ~/.bash_profile


<br/>


	$ sqlplus / as sysdba

	SQL> alter system set standby_file_management=manual scope=both;


Количество должно быть на 1 больше, чем в primary обычных логфайлов.


	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 '+DATA/STANDBY/STANDBYLOG/stby_4.log' SIZE 52428800;
	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 '+DATA/STANDBY/STANDBYLOG/stby_5.log' SIZE 52428800;
	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 '+DATA/STANDBY/STANDBYLOG/stby_6.log' SIZE 52428800;
	SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 '+DATA/STANDBY/STANDBYLOG/stby_7.log' SIZE 52428800;


	SQL> alter system set standby_file_management=auto scope=both;
