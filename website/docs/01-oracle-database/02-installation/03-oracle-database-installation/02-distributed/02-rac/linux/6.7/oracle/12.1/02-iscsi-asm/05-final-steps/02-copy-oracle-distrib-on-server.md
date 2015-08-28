---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Копирование дистрибутивов базы данных на сервер
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/copy-oracle-distrib-on-server/
---


# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Копирование дистрибутивов базы данных на сервер



<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
	</tr>
</table>



<br/>


Войдите в систему пользователем, от имени которого будет будет происходить инсталляция базы данных.

	# su - oracle12


Скопируйте дистрибутивы Oracle во временный каталог /tmp/oracle/12.1/

	$ cd /tmp/oracle/12.1/

<br/>

	$ ls
	linuxamd64_12102_database_1of2.zip  linuxamd64_12102_grid_1of2.zip
	linuxamd64_12102_database_2of2.zip  linuxamd64_12102_grid_2of2.zip


Разархивируем Grid

	$ unzip linuxamd64_12102_grid_1of2.zip; unzip linuxamd64_12102_grid_2of2.zip


Разархивируем DataBase

	$ unzip linuxamd64_12102_database_1of2.zip; unzip linuxamd64_12102_database_2of2.zip
