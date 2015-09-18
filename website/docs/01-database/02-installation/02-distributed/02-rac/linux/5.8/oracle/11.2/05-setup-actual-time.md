---
layout: page
title: Oracle RAC 11.2 ISCSI + ASM - Настройка сервисов отвечающих за синхронизацию времени
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/setup-actual-time/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Настройка сервисов отвечающих за синхронизацию времени

<br/>




<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);"><strong>Настройка времени</strong></span>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2, storage</strong></span></td>
</tr>
</table>


Указать доступные ntp сервера

    # vi /etc/ntp.conf

<br/>

    server 0.rhel.pool.ntp.org
    server 1.rhel.pool.ntp.org
    server 2.rhel.pool.ntp.org


<!--
Настраиваем планировщик заданий

Сервера ru.pool.ntp.org выбраны в качестве примера

# crontab -e

# Set the date and time via NTP
*/15 * * * * /usr/sbin/ntpdate 0.ru.pool.ntp.org 1.ru.pool.ntp.org 2.ru.pool.ntp.org 3.ru.pool.ntp.org   > /var/log/time.log


-->

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
