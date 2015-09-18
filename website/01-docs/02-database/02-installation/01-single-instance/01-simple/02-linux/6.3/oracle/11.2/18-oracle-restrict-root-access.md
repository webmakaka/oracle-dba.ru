---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/12.1/oracle-restrict-root-access/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/12.1/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Запретить удаленное подключение к сереверу баз данных пользователем root:


<br/>

	# vi /etc/ssh/sshd_config


Нужно

	#PermitRootLogin yes

<br/>

заменить на

	PermitRootLogin no

<br/>

	# service sshd restart
