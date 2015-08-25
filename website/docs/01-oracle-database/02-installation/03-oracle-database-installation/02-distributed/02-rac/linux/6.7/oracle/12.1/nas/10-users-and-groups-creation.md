---
layout: page
title: Создание пользователя oracle12 и административных групп
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/users-and-groups-creation/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Создание пользователя oracle12 и административных групп

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


Создаем пользователя oracle12, сообщаем, что он будет членом групп dba и oinstall и домашним каталогом у него будет /home/oracle12

	# useradd -g oinstall -G dba,oper -d /home/oracle12 oracle12

Устанавливаем пароль для пользователе oracle12

	# passwd oracle12
