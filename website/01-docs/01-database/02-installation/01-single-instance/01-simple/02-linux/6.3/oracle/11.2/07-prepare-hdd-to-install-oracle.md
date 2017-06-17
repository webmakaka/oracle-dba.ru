---
layout: page
title: Инсталляция Oracle DataBase Server 11.2.0.3.2 в операционной системе Oracle Linux 6.3 x86_64
permalink: /database/installation/single-instance/simple/linux/6.3/oracle/11.2/prepare-hdd-to-install-oracle/
---

# <a href="/database/installation/single-instance/simple/linux/6.3/oracle/11.2/">[Инсталляция Oracle DataBase Server 11.2.0.3 в Oracle Linux 6.3]</a>: Подготовка дисков к инсталляции базы данных


В каталоге /u01 будет храниться программное обеспечение для работы с базами данных (Database Software) а в каталоге /u02 файлы базы данных.


	# ls /dev/sd*0


<br/>

	/dev/sda   /dev/sda2  /dev/sdc  /dev/sde  /dev/sdg
	/dev/sda1  /dev/sdb   /dev/sdd  /dev/sdf  /dev/sdh


Создаем разделы на имеющихся у нас жестких дисках.

	# fdisk /dev/sdb
	# fdisk /dev/sdc
	# fdisk /dev/sdd

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
	[p]
	Partition number (1-4): [1]
	First cylinder (1-5221, default 1): [Enter]
	Using default value 1
	Last cylinder or +size or +sizeM or +sizeK (1-5221, default 5221): [Enter]
	Using default value 5221

	Command (m for help): [w]
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


	# cp /etc/fstab /etc/fstab.bkp
	# echo "/dev/sdb1 /u01 ext4 defaults 1 2" >> /etc/fstab
	# echo "/dev/sdc1 /u02 ext4 defaults 1 2" >> /etc/fstab
	# echo "/dev/sdd1 /u03 ext4 defaults 1 2" >> /etc/fstab

<br/>

	# mount /u01
	# mount /u02
	# mount /u03

<br/>

Проверка

	# mount | grep sdb1
	# mount | grep sdc1
	# mount | grep sdd1



<br/><br/>
<br/><br/>


<div style="padding:10px; border:thin solid black;">

	<h3>Рекомендую обратиться сразу к последней версии документа, где используются более новые версии программного обеспечения</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>
