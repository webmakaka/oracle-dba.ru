---
layout: page
title: Oracle DataBase 12c - Linux - Запретить удаленное подключение к серверу баз данных пользователем root
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/oracle-restrict-root-access/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Запретить удаленное подключение к серверу баз данных пользователем root


Запрет входа root по SSH


	# vi /etc/ssh/sshd_config

Нужно


	#PermitRootLogin yes

заменить на


	PermitRootLogin no


<br/>

	# service sshd restart
