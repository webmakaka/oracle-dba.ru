---
layout: page
title:  Шаги, выполняемые после создания дупликата на Primary
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/post-duplicate-steps-on-primary/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Шаги, выполняемые после создания дупликата на Primary


При создании дупликата, мы задали какие-то параметры на standby. Нужно сделать так, чтобы такие же параметры были и на primary.


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
