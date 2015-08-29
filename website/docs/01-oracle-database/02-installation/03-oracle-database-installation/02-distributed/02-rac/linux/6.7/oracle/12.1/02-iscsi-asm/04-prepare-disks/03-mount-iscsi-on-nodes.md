---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Монтирование SCSI дисков на узлах кластера
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/mount-iscsi-on-nodes/
---


# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Монтирование SCSI дисков на узлах кластера


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>


	# yum install -y \
    iscsi-initiator-utils.x86_64

<br/>

	# chkconfig --level 345 iscsi on
	# chkconfig --level 345 iscsid on


<br/>

Получить список экспортированных дисков с storage:

    # iscsiadm -m discovery -t sendtargets -p 192.168.3.15:3260

    Starting iscsid:                                           [  OK  ]
    192.168.3.15:3260,1 ru.oracle-dba:disk1
    192.168.3.15:3260,1 ru.oracle-dba:disk2
    192.168.3.15:3260,1 ru.oracle-dba:disk3
    192.168.3.15:3260,1 ru.oracle-dba:disk4
    192.168.3.15:3260,1 ru.oracle-dba:disk5
    192.168.3.15:3260,1 ru.oracle-dba:disk6
    192.168.3.15:3260,1 ru.oracle-dba:disk7


<br/>

	# service iscsid restart
	# service iscsi restart


<br/>

	# ls -l /dev/disk/by-path/
	total 0
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk1-lun-1 -> ../../sdd
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk2-lun-1 -> ../../sde
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk3-lun-1 -> ../../sdh
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk4-lun-1 -> ../../sdc
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk5-lun-1 -> ../../sdg
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk6-lun-1 -> ../../sdf
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk7-lun-1 -> ../../sdi
	***

<br/>

	# ls -l /dev/disk/by-id/

	***
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 scsi-1IET_00010001 -> ../../sdd
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 scsi-1IET_00020001 -> ../../sde
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 scsi-1IET_00030001 -> ../../sdh
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 scsi-1IET_00040001 -> ../../sdc
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 scsi-1IET_00050001 -> ../../sdg
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 scsi-1IET_00060001 -> ../../sdf
	lrwxrwxrwx 1 root root  9 Aug 29 01:30 scsi-1IET_00070001 -> ../../sdi
