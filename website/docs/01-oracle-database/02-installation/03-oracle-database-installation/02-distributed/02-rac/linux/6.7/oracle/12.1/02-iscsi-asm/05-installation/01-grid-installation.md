---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Инсталляция Grid
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/grid-installation/
---



# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Инсталляция Grid


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



	unset ORACLE_HOME


Определите системную переменную DISPLAY следующим образом.

	$ export DISPLAY=192.168.1.5:0.0



В данном случае 192.168.1.5 - ip адрес компьютера, с которого происходит процесс управления установкой.  


<br/>

	$ ./runInstaller


СКОРО
