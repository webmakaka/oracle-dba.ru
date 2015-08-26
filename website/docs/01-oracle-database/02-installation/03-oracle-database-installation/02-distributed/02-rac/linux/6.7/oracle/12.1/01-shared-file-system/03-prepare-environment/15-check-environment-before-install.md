---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Проверка конфигурации кластера перед инсталляцией RAC
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/check-environment-before-install/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Проверка конфигурации кластера перед инсталляцией RAC



<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
	</tr>
</table>



<br/>

	# cd /tmp/oracle/12.1/database/rpm
	# rpm -Uvh cvuqdisk-1.0.9-1.rpm

<br/>

	# su - oracle12
	$ cd /tmp/oracle/12.1/grid


<br/>

	$ ./runcluvfy.sh stage -pre crsinst -n rac1,rac2 -r 12.1

Если возникли ошибки, можно получить лог с более детальным отчетом о возникших проблемах:

	$ ./runcluvfy.sh stage -pre crsinst -n rac1,rac2 -r 12.1  -verbose


<br/>

Получил ошибку:

	Check: Swap space
	  Node Name     Available                 Required                  Status
	  ------------  ------------------------  ------------------------  ----------
	  rac2          4GB (4194300.0KB)         4.1026GB (4301836.0KB)    failed
	  rac1          4GB (4194300.0KB)         4.1026GB (4301836.0KB)    failed
	Result: Swap space check failed




<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
	</tr>
</table>


	# dd if=/dev/zero of=/root/swapfile count=1024 bs=4718592

	# mkswap -f /root/swapfile

	# swapon /root/swapfile

	# swapon -s
	Filename				Type		Size	Used	Priority
	/dev/dm-1                               partition	4194300	0	-1
	/root/swapfile                          file		4301832	0	-2


	# vi /etc/fstab

Комментирую:

	# /dev/mapper/VolGroup-lv_swap swap                    swap    defaults        0 0


Добавляю:

	/root/swapfile      swap                    swap    defaults        0 0



<br/>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
	</tr>
</table>

	# su - oracle12
	$ cd /tmp/oracle/12.1/grid
	$ ./runcluvfy.sh stage -pre crsinst -n rac1,rac2 -r 12.1

	***
	Pre-check for cluster services setup was successful.



Так как я работаю с виртуальными машинами, то считаю, что нужно сохраниться (создать snapshot).
