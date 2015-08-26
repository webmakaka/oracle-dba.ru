---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Создание экземпляра (instance) базы данных
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nfs/oracle-instance-creation/
---


# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Создание экземпляра (instance) базы данных


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
	</tr>
</table>

<br/>

	# mkdir -p /u02/fast_recovery_area
	# chown -R oracle12:dba /u02/fast_recovery_area


	# mkdir -p /u02/oradata
	# chown -R oracle12:dba /u02/oradata

<br/>

	# su - oracle12

<br/>

	$ export DISPLAY=192.168.1.5:0.0

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

	SQL*Plus: Release 12.1.0.2.0 Production on Tue Aug 25 20:08:26 2015

	Copyright (c) 1982, 2014, Oracle.  All rights reserved.


	Connected to:
	Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
	With the Partitioning, Real Application Clusters, OLAP, Advanced Analytics
	and Real Application Testing options


<br/>

	SQL> select status from v$instance;

	STATUS
	------------
	OPEN


<br/>

	SQL> col INST_NUMBER format 5;
	SQL> col INST_NAME format a30;

<br/>

	SQL> SELECT * FROM v$active_instances;

<br/>

	INST_NUMBER INST_NAME			       CON_ID
	----------- ------------------------------ ----------
		  0 rac1.localdomain:rac121		    0


		  0 rac2.localdomain:rac122		    0



<br/>

	https://192.168.1.11:5500/em/
	https://192.168.1.12:5500/em/

	https://rac12-scan:5500/em/




<br/>

<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_installation_completed_01.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_installation_completed_02.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_installation_completed_03.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
