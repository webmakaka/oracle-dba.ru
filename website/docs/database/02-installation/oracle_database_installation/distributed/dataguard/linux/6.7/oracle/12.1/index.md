---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]:


# В разработке!
# В разработке!
## Помогайте, кому нечем заняться!
# В разработке!
# В разработке!


Для информации:

db_name - одинаковое на узлах  
db_unique_name - должно быть разными на узлах  


<br/>


1) Устанавливаю 2 сервера как здесь:
http://oracle-dba.ru/oracle-database-installation/asm/linux/6.7/oracle/12.1/


На втором не создаю instance. Он будет скопирован с первого.


Primary:  
Hostname: moscow  
Instance: orcl  
IP: 192.168.1.11  

StandBy:  
Hostname: piter  
Instance: orcl  
IP: 192.168.1.12  


Все время забываю, где прописывается hostname сервера

	# vi /etc/sysconfig/network

**После переименования, лучше перезагрузить сервер или каким-то способом применить изменения, или иначе в конфигах будет прописано что-то не то и придется их потом еще и править**


Устанавливаю пакет scp для копирования данных между серверами на обоих узлах

	# yum install -y openssh-clients


<br/>

	# vi /etc/hosts

<br/>

	## Localdomain and Localhost

	127.0.0.1 localhost.localdomain localhost


	## DataBases

	# moscow - primary; piter - standby

	192.168.1.11 moscow.localdomain moscow
	192.168.1.12 piter.localdomain piter


<br/>


	vi /home/oracle12/.bash_profile

<br/>

	#### Oracle Parameters ###########################

		umask 022

		export ORACLE_BASE=/u01/oracle
		export ORACLE_HOME=$ORACLE_BASE/database/12.1

		export GRID_HOME=$ORACLE_BASE/grid/12.1

		export ORACLE_SID=orcl
		export ORACLE_UNQNAME=orcl
		export NLS_LANG=AMERICAN_AMERICA.AL32UTF8

		export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin
		export LD_LIBRARY_PATH=$ORACLE_HOME/lib

		alias sqlplus='rlwrap sqlplus'
		alias rman='rlwrap rman'

	#### Oracle Parameters ###########################


### Primary

### ENABLE ARCHIVELOG


	SQL> archive log list;
	Database log mode	       No Archive Mode
	Automatic archival	       Disabled
	Archive destination	       USE_DB_RECOVERY_FILE_DEST
	Oldest online log sequence     8
	Current log sequence	       10

<br/>

	SQL> shutdown immediate;
	SQL> startup mount;
	SQL> alter database archivelog;
	SQL> alter database open;

<br/>

	SQL>  archive log list;
	Database log mode	       Archive Mode
	Automatic archival	       Enabled
	Archive destination	       USE_DB_RECOVERY_FILE_DEST
	Oldest online log sequence     8
	Next log sequence to archive   10
	Current log sequence	       10

<br/>

	SQL> select name, total_mb, free_mb from v$asm_diskgroup;

	NAME				 TOTAL_MB    FREE_MB
	------------------------------ ---------- ----------
	DATA				   245754     241163





### FORCE_LOGGING


	SQL> select force_logging from v$database;

	FORCE_LOGGING
	---------------------------------------
	NO


<br/>

	SQL> alter database force logging;


<br/>

	SQL> select force_logging from v$database;

	FORCE_LOGGING
	---------------------------------------
	YES

================================================================================
================================================================================



// На обоих серверах


	$ cd /u01/oracle/database/12.1/network/admin

<br/>

	$ vi tnsnames.ora

<br/>

	primary_orcl =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = moscow.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = orcl)
	    )
	  )


	standby_orcl =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = piter.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = orcl)
	    )
	  )




// Standby


$ vi listener.ora

<br/>

LISTENER =
(ADDRESS_LIST=
		(ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521))
		(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))

SID_LIST_LISTENER=
			(SID_LIST=
					(SID_DESC=
					(GLOBAL_DBNAME=orcl)
					(ORACLE_HOME=/u01/oracle/database/12.1)
					(SID_NAME=orcl)
					)
			)



	$ lsnrctl stop
	$ lsnrctl start


<br/>

С обоих серверов:

	$ tnsping primary_orcl
	$ tnsping standby_orcl

Должно быть OK.


================================================================================
================================================================================


<br/>

### Passwordfile

	SQL> show parameter remote_login_passwordfile

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	remote_login_passwordfile	     string	 EXCLUSIVE


<br/>

SQL> exit


<br/>

	$ chmod 4640 $ORACLE_HOME/dbs/orapworcl



<br/>

<!--

Зачем-то удалили файл паролей и создали новый. Возможно, чтобы просто показать.

orapwd fiel=orapwdlondon password=oracle entries=5


-->


### Primary

	Копирую файл паролей

	$ scp $ORACLE_HOME/dbs/orapworcl oracle12@piter:$ORACLE_HOME/dbs/orapworcl



