---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/oracle-instance-creation/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Создание экземпляра (instance) базы данных

<br/>

	$ dbca



<br/><br/>


<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_01.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_02.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_03.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_04.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_05.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_06.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_07.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_08.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_09.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_10.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_11.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_12.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_13.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_14.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_15.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_16.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_17.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_18.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_19.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_20.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_21.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_instance_installation_22.PNG" border="0" alt="Oracle RAC installation"><br/><br/>



	$ sqlplus / as sysdba

	SQL*Plus: Release 11.2.0.3.0 Production on Fri May 25 16:20:47 2012

	Copyright (c) 1982, 2011, Oracle.  All rights reserved.


	Connected to:
	Oracle Database 11g Enterprise Edition Release 11.2.0.3.0 - 64bit Production
	With the Partitioning, Real Application Clusters, Automatic Storage Management, OLAP,
	Data Mining and Real Application Testing options

<br/>

	SQL> select status from v$instance;

<br/>

	STATUS
	------------------------------------
	OPEN

<br/>

	col  INST_NUMBER format 5;
	col  INST_NAME format a30;

<br/>

	SELECT * FROM v$active_instances;

<br/>

	INST_NUMBER INST_NAME
	----------- ------------------------------
	          1 node1.localdomain:racnode1
	          2 node2.localdomain:racnode2


<br/><br/>

<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_installation_completed_01.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_installation_completed_02.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_installation_completed_03.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
