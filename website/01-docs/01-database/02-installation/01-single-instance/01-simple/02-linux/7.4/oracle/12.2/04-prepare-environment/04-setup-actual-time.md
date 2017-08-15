---
layout: page
title: Oracle DataBase 12.2 - Oracle Linux 7.4 - Настройка сервисов отвечающих за синхронизацию времени
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/setup-actual-time/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>


# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>: Настройка сервисов отвечающих за синхронизацию времени



=============================================

Пока не стал настраивать !!!!

=============================================


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
