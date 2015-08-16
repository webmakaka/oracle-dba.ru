---
layout: page
title: Инсталляция Oracle DataBase 12c Release 1 x86 64 bit в операционной системе Oracle Linux 6.4 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/setup-actual-time/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.4/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.4]</a>:  Настройка актуального времени




Указать доступные ntp сервера


	# vi /etc/ntp.conf


Например:

server 0.rhel.pool.ntp.org<br/>
server 1.rhel.pool.ntp.org<br/>
server 2.rhel.pool.ntp.org<br/>


<br/><br/>
Нужно внести изменения в файл параметров ntpd

	# vi /etc/sysconfig/ntpd


заменить

	# Drop root to id 'ntp:ntp' by default.
	OPTIONS="-u ntp:ntp -p /var/run/ntpd.pid"


на

	# Drop root to id 'ntp:ntp' by default.
	# OPTIONS="-u ntp:ntp -p /var/run/ntpd.pid"
	OPTIONS="-x -u ntp:ntp -p /var/run/ntpd.pid"



<br/>

	# service ntpd restart
