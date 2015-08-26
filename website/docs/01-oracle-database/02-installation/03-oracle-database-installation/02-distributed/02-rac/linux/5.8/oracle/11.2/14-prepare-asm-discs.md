---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/prepare-asm-discs/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Инсталляция asmlib


<br/>


<strong>Необходимо установить 3 пакета:</strong><br/>

<ul>
	<li>oracleasm-*.rpm (пакет должен соответствовать ядру)</li>
	<li>oracleasm-support*.rpm</li>
	<li>oracleasmlib*.rpm</li>
</ul>

<br/>

	# yum search oracleasm
	# yum search oracleasmlib
	# yum search oracleasm-support


Те пакеты, которые не удастся найти в репозитории Oracle, рекомендуется скачать с официального сайта:<br/>
http://www.oracle.com/technetwork/server-storage/linux/downloads/rhel5-084877.html

<br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Инсталляция пакетов ASMlib</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
</tr>

</table>


Для начала следует понять, какое ядро linux поддерживается инсталлируемыми пакетами.


Проверяем, какое ядро используется на нашей виртуальной машине:

	# uname -rm
	2.6.32-300.10.1.el5uek x86_64


В репозитории последние пакеты oracleasm для ядра.
oracleasm-2.6.18-308.el5.x86_64

Необходимо выбрать нужное ядро.

В файле grub.conf нужно указать, какое ядро следует использовать и после этого перезагружить узел.

	# vi /etc/grub.conf

<br/>

	default=1
	timeout=0
	splashimage=(hd0,0)/boot/grub/splash.xpm.gz
	hiddenmenu
	title Oracle Linux Server (2.6.32-300.10.1.el5uek)
	        root (hd0,0)
	        kernel /boot/vmlinuz-2.6.32-300.10.1.el5uek ro root=LABEL=/
	        initrd /boot/initrd-2.6.32-300.10.1.el5uek.img
	title Oracle Linux Server-base (2.6.18-308.el5)
	        root (hd0,0)
	        kernel /boot/vmlinuz-2.6.18-308.el5 ro root=LABEL=/
	        initrd /boot/initrd-2.6.18-308.el5.img

<br/>

	# reboot

После перезагрузки:

	# uname -rm
	2.6.18-308.el5 x86_64

Для инсталляции достаточно будет выполнить следующие команы:

	# cd /tmp
	# wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.4-1.el5.x86_64.rpm

<br/>

	# yum install -y \
	oracleasm-2.6.18-308.el5.x86_64 \
	oracleasmlib-2.0.4-1.el5.x86_64.rpm \
	oracleasm-support.x86_64


Убедитесь, что установлены следующие пакеты на обоих узлах кластера

	# rpm -qa | grep oracleasm
	oracleasm-support-2.1.7-1.el5
	oracleasm-2.6.18-308.el5-2.0.5-1.el5
	oracleasmlib-2.0.4-1.el5


<br/><br/>


<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Конфигурирование Oracle ASM</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
</tr>

</table>


	# /etc/init.d/oracleasm configure

<br/>

	Default user to own the driver interface []: oracle11
	Default group to own the driver interface []: dba
	Start Oracle ASM library driver on boot (y/n) [n]: y
	Scan for Oracle ASM disks on boot (y/n) [y]: y
	Writing Oracle ASM library driver configuration: done
	Initializing the Oracle ASMLib driver:                 	[  OK  ]
	Scanning the system for Oracle ASMLib disks:           	[  OK  ]


Если [FAILED], можно посмотреть логи

	# less /var/log/oracleasm

Ошибка может возникнуть, если указаны неправильные параметры user, group или выбран неправильная версия драйвера Oracle ASM (драйвер должен соответствовать ядру).


	# /etc/init.d/oracleasm status
	Checking if ASM is loaded: yes
	Checking if /dev/oracleasm is mounted: yes



<br/><br/>


<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Добавление дисков в пул ASM</strong></span>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1</strong></span></td>
	</tr>
</table>

<!--

# fdisk /dev/iscsi_A
# fdisk /dev/iscsi_B
# fdisk /dev/iscsi_C
# fdisk /dev/iscsi_D
# fdisk /dev/iscsi_E
# fdisk /dev/iscsi_F
# fdisk /dev/iscsi_G


Мне не удалось в версии 5.8 получить идентификатор подключаемых разделов.
Как следствие я не смог их смонтировать с нужными для меня именами.

-->

	# fdisk /dev/{подмонтированный диск1}

<br/>

	# ls /dev/sd*
	/dev/sda   /dev/sdb   /dev/sdd  /dev/sdg   /dev/sdj1  /dev/sdm1
	/dev/sda1  /dev/sdb1  /dev/sde  /dev/sdh   /dev/sdk1  /dev/sdn1
	/dev/sda2  /dev/sdc   /dev/sdf  /dev/sdi1  /dev/sdl1  /dev/sdo1


Маркируем диски как ASM диски:


	# /etc/init.d/oracleasm createdisk VOL1 /dev/sdi1
	# /etc/init.d/oracleasm createdisk VOL2 /dev/sdj1
	# /etc/init.d/oracleasm createdisk VOL3 /dev/sdk1
	# /etc/init.d/oracleasm createdisk VOL4 /dev/sdl1
	# /etc/init.d/oracleasm createdisk VOL5 /dev/sdm1
	# /etc/init.d/oracleasm createdisk VOL6 /dev/sdn1
	# /etc/init.d/oracleasm createdisk VOL7 /dev/sdo1

	Marking disk "VOL1" as an ASM disk:                    	[  OK  ]



// Посмотреть метку диска

	# oracleasm querydisk /dev/sdi1

// Если нужно удалить

	# /etc/init.d/oracleasm deletedisk VOL1
	# dd if=/dev/zero of=/dev/sdi1



// Посмотреть список дисков ASM

	# /etc/init.d/oracleasm listdisks

	VOL1
	VOL2
	VOL3
	VOL4
	VOL5
	VOL6
	VOL7

// Или так

	# ls /dev/oracleasm/disks/
	VOL1  VOL2  VOL3  VOL4  VOL5  VOL6  VOL7


// файл логов

	# less /var/log/oracleasm

// В некоторых случаях, необходимо перестартовать oracleasm

	# /etc/init.d/oracleasm restart


<br/><br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Проверка правильности инсталляции и конфигурирования ASM</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
</tr>

</table>


node1:

	# /etc/init.d/oracleasm scandisks

node2:

	# /etc/init.d/oracleasm scandisks

node1:

	# /etc/init.d/oracleasm listdisks

node2:

	# /etc/init.d/oracleasm listdisks


Нужно убедиться что диски подмонтированы на обоих серверах.
Если нет, перезагрузить узлы (после установки приоритетов автостарта пакетов, см. ниже)


<br/><br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Проверка правильности приоритера старта пакетов</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1, node2</strong></span></td>
</tr>

</table>


	# cd /etc/rc3.d

например:

	S60iscsi
	S65iscsid
	S80oracleasm
