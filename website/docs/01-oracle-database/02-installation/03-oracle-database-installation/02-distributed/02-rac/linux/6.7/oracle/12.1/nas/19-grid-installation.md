---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/grid-installation/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Инсталляция Grid


<br/>


Инсталляция ПО Oracle (GRID)


Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12

Выполните команду

	$ id
	uid=500(oracle12) gid=1000(oinstall) groups=1000(oinstall),1001(dba),1002(oper)



<br/>

	$ cd /tmp/oracle/12.1/grid


Определите системную переменную DISPLAY следующим образом.

	$ export DISPLAY=192.168.1.5:0.0


В данном случае 192.168.1.5 - ip адрес компьютера, с которого происходит процесс управления установкой.  

На 192.168.1.5 инсталлирован и стартован Xming


<br/>

	$ ./runInstaller



<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_01.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_02.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_03.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_04.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_05.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_06.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_07.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_08.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_09.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_10.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_11.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_12.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_13.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_14.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_15.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_16.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_17.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_18.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_19.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_20.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_21.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_22.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_23.PNG" border="0" alt="Oracle RAC installation"><br/><br/>
<img src="http://img.oradba.net/img/oracle/database/rac/11.2/rac_grid_installation_24.PNG" border="0" alt="Oracle RAC installation"><br/><br/>


node1


	# /u01/app/oraInventory/orainstRoot.sh

	Changing permissions of /u01/app/oraInventory.
	Adding read,write permissions for group.
	Removing read,write,execute permissions for world.

	Changing groupname of /u01/app/oraInventory to oinstall.
	The execution of the script is complete.


<br/>

	# /u01/app/oraInventory/orainstRoot.sh

	Changing permissions of /u01/app/oraInventory.
	Adding read,write permissions for group.
	Removing read,write,execute permissions for world.

	Changing groupname of /u01/app/oraInventory to oinstall.
	The execution of the script is complete.
	[root@node1 ~]# /u01/app/grid/11.2/root.sh
	Performing root user operation for Oracle 11g

	The following environment variables are set as:
	    ORACLE_OWNER= oracle11
	    ORACLE_HOME=  /u01/app/grid/11.2

	Enter the full pathname of the local bin directory: [/usr/local/bin]:
	   Copying dbhome to /usr/local/bin ...
	   Copying oraenv to /usr/local/bin ...
	   Copying coraenv to /usr/local/bin ...


	Creating /etc/oratab file...
	Entries will be added to the /etc/oratab file as needed by
	Database Configuration Assistant when a database is created
	Finished running generic part of root script.
	Now product-specific root actions will be performed.
	Using configuration parameter file: /u01/app/grid/11.2/crs/install/crsconfig_params
	Creating trace directory
	User ignored Prerequisites during installation
	OLR initialization - successful
	  root wallet
	  root wallet cert
	  root cert export
	  peer wallet
	  profile reader wallet
	  pa wallet
	  peer wallet keys
	  pa wallet keys
	  peer cert request
	  pa cert request
	  peer cert
	  pa cert
	  peer root cert TP
	  profile reader root cert TP
	  pa root cert TP
	  peer pa cert TP
	  pa peer cert TP
	  profile reader pa cert TP
	  profile reader peer cert TP
	  peer user cert
	  pa user cert
	Adding Clusterware entries to inittab
	CRS-2672: Attempting to start 'ora.mdnsd' on 'node1'
	CRS-2676: Start of 'ora.mdnsd' on 'node1' succeeded
	CRS-2672: Attempting to start 'ora.gpnpd' on 'node1'
	CRS-2676: Start of 'ora.gpnpd' on 'node1' succeeded
	CRS-2672: Attempting to start 'ora.cssdmonitor' on 'node1'
	CRS-2672: Attempting to start 'ora.gipcd' on 'node1'
	CRS-2676: Start of 'ora.cssdmonitor' on 'node1' succeeded
	CRS-2676: Start of 'ora.gipcd' on 'node1' succeeded
	CRS-2672: Attempting to start 'ora.cssd' on 'node1'
	CRS-2672: Attempting to start 'ora.diskmon' on 'node1'
	CRS-2676: Start of 'ora.diskmon' on 'node1' succeeded
	CRS-2676: Start of 'ora.cssd' on 'node1' succeeded

	ASM created and started successfully.

	Disk Group DATA created successfully.

	clscfg: -install mode specified
	Successfully accumulated necessary OCR keys.
	Creating OCR keys for user 'root', privgrp 'root'..
	Operation successful.
	CRS-4256: Updating the profile
	Successful addition of voting disk 022a7b578f614f2ebf0a380dc50f7b40.
	Successful addition of voting disk 4cf55b0a2cf14fa1bf182111f8c4794c.
	Successful addition of voting disk 258a94b2d4144f98bf7a4db2084c7d95.
	Successfully replaced voting disk group with +DATA.
	CRS-4256: Updating the profile
	CRS-4266: Voting file(s) successfully replaced
	##  STATE    File Universal Id                File Name Disk group
	--  -----    -----------------                --------- ---------
	 1. ONLINE   022a7b578f614f2ebf0a380dc50f7b40 (ORCL:VOL1) [DATA]
	 2. ONLINE   4cf55b0a2cf14fa1bf182111f8c4794c (ORCL:VOL2) [DATA]
	 3. ONLINE   258a94b2d4144f98bf7a4db2084c7d95 (ORCL:VOL3) [DATA]
	Located 3 voting disk(s).
	CRS-2672: Attempting to start 'ora.asm' on 'node1'
	CRS-2676: Start of 'ora.asm' on 'node1' succeeded
	CRS-2672: Attempting to start 'ora.DATA.dg' on 'node1'
	CRS-2676: Start of 'ora.DATA.dg' on 'node1' succeeded
	CRS-2672: Attempting to start 'ora.registry.acfs' on 'node1'
	CRS-2676: Start of 'ora.registry.acfs' on 'node1' succeeded
	Configure Oracle Grid Infrastructure for a Cluster ... succeeded


