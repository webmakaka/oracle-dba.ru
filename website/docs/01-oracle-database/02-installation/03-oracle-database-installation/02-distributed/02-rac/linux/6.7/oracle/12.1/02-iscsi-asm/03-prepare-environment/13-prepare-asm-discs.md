---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Настройка конфигурации для работы в ASM
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/prepare-asm-discs/
---


<br/>

### [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Настройка конфигурации для работы в ASM


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>

<br/>

    # /etc/init.d/oracleasm configure

<br/>

    Default user to own the driver interface []: oracle12
    Default group to own the driver interface []: dba
    Start Oracle ASM library driver on boot (y/n) [n]: y
    Scan for Oracle ASM disks on boot (y/n) [y]: y
    Writing Oracle ASM library driver configuration: done
    Initializing the Oracle ASMLib driver:                     [  OK  ]
    Scanning the system for Oracle ASMLib disks:               [  OK  ]


<br/>

    # /etc/init.d/oracleasm status

<br/>

    Checking if ASM is loaded: yes
    Checking if /dev/oracleasm is mounted: yes


<br/>


# Маркируем диски как ASM диски:


<br/>

### Eсли использовался вариант 1: С помощь device-mapper


    # /etc/init.d/oracleasm createdisk ASMDISK1 /dev/mapper/asm-disk1
    # /etc/init.d/oracleasm createdisk ASMDISK2 /dev/mapper/asm-disk2
    # /etc/init.d/oracleasm createdisk ASMDISK3 /dev/mapper/asm-disk3
    # /etc/init.d/oracleasm createdisk ASMDISK4 /dev/mapper/asm-disk4
    # /etc/init.d/oracleasm createdisk ASMDISK5 /dev/mapper/asm-disk5
    # /etc/init.d/oracleasm createdisk ASMDISK6 /dev/mapper/asm-disk6
    # /etc/init.d/oracleasm createdisk ASMDISK7 /dev/mapper/asm-disk7

    Marking disk "ASMDISK" as an ASM disk:                        [  OK  ]


<br/>

### Eсли использовался вариант 2: С помощь udev правил


Какое-то абсолютное непонимание, почему так. Да еще и на 2-х серверах.
Наверное, что-то неправильное делаю.

    # fdisk /dev/asm-disk1
    # fdisk /dev/asm-disk2
    # fdisk /dev/asm-disk3
    # fdisk /dev/asm-disk4
    # fdisk /dev/asm-disk5
    # fdisk /dev/asm-disk6
    # fdisk /dev/asm-disk7



<br/>


    # /etc/init.d/oracleasm createdisk ASMDISK1 /dev/asm-disk1
    # /etc/init.d/oracleasm createdisk ASMDISK2 /dev/asm-disk2
    # /etc/init.d/oracleasm createdisk ASMDISK3 /dev/asm-disk3
    # /etc/init.d/oracleasm createdisk ASMDISK4 /dev/asm-disk4
    # /etc/init.d/oracleasm createdisk ASMDISK5 /dev/asm-disk5
    # /etc/init.d/oracleasm createdisk ASMDISK6 /dev/asm-disk6
    # /etc/init.d/oracleasm createdisk ASMDISK7 /dev/asm-disk7

    Marking disk "ASMDISK" as an ASM disk:                        [  OK  ]



<br/>

// Посмотреть список дисков

    # /etc/init.d/oracleasm listdisks
    ASMDISK1
    ASMDISK2
    ASMDISK3
    ASMDISK4
    ASMDISK5
    ASMDISK6
    ASMDISK7

// Или так


    # ls /dev/oracleasm/disks/
    ASMDISK1  ASMDISK2  ASMDISK3  ASMDISK4  ASMDISK5  ASMDISK6  ASMDISK7



Посмотреть конфиг

    # /usr/sbin/oracleasm configure
    ORACLEASM_ENABLED=true
    ORACLEASM_UID=oracle12
    ORACLEASM_GID=dba
    ORACLEASM_SCANBOOT=true
    ORACLEASM_SCANORDER=""
    ORACLEASM_SCANEXCLUDE=""
    ORACLEASM_USE_LOGICAL_BLOCK_SIZE="false"

Конфиг в текстовом формате

    # vi /etc/sysconfig/oracleasm

<br/>

    # /etc/init.d/oracleasm querydisk -p ASMDISK1
    Disk "ASMDISK1" is a valid ASM disk
    /dev/sdd1: LABEL="ASMDISK1" TYPE="oracleasm"


<br/>

// файл логов

    # less /var/log/oracleasm

<br/>

// В некоторых случаях, необходимо перестартовать oracleasm

    # /etc/init.d/oracleasm restart




<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Проверка правильности инсталляции и конфигурирования ASM</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>


rac1:

	# /etc/init.d/oracleasm scandisks

rac2:

	# /etc/init.d/oracleasm scandisks

rac1:

	# /etc/init.d/oracleasm listdisks

rac2:

	# /etc/init.d/oracleasm listdisks


Нужно убедиться что диски подмонтированы на обоих серверах.
Если нет, перезагрузить узлы (после установки приоритетов автостарта пакетов, см. ниже)


<br/><br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Проверка правильности приоритера старта пакетов</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>


	# cd /etc/rc3.d

например:

	S60iscsi
	S65iscsid
	S80oracleasm

    # mv S13iscsi S60iscsi
    # mv S07iscsid S65iscsid
    # mv S29oracleasm S80oracleasm
