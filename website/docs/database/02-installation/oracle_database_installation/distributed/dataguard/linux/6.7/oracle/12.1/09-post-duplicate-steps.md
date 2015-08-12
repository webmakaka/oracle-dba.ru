---
layout: page
title:  Шаги, выполняемые после создания дупликата
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Шаги, выполняемые после создания дупликата


### Primary


	SQL> show parameter arch


	# SQL> alter system set log_archive_dest_1='LOCATION=+ARCH VALID_FOR=(all_logfiles,all_roles) DB_UNIQUE_NAME=orcl' scope=both;

	SQL> alter system set log_archive_dest_2='service=standby LGWR ASYNC NOAFFIRM NET_TIMEOUT=30 valid_for=(ONLINE_LOGFILE,PRIMARY_ROLE) db_unique_name=standby';


	SQL> alter system set LOG_ARCHIVE_CONFIG='DG_CONFIG=(orcl, standby)' scope=both;


	SQL> show parameter log_archive_dest_state_1


	SQL> alter system set log_archive_dest_state_2=DEFER scope=both;

	# SQL> alter system set standby_archive_dest='+ARCH' scope=both;

	SQL> alter system set standby_file_management= AUTO scope=both;

	SQL> alter system set fal_server = orcl scope=both;

	SQL> alter system set fal_client = standby scope=both;

	SQL> show parameter remote_login_passwordfile


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
