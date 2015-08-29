---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Настройка ASM на узлах кластера, маркировка дисков как ASM /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/prepare-asm-discs/
---


<br/>

### [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Настройка ASM на узлах кластера, маркировка дисков как ASM


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
    Default group to own the driver interface []: asmadmin
    Start Oracle ASM library driver on boot (y/n) [n]: y
    Scan for Oracle ASM disks on boot (y/n) [y]: y
    Writing Oracle ASM library driver configuration: done
    Initializing the Oracle ASMLib driver:                     [  OK  ]
    Scanning the system for Oracle ASMLib disks:               [  OK  ]


Проверка:

    # /etc/init.d/oracleasm status

    Checking if ASM is loaded: yes
    Checking if /dev/oracleasm is mounted: yes


Если используется Divice Mapper, то выполняем следующий шаг, иначе при инсталляции возникнет ошибка: <a href="http://oracledba.net/docs/errors/ins-32148/Execution-of-GI-Install-script-failed-on-nodes/">[INS-32148] Execution of 'GI Install' script failed on nodes: [rac2]</a>



    # vi /etc/sysconfig/oracleasm

    ***
	ORACLEASM_SCANORDER=”dm”
	ORACLEASM_SCANEXCLUDE=”sd”
    ***

Перестартовываем сервис asmlib:

	# /etc/init.d/oracleasm restart

<br/>


# Маркируем диски как ASM диски:

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
</tr>

<br/>

### Маркируем диски как ASM:


    # /etc/init.d/oracleasm createdisk ASMDISK1 /dev/mapper/asm-disk1
    # /etc/init.d/oracleasm createdisk ASMDISK2 /dev/mapper/asm-disk2
    # /etc/init.d/oracleasm createdisk ASMDISK3 /dev/mapper/asm-disk3
    # /etc/init.d/oracleasm createdisk ASMDISK4 /dev/mapper/asm-disk4
    # /etc/init.d/oracleasm createdisk ASMDISK5 /dev/mapper/asm-disk5
    # /etc/init.d/oracleasm createdisk ASMDISK6 /dev/mapper/asm-disk6
    # /etc/init.d/oracleasm createdisk ASMDISK7 /dev/mapper/asm-disk7

    Marking disk "ASMDISK" as an ASM disk:                        [  OK  ]


<br/>


    # ls -l /dev/disk/by-label/
    total 0
    lrwxrwxrwx 1 root root 15 Aug 29 03:09 ASMDISK1 -> ../../asm-disk1
    lrwxrwxrwx 1 root root 15 Aug 29 03:09 ASMDISK2 -> ../../asm-disk2
    lrwxrwxrwx 1 root root 15 Aug 29 03:09 ASMDISK3 -> ../../asm-disk3
    lrwxrwxrwx 1 root root 15 Aug 29 03:09 ASMDISK4 -> ../../asm-disk4
    lrwxrwxrwx 1 root root 15 Aug 29 03:09 ASMDISK5 -> ../../asm-disk5
    lrwxrwxrwx 1 root root 15 Aug 29 03:09 ASMDISK6 -> ../../asm-disk6
    lrwxrwxrwx 1 root root 15 Aug 29 03:09 ASMDISK7 -> ../../asm-disk7

<br/>


Посмотреть список дисков

    # /etc/init.d/oracleasm listdisks
    ASMDISK1
    ASMDISK2
    ASMDISK3
    ASMDISK4
    ASMDISK5
    ASMDISK6
    ASMDISK7

Или так


    # ls /dev/oracleasm/disks/
    ASMDISK1  ASMDISK2  ASMDISK3  ASMDISK4  ASMDISK5  ASMDISK6  ASMDISK7




<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac2</strong></span></td>
</tr>

</table>


	# /etc/init.d/oracleasm scandisks --verbose
    # /etc/init.d/oracleasm listdisks
    ASMDISK1
    ASMDISK2
    ASMDISK3
    ASMDISK4
    ASMDISK5
    ASMDISK6
    ASMDISK7




Нужно убедиться что диски подмонтированы на всех узлах кластера.
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


<br/>

### Дополнительно для информации


    # /etc/init.d/oracleasm querydisk -p ASMDISK1
    Disk "ASMDISK1" is a valid ASM disk
    /dev/mapper/asm-disk1: LABEL="ASMDISK1" TYPE="oracleasm"



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

Файл логов

    # less /var/log/oracleasm
