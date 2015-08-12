---
layout: page
title: Настройка сетевых служб Oracle для создания standby дупликата
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/setup-oracle-network-services/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Настройка сетевых служб Oracle для создания standby дупликата


### Следующие шаги выполняются на Primary и Standby


	$ cd /u01/oracle/database/12.1/network/admin

<br/>

	$ vi tnsnames.ora

<br/>

	***

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



<br/>

### На Standby нужно еще создать listener


	$ vi listener.ora

<br/>

	LISTENER =
	(ADDRESS_LIST=
			(ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521))
			(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))

	SID_LIST_LISTENER=
				(SID_LIST=
						(SID_DESC=
						(GLOBAL_DBNAME=orcl12)
						(ORACLE_HOME=/u01/oracle/database/12.1)
						(SID_NAME=orcl12)
						)
				)

<br/>

	$ lsnrctl stop

<br/>	

	$ lsnrctl start

	LSNRCTL for Linux: Version 12.1.0.2.0 - Production on 12-AUG-2015 12:21:15

	Copyright (c) 1991, 2014, Oracle.  All rights reserved.

	Starting /u01/oracle/database/12.1/bin/tnslsnr: please wait...

	TNSLSNR for Linux: Version 12.1.0.2.0 - Production
	System parameter file is /u01/oracle/database/12.1/network/admin/listener.ora
	Log messages written to /u01/oracle/diag/tnslsnr/piter/listener/alert/log.xml
	Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521)))
	Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))

	Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521))
	STATUS of the LISTENER
	------------------------
	Alias                     LISTENER
	Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
	Start Date                12-AUG-2015 12:21:15
	Uptime                    0 days 0 hr. 0 min. 0 sec
	Trace Level               off
	Security                  ON: Local OS Authentication
	SNMP                      OFF
	Listener Parameter File   /u01/oracle/database/12.1/network/admin/listener.ora
	Listener Log File         /u01/oracle/diag/tnslsnr/piter/listener/alert/log.xml
	Listening Endpoints Summary...
	  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=piter.localdomain)(PORT=1521)))
	  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=extproc)))
	Services Summary...
	Service "orcl12" has 1 instance(s).
	  Instance "orcl12", status UNKNOWN, has 1 handler(s) for this service...
	The command completed successfully



Как бы еще файл с описанием listener, в каталог с grid засунуть....


<br/>

**С обоих серверов должен проходить tnsping**:

	$ tnsping primary_orcl
	$ tnsping standby_orcl

Должно быть OK.
