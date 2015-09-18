---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Подготовка локальных дисков на узлах кластера для инсталляции на них Oracle Database Software
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/prepare-hdd-to-install-oracle/
---


# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Подготовка локальных дисков на узлах кластера для инсталляции на них Oracle Database Software


<br/>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>



	# fdisk /dev/sdb

	WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
	         switch off the mode (command 'c') and change display units to
	         sectors (command 'u').

	Command (m for help): c
	DOS Compatibility flag is not set

	Command (m for help): u
	Changing display/entry units to sectors

	Command (m for help): n
	Command action
	   e   extended
	   p   primary partition (1-4)
	p
	Partition number (1-4): 1
	First sector (2048-83886079, default 2048):
	Using default value 2048
	Last sector, +sectors or +size{K,M,G} (2048-83886079, default 83886079):
	Using default value 83886079

	Command (m for help): w
	The partition table has been altered!

	Calling ioctl() to re-read partition table.
	Syncing disks.



<br/>

	# mkfs.ext4 /dev/sdb1

<br/>

	# mkdir /u01

<br/>

	# cp /etc/fstab /etc/fstab.bkp
	# echo "/dev/sdb1 /u01 ext4 defaults 1 2" >> /etc/fstab

<br/>

	# mount /u01

<br/>

	# mount | grep sdb1
	/dev/sdb1 on /u01 type ext4 (rw)
