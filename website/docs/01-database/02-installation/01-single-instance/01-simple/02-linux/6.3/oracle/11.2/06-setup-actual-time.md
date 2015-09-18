---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/12.1/setup-actual-time/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/12.1/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Настройка актуального времени


Указать доступные ntp сервера

	# vi /etc/ntp.conf


Например:

	server 0.rhel.pool.ntp.org
	server 1.rhel.pool.ntp.org
	server 2.rhel.pool.ntp.org


Внесите изменения в файл параметров ntpd

	# vi /etc/sysconfig/ntpd

замените

	# Drop root to id 'ntp:ntp' by default.
	OPTIONS="-u ntp:ntp -p /var/run/ntpd.pid"


на

	# Drop root to id 'ntp:ntp' by default.
	# OPTIONS="-u ntp:ntp -p /var/run/ntpd.pid"
	OPTIONS="-x -u ntp:ntp -p /var/run/ntpd.pid"

<br/>

	# service ntpd restart
