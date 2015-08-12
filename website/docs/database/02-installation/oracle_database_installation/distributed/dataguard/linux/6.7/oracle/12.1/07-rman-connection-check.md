---
layout: page
title:  Проверка подключения RMAN к обоим Instance
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/rman-connection-check/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Проверка подключения RMAN к обоим Instance


### Primary и StandBy

	$ rman target sys/manager@primary_orcl

manager - мой пароль, созданный при инсталляции базы данных

	$ rman target sys/manager@standby_orcl


<br/>

### Primary


	$ rman target sys/manager@primary_orcl auxiliary sys/manager@standby_orcl

	Recovery Manager: Release 12.1.0.2.0 - Production on Tue Aug 11 07:02:50 2015

	Copyright (c) 1982, 2014, Oracle and/or its affiliates.  All rights reserved.

	connected to target database: ORCL (DBID=1415171842)
	connected to auxiliary database: ORCL (not mounted)



	
