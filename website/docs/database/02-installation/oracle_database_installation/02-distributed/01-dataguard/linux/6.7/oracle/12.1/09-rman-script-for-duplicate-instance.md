---
layout: page
title:  Создание rman скрипта для дупликата и его выполнение
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-script-for-duplicate-instance/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Создание rman скрипта для дупликата и его выполнение



### На Primary

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

fal_server - fetch archive log

<br/>

	$ rman CHECKSYNTAX @rmanscript.rman


Поехали:

	$ rman target sys/manager@primary_orcl auxiliary sys/manager@standby_orcl @rmanscript.rman

<br/>

	***
	Finished Duplicate Db at 11-AUG-15
	released channel: prmy1
	released channel: stby

	Recovery Manager complete.
