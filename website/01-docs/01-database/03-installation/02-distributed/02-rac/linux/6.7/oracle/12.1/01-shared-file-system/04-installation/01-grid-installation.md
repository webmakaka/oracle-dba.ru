---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Инсталляция Grid
description: Oracle RAC 12.1 SHARED FILE SYSTEM - Инсталляция Grid
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, SHARED FILE SYSTEM
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/grid-installation/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Инсталляция Grid

<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
	</tr>
</table>

Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

    # su - oracle12

<br/>

    $ cd /tmp/oracle/12.1/grid

Чтобы не набирать путь установки grid в окне, выполните команду

    $ export ORACLE_HOME=/u01/app/grid/12.1

Определите системную переменную DISPLAY следующим образом.

    $ export DISPLAY=192.168.1.5:0.0

В данном случае 192.168.1.5 - ip адрес компьютера, с которого происходит процесс управления установкой.

<br/>

    $ ./runInstaller

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_01.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_02.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_03.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_04.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_05.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_06.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_07.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_08.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_09.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_10.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_11.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_12.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_13.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_14.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_15.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_16.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_17.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_18.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_19.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_20.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_21.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_22.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>

<img src="https://img.oracledba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/01-shared-file-system/01-grid-installation/grid-installation_23.png" border="0" alt="Oracle RAC installation Shared File System"><br/><br/>
