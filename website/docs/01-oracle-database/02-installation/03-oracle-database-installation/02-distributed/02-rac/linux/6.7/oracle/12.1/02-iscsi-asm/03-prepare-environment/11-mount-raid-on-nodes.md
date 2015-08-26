---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Монтирование RAID на узлах кластера
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/mount-raid-on-nodes/
---


# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Монтирование SCSI на узлах кластера


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>



<br/>


<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Настройка правил UDEV, для определения правил присваивания имен импортируемым дискам.</strong></span>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
</tr>

</table>


Рекомендую отказаться от использования правил UDEV.<br/>
В некоторых случаях возникают проблемы при монтированни разделов ASM на других узлах кластера.<br/>
По крайней мере пока я не откючил правила, появлялась ошибка: <br/><br/>

	oracleasm-read-label: Unable to open device "/dev/sdb": No such file or directory


Более того, ядро RedHat с версии 5.8 и 6.x не возвращают идентификатор подмонтированного iSCSI устройства.


Если есть способы обойти, дайте мне знать!


<!--
<pre>

# cp /etc/scsi_id.config /etc/scsi_id.config.bkp
# echo "vendor="NETAPP", model=LUN, options=-g" >> /etc/scsi_id.config

# vi /etc/udev/rules.d/99-static-scsi-names.rules

#----------------------------
# External DISKS
#----------------------------
# SCSI1
KERNEL=="sd*", BUS=="scsi", PROGRAM=="/sbin/scsi_id -g -u -s %p", RESULT=="1IET_00010001", NAME="iscsi_A", OWNER="oracle11", GROUP="dba", MODE="0640"
# SCSI2
KERNEL=="sd*", BUS=="scsi", PROGRAM=="/sbin/scsi_id -g -u -s %p", RESULT=="1IET_00020001", NAME="iscsi_B", OWNER="oracle11", GROUP="dba", MODE="0640"
# SCSI3
KERNEL=="sd*", BUS=="scsi", PROGRAM=="/sbin/scsi_id -g -u -s %p", RESULT=="1IET_00030001", NAME="iscsi_C", OWNER="oracle11", GROUP="dba", MODE="0640"
# SCSI4
KERNEL=="sd*", BUS=="scsi", PROGRAM=="/sbin/scsi_id -g -u -s %p", RESULT=="1IET_00040001", NAME="iscsi_D", OWNER="oracle11", GROUP="dba", MODE="0640"
# SCSI5
KERNEL=="sd*", BUS=="scsi", PROGRAM=="/sbin/scsi_id -g -u -s %p", RESULT=="1IET_00050001", NAME="iscsi_E", OWNER="oracle11", GROUP="dba", MODE="0640"
# SCSI6
KERNEL=="sd*", BUS=="scsi", PROGRAM=="/sbin/scsi_id -g -u -s %p", RESULT=="1IET_00060001", NAME="iscsi_F", OWNER="oracle11", GROUP="dba", MODE="0640"
# SCSI7
KERNEL=="sd*", BUS=="scsi", PROGRAM=="/sbin/scsi_id -g -u -s %p", RESULT=="1IET_00070001", NAME="iscsi_G", OWNER="oracle11", GROUP="dba", MODE="0640"


# udevcontrol reload_rules

# start_udev


-->

<br/><br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);"><strong>Подключение экспортированных дисков к узлам кластера</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
	</tr>
</table>

	# yum install -y iscsi-initiator-utils.x86_64

<br/>

	# service iscsid start

<br/>

// Получить список экспортированных дисков с storage:

	# iscsiadm -m discovery -t sendtargets -p 192.168.3.15:3260

<br/>

	# service iscsi restart

<br/>

<!--

Получить список подключенных дисков

# ls /dev/iscsi*
/dev/iscsi_A  /dev/iscsi_C  /dev/iscsi_E  /dev/iscsi_G
/dev/iscsi_B  /dev/iscsi_D  /dev/iscsi_F

-->

	# chkconfig --level 345 iscsi on
	# chkconfig --level 345 iscsid on


<br/><br/>

Посмотреть перед тем как использовать:<br/>
http://www.oracle-base.com/articles/linux/udev-scsi-rules-configuration-in-oracle-linux-5-and-6.php
