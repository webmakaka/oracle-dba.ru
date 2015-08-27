---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/check-environment-before-install/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Проверка конфигурации кластера перед инсталляцией RAC


<br/>

Скачайте с сайта oracle последнюю версию «Oracle Cluster Verification Utility»  
http://www.oracle.com/technetwork/database/clustering/downloads/cvu-download-homepage-099973.html



<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Инсталляция cvuqdisk-1.0.9-1.rpm</strong></span>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1,node2</strong></span></td>
	</tr>
</table>


Нужно установить пакет cvuqdisk-1.0.9-1.rpm на всех узлах кластера

Ранее, я скопировал данный пакет на один из серверов linux.  

Забираю их следующей командой:

	# scp marley@192.168.1.5:/mnt/dsk2/_ISO/oracle/linux/cvupack_Linux_x86_64.zip /tmp/

<br/>

	# cd /tmp

<br/>

	# mkdir cvupack
	# mv cvupack_Linux_x86_64.zip ./cvupack
	# cd /tmp/cvupack
	# unzip cvupack_Linux_x86_64.zip

<br/>

	# rpm -Uvh /tmp/cvupack/rpm/cvuqdisk-1.0.9-1.rpm

<br/>

	# chown -R oracle11:oinstall /tmp/cvupack


<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Проверка правильности конфигурации подготовленных узлов кластера</strong></span>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1</strong></span></td>
	</tr>
</table>


	# su - oracle11

<br/>

	$ cd /tmp/cvupack/bin

<br/>

	$ ./cluvfy stage -pre crsinst -n node1,node2

Если возникли ошибки, можно получить лог с более детальным отчетом о возникших проблемах:

	$ ./cluvfy stage -pre crsinst -n node1,node2 -r 11gR2  -verbose > /tmp/log.log

<br/>

	***

	Check: Membership of user "oracle11" in group "oinstall" [as Primary]
	  Node Name         User Exists   Group Exists  User in Group  Primary       Status
	  ----------------  ------------  ------------  ------------  ------------  ------------
	  devsp038          yes           yes           yes           no            failed
	  devsp037          yes           yes           yes           no            failed
	Result: Membership check for user "oracle11" in group "oinstall" [as Primary] failed

	***

<br/>

	$ id
	uid=502(oracle11) gid=500(dba) groups=500(dba),1003(oinstall)


<br/>

	# usermod -g oinstall oracle11
	# usermod -G dba oracle11

<br/>

	# su - oracle11
	$ id
	uid=502(oracle11) gid=1003(oinstall) groups=500(dba),1003(oinstall)


Результатом проверки должна быть следующее сообщение.
Pre-check for cluster services setup was successful.



Интересно следующее, в самой консоли, требуется, чтобы основная группа была dba.

Поэтому:

	# usermod -g dba oracle11
	# usermod -G oinstall oracle11
