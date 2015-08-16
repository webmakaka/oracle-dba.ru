---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.3/oracle/11.2/create-folder-structure-and-user-permissions/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Создание структуры каталогов и назначение необходимых прав



	# mkdir -p /u01/oracle/database/11.2
	# chown -R oracle11:dba /u01/oracle
	# chmod -R 775 /u01/oracle/database/11.2


	# mkdir -p /u01/oraInventory
	# chown -R oracle11:oinstall /u01/oraInventory
	# chmod -R 775 /u01/oraInventory


	# mkdir -p /u02/oradata
	# chown -R oracle11:oinstall /u02/oradata
	# chmod -R 775 /u02/oradata

	# mkdir -p /u03/oradata
	# chown -R oracle11:oinstall /u03/oradata
	# chmod -R 775 /u03/oradata


	# mkdir -p /u03/orabackups
	# chown -R oracle11:oinstall /u03/orabackups
	# chmod -R 775 /u03/orabackups  
