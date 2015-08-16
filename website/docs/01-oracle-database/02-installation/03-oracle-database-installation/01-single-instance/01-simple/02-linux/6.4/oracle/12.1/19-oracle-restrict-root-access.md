---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/oracle-restrict-root-access/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>: Запретить удаленное подключение к сереверу баз данных пользователем root


Запрет входа root по SSH


	# vi /etc/ssh/sshd_config

Нужно


	#PermitRootLogin yes

заменить на


	PermitRootLogin no


<br/>

	# service sshd restart
