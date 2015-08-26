---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Подготовка сервера storage
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nfs/prepare-storage/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Подготовка сервера storage (RAID, NFS)


В реальной жизни все должно быть сделано аппаратно.
Прочем и я мог изначально создать большой диск.

По факту. Имеем группу дисков, которую хотим объединить в 1 диск и расшарить его на узлах кластера.

### Создание RAID массива


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">


<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>storage</strong></span></td>
</tr>

</table>



	# ls /dev/sd*
	/dev/sda   /dev/sda2  /dev/sdc  /dev/sde  /dev/sdg
	/dev/sda1  /dev/sdb   /dev/sdd  /dev/sdf  /dev/sdh


<br/>

	# fdisk /dev/sdb
	# fdisk /dev/sdc
	# fdisk /dev/sdd
	# fdisk /dev/sde
	# fdisk /dev/sdf
	# fdisk /dev/sdg
	# fdisk /dev/sdh

Повторяем на всех вышеперечисленных дискахдисках


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

	Command (m for help): t
	Selected partition 1
	Hex code (type L to list codes): fd
	Changed system type of partition 1 to fd (Linux raid autodetect)

	Command (m for help): w
	The partition table has been altered!

	Calling ioctl() to re-read partition table.
	Syncing disks.



<br/>


	#  fdisk -l

	Disk /dev/sdc: 42.9 GB, 42949672960 bytes
	171 heads, 5 sectors/track, 98112 cylinders
	Units = cylinders of 855 * 512 = 437760 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x000ac338

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sdc1               3       98113    41942016   fd  Linux raid autodetect

	Disk /dev/sda: 42.9 GB, 42949672960 bytes
	255 heads, 63 sectors/track, 5221 cylinders
	Units = cylinders of 16065 * 512 = 8225280 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x0004fc99

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sda1   *           1          64      512000   83  Linux
	Partition 1 does not end on cylinder boundary.
	/dev/sda2              64        5222    41430016   8e  Linux LVM

	Disk /dev/sdb: 42.9 GB, 42949672960 bytes
	171 heads, 5 sectors/track, 98112 cylinders
	Units = cylinders of 855 * 512 = 437760 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x0007dff7

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sdb1               3       98113    41942016   fd  Linux raid autodetect

	Disk /dev/sdd: 42.9 GB, 42949672960 bytes
	171 heads, 5 sectors/track, 98112 cylinders
	Units = cylinders of 855 * 512 = 437760 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x000cf6ea

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sdd1               3       98113    41942016   fd  Linux raid autodetect

	Disk /dev/sdf: 42.9 GB, 42949672960 bytes
	171 heads, 5 sectors/track, 98112 cylinders
	Units = cylinders of 855 * 512 = 437760 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x0003bbef

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sdf1               3       98113    41942016   fd  Linux raid autodetect

	Disk /dev/sdg: 42.9 GB, 42949672960 bytes
	171 heads, 5 sectors/track, 98112 cylinders
	Units = cylinders of 855 * 512 = 437760 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x0005d150

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sdg1               3       98113    41942016   fd  Linux raid autodetect

	Disk /dev/sdh: 42.9 GB, 42949672960 bytes
	171 heads, 5 sectors/track, 98112 cylinders
	Units = cylinders of 855 * 512 = 437760 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x000743bd

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sdh1               3       98113    41942016   fd  Linux raid autodetect

	Disk /dev/sde: 42.9 GB, 42949672960 bytes
	171 heads, 5 sectors/track, 98112 cylinders
	Units = cylinders of 855 * 512 = 437760 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x0000a2ae

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sde1               3       98113    41942016   fd  Linux raid autodetect

	Disk /dev/mapper/VolGroup-lv_root: 38.3 GB, 38260441088 bytes
	255 heads, 63 sectors/track, 4651 cylinders
	Units = cylinders of 16065 * 512 = 8225280 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x00000000


	Disk /dev/mapper/VolGroup-lv_swap: 4160 MB, 4160749568 bytes
	255 heads, 63 sectors/track, 505 cylinders
	Units = cylinders of 16065 * 512 = 8225280 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x00000000


<br/>


### Создание RAID-массива

	# mdadm --create --verbose /dev/md0 --level=5 --raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
	mdadm: layout defaults to left-symmetric
	mdadm: layout defaults to left-symmetric
	mdadm: chunk size defaults to 512K
	mdadm: size set to 41909248K
	mdadm: Defaulting to version 1.2 metadata
	mdadm: array /dev/md0 started.

<br/>

Создание файловой системы поверх RAID-массива


	# mkfs.ext4 /dev/md0

<br/>

	# mdadm --detail --scan --verbose

	ARRAY /dev/md0 level=raid5 num-devices=4 metadata=1.2 spares=1 name=storage.localdomain:0 UUID=8e3f5ae7:79a8160a:cbcad47a:ae3d9ccd
	   devices=/dev/sdb1,/dev/sdc1,/dev/sdd1,/dev/sde1


Создание конфигурационного файла mdadm.conf

	# mkdir /etc/mdadm
	# echo "DEVICE partitions" > /etc/mdadm/mdadm.conf
	# mdadm --detail --scan --verbose | awk '/ARRAY/ {print}' >> /etc/mdadm/mdadm.conf





Создание каталога, куда будет смонтировал RAID локально

	# mkdir /raid
	# chown -R oracle12:oinstall /raid
	# chmod -R 777 /raid


Создание каталога, куда будет смонтировал RAID локально

	# vi /etc/fstab

добавляем

	/dev/md0              /raid          ext4      defaults


<br/>

	# mount /raid

<br/>

	# df -h
	Filesystem            Size  Used Avail Use% Mounted on
	/dev/mapper/VolGroup-lv_root
	                       35G  1.8G   32G   6% /
	tmpfs                 1.9G     0  1.9G   0% /dev/shm
	/dev/sda1             477M  140M  308M  32% /boot
	/dev/md0              118G   60M  112G   1% /raid


<br/>

### Расшариваем диск

	# vi /etc/exports

добавить

	/raid *(rw,sync,no_wdelay,insecure_locks,no_root_squash)

<br/>

	# service  rpcbind restart
	# chkconfig --level 345 rpcbind on

	# chkconfig --level 345 nfs on
	# service nfs restart
