---
layout: page
title: Oracle DataBase 12c - Linux - Подготовка жестких дисков к инсталляции базы данных
permalink: /database/installation/single-instance/simple/linux/7.3/oracle/12.2/prepare-hdd-to-install-oracle/
---

<br/>

<div style="padding:10px; border:thin solid black;">

	<h3>Этот материал в разработке. Рекомендую обратиться к последней версии документа.</h3>

    <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">Ссылка на документ по инсталляции Oracle.</a>

</div>

<br/>

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Подготовка жестких дисков к инсталляции базы данных



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


# fdisk /dev/sdb


    Welcome to fdisk (util-linux 2.23.2).

    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.

    Device does not contain a recognized partition table
    Building a new DOS disklabel with disk identifier 0x32ddb4e2.

    Command (m for help): n
    Partition type:
       p   primary (0 primary, 0 extended, 4 free)
       e   extended
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-83886079, default 2048):
    Using default value 2048
    Last sector, +sectors or +size{K,M,G} (2048-83886079, default 83886079):
    Using default value 83886079
    Partition 1 of type Linux and of size 40 GiB is set

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
