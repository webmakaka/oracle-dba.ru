---
layout: page
title: Oracle DataBase 12c - Linux - Подготовка жестких дисков к инсталляции базы данных
permalink: /docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.7/oracle/12.1/prepare-hdd-to-install-oracle/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Подготовка жестких дисков к инсталляции базы данных



В каталоге /u01 будет храниться программное обеспечение для работы с базами данных (Database Software) а в каталоге /u02 файлы базы данных.


	# ls /dev/sd*

<br/>


	/dev/sda   /dev/sda2  /dev/sdc  /dev/sde  /dev/sdg
	/dev/sda1  /dev/sdb   /dev/sdd  /dev/sdf  /dev/sdh



Создаем разделы на имеющихся у нас жестких дисках.


	# fdisk /dev/sdb
	# fdisk /dev/sdc
	# fdisk /dev/sdd


<br/>


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



Создаем файловую систему на созданных разделах.


	# mkfs.ext4 /dev/sdb1
	# mkfs.ext4 /dev/sdc1
	# mkfs.ext4 /dev/sdd1

<br/>

	# mkdir /u01
	# mkdir /u02
	# mkdir /u03


Записываем информацию о том, куда следует монтировать разделы при загрузки операционной системы.


	# cp /etc/fstab /etc/fstab.bkp.$(date +%Y-%m-%d)
	# echo "/dev/sdb1 /u01 ext4 defaults 1 2" >> /etc/fstab
	# echo "/dev/sdc1 /u02 ext4 defaults 1 2" >> /etc/fstab
	# echo "/dev/sdd1 /u03 ext4 defaults 1 2" >> /etc/fstab


<br/>

	# mount /u01
	# mount /u02
	# mount /u03


Проверка


	# mount | grep sdb1
	# mount | grep sdc1
	# mount | grep sdd1
