---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/create-folder-structure-and-user-permissions/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Создание структуры каталогов и назначение необходимых прав


<br/>


Необходимо выполнить на каждом из узлов кластера:

Давольно неудобное расположение каталогов, обусловлено тем, что в разных каталогах, необходим
разный набор прав на каталоги. + при внесении изменений возможна ругань при инсталляции.


	# mkdir -p /u01/app/oraInventory
	# chown -R oracle12:oinstall /u01/app/oraInventory
	# chmod -R 775 /u01/app/oraInventory

<br/>

	# mkdir -p /u01/app/grid/12.1
	# chown -R oracle12:oinstall /u01/app/grid/12.1
	# chmod -R 775 /u01/app/grid/12.1

<br/>

	# mkdir -p /u01/app/oracle/product/rac/12.1
	# chown -R oracle12:oinstall /u01/app/oracle
	# chmod -R 775 /u01/app/oracle
