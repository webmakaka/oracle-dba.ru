---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Настройка сервисов отвечающих за синхронизацию времени
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-actual-time/
---

# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Настройка сервисов отвечающих за синхронизацию времени

<br/>


<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);"><strong>Настройка времени</strong></span>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2, storage</strong></span></td>
</tr>
</table>



Внесите изменения в файл параметров ntpd

    # vi /etc/sysconfig/ntpd

замените

    # Drop root to id 'ntp:ntp' by default.
    OPTIONS="-u ntp:ntp -p /var/run/ntpd.pid -g"

на

	# Drop root to id 'ntp:ntp' by default.
	# OPTIONS="-u ntp:ntp -p /var/run/ntpd.pid -g"
	OPTIONS="-x -u ntp:ntp -p /var/run/ntpd.pid -g"

<br/>


	# chkconfig --level 345 ntpd on
	# service ntpd restart



<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
</tr>
</table>


	# cd /etc
	# cp ntp.conf ntp.conf.bak

	# vi ntp.conf

Оставляю только:

	server rac1-priv-storage
	restrict rac1-priv-storage mask 255.255.255.255 nomodify notrap noquery

<br/>

	# service ntpd restart


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac2</strong></span></td>
</tr>
</table>


	# cd /etc
	# cp ntp.conf ntp.conf.bak

	# vi ntp.conf

	Оставляю только:

	server rac2-priv-storage
	restrict rac2-priv-storage mask 255.255.255.255 nomodify notrap noquery

	<br/>

	# service ntpd restart


Проверка:

	# ntpq -pn
	# ntpq -c peers


	# ntpq -p
	     remote           refid      st t when poll reach   delay   offset  jitter
	==============================================================================
	 rac1-priv-stora .INIT.          16 u    -   64    0    0.000    0.000   0.000
