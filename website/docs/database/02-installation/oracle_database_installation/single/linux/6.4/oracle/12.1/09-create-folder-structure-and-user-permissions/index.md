---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /oracle-database-installation/linux/6.4/oracle/12.1/create-folder-structure-and-user-permissions/
---

# <a href="/oracle-database-installation/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Создание структуры каталогов и назначение необходимых прав


	# mkdir -p /u01/oracle/database/12.1
	# chown -R oracle:dba /u01/oracle
	# chmod -R 775 /u01/oracle/database/12.1


	# mkdir -p /u01/oraInventory
	# chown -R oracle:oinstall /u01/oraInventory
	# chmod -R 775 /u01/oraInventory


	# mkdir -p /u02/oracle/oradata
	# chown -R oracle:dba /u02/oracle/oradata
	# chmod -R 775 /u02/oracle/oradata

	# mkdir -p /u03/oracle/oradata
	# chown -R oracle:dba /u03/oracle/oradata
	# chmod -R 775 /u03/oracle/oradata

	# mkdir -p /u03/oracle/oradata/orcl/backups
	# chown -R oracle:dba /u03/oracle/oradata
	# chmod -R 775 /u03/oracle/oradata
