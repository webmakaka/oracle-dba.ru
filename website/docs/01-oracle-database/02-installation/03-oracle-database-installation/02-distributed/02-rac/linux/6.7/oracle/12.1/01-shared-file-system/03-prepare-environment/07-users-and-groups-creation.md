---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Создание пользователя oracle12 и административных групп
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nfs/users-and-groups-creation/
---



# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Создание пользователя oracle12 и административных групп


<br/>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">


<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2, storage</strong></span></td>
</tr>

</table>


Перед тем как вносить изменения в конфигурационные скрипты, следует предварительно создать их резервные копии:

	# {
	cp /etc/sysctl.conf /etc/sysctl.conf.bkp
	cp /etc/security/limits.conf /etc/security/limits.conf.bkp
	cp /etc/pam.d/login /etc/pam.d/login.bkp
	cp /etc/profile /etc/profile.bkp
	}

Создаем группы:

	# groupadd -g 1000 oinstall
	# groupadd -g 1001 dba
	# groupadd -g 1002 oper


Вроде как мы не используем здесь ASM, но группы почему-то требуются.

	OSASM Group

		# groupadd -g 1003 asmadmin

	OSDBA Group

		# groupadd -g 1004 asmdba

	OSOPER Group

		# groupadd -g 1005 asmoper


Создаем пользователя oracle12, сообщаем, что он будет членом групп dba и oinstall и домашним каталогом у него будет /home/oracle12

	# useradd -g oinstall -G dba,oper,asmadmin,asmdba,asmoper -d /home/oracle12 oracle12

Устанавливаем пароль для пользователе oracle12

	# passwd oracle12
