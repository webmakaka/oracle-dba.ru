---
layout: page
title: Oracle RAC 11.2 ISCSI + ASM - Подготовка дисков
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/prepare-hdd-to-install-oracle/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Подготовка дисков


<br/>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
</tr>

</table>


	# fdisk /dev/sdb


<br/>

	The number of cylinders for this disk is set to 5221.
	There is nothing wrong with that, but this is larger than 1024,
	and could in certain setups cause problems with:
	1) software that runs at boot time (e.g., old versions of LILO)
	2) booting and partitioning software from other OSs
	  (e.g., DOS FDISK, OS/2 FDISK)

	Command (m for help): n
	Command action
	  e   extended
	  p   primary partition (1-4)
	p
	Partition number (1-4): 1
	First cylinder (1-5221, default 1):
	Using default value 1
	Last cylinder or +size or +sizeM or +sizeK (1-5221, default 5221):
	Using default value 5221

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

<br/>

	/dev/sdb1 on /u01 type ext4 (rw)
