---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Создание структуры каталогов и назначение необходимых прав
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/create-folder-structure-and-user-permissions/
---


# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Создание структуры каталогов и назначение необходимых прав



<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
	</tr>
</table>


Необходимо выполнить на каждом из узлов кластера:

Довольно неудобное расположение каталогов, обусловлено тем, что в разных каталогах, необходим
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
