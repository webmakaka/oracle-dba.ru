---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Инсталляция Database Software
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/oracle-database-software-installation/
---


# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Инсталляция Database Software


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
	</tr>
</table>


<br/>

	$ cd /tmp/oracle/12.1/database

Чтобы не набирать ORACLE_HOME в окне, выполните команду

	$ export ORACLE_HOME=/u01/app/oracle/product/rac/12.1

Определите системную переменную DISPLAY следующим образом.

	$ export DISPLAY=192.168.1.5:0.0

<br/>

	$ ./runInstaller


<br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_01.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>


<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_02.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_03.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_04.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>


<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_05.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_06.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_07.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>


<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_08.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_09.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_10.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_11.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_12.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_13.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>


<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1,rac2</strong></span></td>
	</tr>
</table>

	# /u01/app/oracle/product/rac/12.1/root.sh


<br/>

<img src="http://img.oradba.net/images/docs/01-oracle-database/02-installation/03-oracle-database-installation/02-distributed/02-rac/linux/6.7/oracle/12.1/02-iscsi-asm/03-oracle-database-software-installation/oracle-database-software-installation_14.png" border="0" alt="Oracle RAC installation ISCSI ASM"><br/><br/>
