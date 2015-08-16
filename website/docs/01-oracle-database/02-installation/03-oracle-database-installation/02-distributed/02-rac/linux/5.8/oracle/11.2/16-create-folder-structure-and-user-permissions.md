---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/create-folder-structure-and-user-permissions/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Создание структуры каталогов и назначение необходимых прав


<br/>


Необходимо выполнить на каждом из узлов кластера:

Давольно неудобное расположение каталогов, обусловлено тем, что в разных каталогах, необходим
разный набор прав на каталоги. + при внесении изменений возможна ругань при инсталляции.


	# mkdir -p /u01/app/oraInventory
	# chown -R oracle11:oinstall /u01/app/oraInventory
	# chmod -R 775 /u01/app/oraInventory

<br/>

	# mkdir -p /u01/app/grid/11.2
	# chown -R oracle11:oinstall /u01/app/grid/11.2
	# chmod -R 775 /u01/app/grid/11.2

<br/>

	# mkdir -p /u01/app/oracle/product/rac/11.2
	# chown -R oracle11:oinstall /u01/app/oracle
	# chmod -R 775 /u01/app/oracle
