---
layout: page
title:  Проверка подключения RMAN к обоим Instance
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/dataguard/linux/6.7/oracle/12.1/rman-connection-check/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Проверка подключения RMAN к обоим Instance



### Primary


manager - мой пароль, созданный при инсталляции базы данных


	$ rman target sys/manager@primary auxiliary sys/manager@standby

	Recovery Manager: Release 12.1.0.2.0 - Production on Thu Aug 13 17:16:07 2015

	Copyright (c) 1982, 2014, Oracle and/or its affiliates.  All rights reserved.

	connected to target database: ORCL12 (DBID=3487298206)
	connected to auxiliary database: ORCL12 (not mounted)


<br/>

### Если не заработало, то можно на Primary и Standby повыполнять отдельно команды:

	$ rman target sys/manager@primary

<br/>

	$ rman target sys/manager@standby