node2

	# /u01/app/oraInventory/orainstRoot.sh

	Changing permissions of /u01/app/oraInventory.
	Adding read,write permissions for group.
	Removing read,write,execute permissions for world.

	Changing groupname of /u01/app/oraInventory to oinstall.
	The execution of the script is complete.

<br/>

	# /u01/app/oraInventory/orainstRoot.sh
	Changing permissions of /u01/app/oraInventory.
	Adding read,write permissions for group.
	Removing read,write,execute permissions for world.

	Changing groupname of /u01/app/oraInventory to oinstall.
	The execution of the script is complete.
	You have new mail in /var/spool/mail/root
	[root@node2 ~]# /u01/app/grid/11.2/root.sh
	Performing root user operation for Oracle 11g

	The following environment variables are set as:
	    ORACLE_OWNER= oracle11
	    ORACLE_HOME=  /u01/app/grid/11.2

	Enter the full pathname of the local bin directory: [/usr/local/bin]:
	   Copying dbhome to /usr/local/bin ...
	   Copying oraenv to /usr/local/bin ...
	   Copying coraenv to /usr/local/bin ...


	Creating /etc/oratab file...
	Entries will be added to the /etc/oratab file as needed by
	Database Configuration Assistant when a database is created
	Finished running generic part of root script.
	Now product-specific root actions will be performed.
	Using configuration parameter file: /u01/app/grid/11.2/crs/install/crsconfig_params
	Creating trace directory
	User ignored Prerequisites during installation
	OLR initialization - successful
	Adding Clusterware entries to inittab
	CRS-4402: The CSS daemon was started in exclusive mode but found an active CSS daemon on node node1, number 1, and is terminating
	An active cluster was found during exclusive startup, restarting to join the cluster
	Configure Oracle Grid Infrastructure for a Cluster ... succeeded