### Standby

	$ chmod 4640 /u01/oracle/database/12.1/dbs/orapworcl

<br/>

	$ cd $ORACLE_HOME/dbs

<br/>

	$ echo DB_NAME=orcl > initorcl.ora

<br/>

	$ sqlplus / as sysdba

<br/>

	SQL> startup nomount pfile=$ORACLE_HOME/dbs/initorcl.ora

<br/>

	SQL> select status from v$instance;

	STATUS
	------------------------------------
	STARTED

=================================================================================
=================================================================================

### Primary и StandBy

	$ rman target sys/manager@primary_orcl

- manager - мой пароль, созданный при инсталляции базы данных


	$ rman target sys/manager@standby_orcl


### Primary


	$ rman target sys/manager@primary_orcl auxiliary sys/manager@standby_orcl

	Recovery Manager: Release 12.1.0.2.0 - Production on Tue Aug 11 07:02:50 2015

	Copyright (c) 1982, 2014, Oracle and/or its affiliates.  All rights reserved.

	connected to target database: ORCL (DBID=1415171842)
	connected to auxiliary database: ORCL (not mounted)


=================================================================================
=================================================================================



# Creation of the standby with Rman Duplicate

Нужно лучше разобраться с параметрами!


На Primary

	SQL> show parameter audit

	NAME				     TYPE	 VALUE
	------------------------------------ ----------- ------------------------------
	audit_file_dest 		     string	 /u01/oracle/admin/orcl/adump
	audit_sys_operations		     boolean	 TRUE
	audit_syslog_level		     string
	audit_trail			     string	 DB
	unified_audit_sga_queue_size	     integer	 1048576


На Standby


	$ mkdir -p /u01/oracle/admin/orcl/adump



На Primary

<br/>

	$ vi rmanscript.rman


<br/>

	run {
	    allocate channel prmy1 type disk;
		allocate auxiliary channel stby type disk;
		duplicate target database for standby from active database spfile
			set db_unique_name='standby'
			set control_files='+DATA/standby/controlfile/control01.ctl'
			set log_archive_max_processes='5'
			set fal_server='orcl'
			set standby_file_management='AUTO'
			set log_archive_config='dg_config=(orcl,standby)'
			# set log_archive_dest_1='+ARCH'
			set log_archive_dest_2='service=orcl LGWR ASYNC NOAFFIRM valid_for=(ONLINE_LOGFILE,PRIMARY_ROLE) db_unique_name=orcl';
	     }

<br/>

fal_server - fatch archive log

<br/>

	$ rman CHECKSYNTAX @rmanscript.rman

<br/>

	$ rman target sys/manager@primary_orcl auxiliary sys/manager@standby_orcl @rmanscript.rman

<br/>

	***
	Finished Duplicate Db at 11-AUG-15
	released channel: prmy1
	released channel: stby

	Recovery Manager complete.




# Post Duplicate Steps


Primary


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


==================

НА Primary


	SQL> select max (bytes), count (1) from v$log;

	MAX(BYTES)   COUNT(1)
	---------- ----------
	  52428800	    3


<br/>

	$ cd ~
	$ . asm.sh


$ asmcmd


ASMCMD> ls
DATA/


ASMCMD> mkdir +DATA/ORCL/STANDBYLOG/

ASMCMD> exit



source ~/.bash_profile

sqlplus / as sysdba

alter system set standby_file_management=manual scope=both;

Количество должно быть на 1 больше, чем в primary обычных логфайлов.


	ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 '+DATA/ORCL/STANDBYLOG/stby_4.log' SIZE 100M;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 '+DATA/ORCL/STANDBYLOG/stby_5.log' SIZE 100M;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 '+DATA/ORCL/STANDBYLOG/stby_6.log' SIZE 100M;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 '+DATA/ORCL/STANDBYLOG/stby_7.log' SIZE 100M;


alter system set standby_file_management=auto scope=both;



==============================


Standby



<br/>

	$ cd ~
	$ . asm.sh


$ asmcmd

ASMCMD> mkdir +DATA/STANDBY/STANDBYLOG/


ASMCMD> exit



source ~/.bash_profile

sqlplus / as sysdba

alter system set standby_file_management=manual scope=both;

Количество должно быть на 1 больше, чем в primary обычных логфайлов.


	ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 '+DATA/STANDBY/STANDBYLOG/stby_4.log' SIZE 100M;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 '+DATA/STANDBY/STANDBYLOG/stby_5.log' SIZE 100M;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 '+DATA/STANDBY/STANDBYLOG/stby_6.log' SIZE 100M;
	ALTER DATABASE ADD STANDBY LOGFILE GROUP 7 '+DATA/STANDBY/STANDBYLOG/stby_7.log' SIZE 100M;


alter system set standby_file_management=auto scope=both;



=================================================
=================================================

PRIMARY

	$ cd /u01/oracle/database/12.1/network/admin
