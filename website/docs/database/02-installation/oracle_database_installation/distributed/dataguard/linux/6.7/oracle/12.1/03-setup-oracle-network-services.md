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
						(GLOBAL_DBNAME=orcl)
						(ORACLE_HOME=/u01/oracle/database/12.1)
						(SID_NAME=orcl)
						)
				)

<br/>

	$ lsnrctl stop
	$ lsnrctl start


<br/>

**С обоих серверов должен проходить tnsping**:

	$ tnsping primary_orcl
	$ tnsping standby_orcl

Должно быть OK.
