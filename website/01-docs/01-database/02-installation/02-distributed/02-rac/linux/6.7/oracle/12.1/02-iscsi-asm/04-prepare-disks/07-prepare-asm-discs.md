---
layout: page
title: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Настройка ASM на узлах кластера, маркировка дисков как ASM
description: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Настройка ASM на узлах кластера, маркировка дисков как ASM
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, (ISCSI + ASM)
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/prepare-asm-discs/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: Настройка ASM на узлах кластера, маркировка дисков как ASM

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

Если используется Divice Mapper, то выполняем следующий шаг, иначе при инсталляции возникнет ошибка: <a href="https://oracledba.net/docs/errors/ins-32148/Execution-of-GI-Install-script-failed-on-nodes/">[INS-32148] Execution of 'GI Install' script failed on nodes: [rac2]</a>

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
</table>

<br/>

### Маркируем диски как ASM:

Если используется Device Mapper то:

    # {
        /etc/init.d/oracleasm createdisk ASMDISK1 /dev/mapper/iscsi-disk1
        /etc/init.d/oracleasm createdisk ASMDISK2 /dev/mapper/iscsi-disk2
        /etc/init.d/oracleasm createdisk ASMDISK3 /dev/mapper/iscsi-disk3
        /etc/init.d/oracleasm createdisk ASMDISK4 /dev/mapper/iscsi-disk4
        /etc/init.d/oracleasm createdisk ASMDISK5 /dev/mapper/iscsi-disk5
        /etc/init.d/oracleasm createdisk ASMDISK6 /dev/mapper/iscsi-disk6
        /etc/init.d/oracleasm createdisk ASMDISK7 /dev/mapper/iscsi-disk7
    }

    Marking disk "ASMDISK" as an ASM disk:                        [  OK  ]

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

Нужно убедиться что диски подмонтированы на всех узлах кластера. И при вводе следующей команды, возвращают следующие данные на обоих узлах.

    # oracleasm listdisks
    ASMDISK1
    ASMDISK2
    ASMDISK3
    ASMDISK4
    ASMDISK5
    ASMDISK6
    ASMDISK7

Если используется Device Mapper то:

    # oracleasm scandisks
    # oracleasm listdisks

---

Если используются правила Udev то, нужно явно указать, где лежат эти самые диски:

    # oracleasm scandisks /dev/mapper/iscsi-disk* --verbose
    # oracleasm listdisks

Я пока не нашел способа, как настроить сканирование дисков без доп параметров. Скорее всего это явно прописывается в файле /etc/sysconfig/oracleasm. Но мне пока не удалось добиться нужно результата.

Поэтому, дополнительно прописываю в cron задание, которое должно быть выполнено при перезагрузке.

---

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1,rac2</strong></span></td>
</tr>

</table>

    # chkconfig --level 345 crond on
    # service crond restart

    # crontab -e
    @reboot /usr/sbin/oracleasm scandisks /dev/mapper/iscsi-disk*

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
    ORACLEASM_GID=asmadmin
    ORACLEASM_SCANBOOT=true
    ORACLEASM_SCANORDER=""
    ORACLEASM_SCANEXCLUDE=""
    ORACLEASM_USE_LOGICAL_BLOCK_SIZE="false"

Конфиг в текстовом формате

    # vi /etc/sysconfig/oracleasm

Файл логов

    # less /var/log/oracleasm

<br/>

    # udevadm info --query=all --name=/dev/iscsi-disk1
    P: /devices/platform/host3/session1/target3:0:0/3:0:0:1/block/sdc/sdc1
    N: iscsi-disk1
    W: 73
    S: block/8:33
    S: disk/by-id/scsi-1IET_00040001-part1
    S: disk/by-path/ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk4-lun-1-part1
    S: disk/by-label/ASMDISK1
    E: UDEV_LOG=3
    E: DEVPATH=/devices/platform/host3/session1/target3:0:0/3:0:0:1/block/sdc/sdc1
    E: MAJOR=8
    E: MINOR=33
    E: DEVNAME=/dev/iscsi-disk1
    E: DEVTYPE=partition
    E: SUBSYSTEM=block
    E: ID_SCSI=1
    E: ID_VENDOR=IET
    E: ID_VENDOR_ENC=IET\x20\x20\x20\x20\x20
    E: ID_MODEL=VIRTUAL-DISK
    E: ID_MODEL_ENC=VIRTUAL-DISK
    E: ID_REVISION=0001
    E: ID_TYPE=disk
    E: ID_SERIAL_RAW=1IET     00040001
    E: ID_SERIAL=1IET_00040001
    E: ID_SERIAL_SHORT=IET_00040001
    E: ID_SCSI_SERIAL=beaf41
    E: ID_BUS=scsi
    E: ID_PATH=ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk4-lun-1
    E: ID_PART_TABLE_TYPE=dos
    E: ID_FS_LABEL=ASMDISK1
    E: ID_FS_LABEL_ENC=ASMDISK1
    E: ID_FS_TYPE=oracleasm
    E: ID_FS_USAGE=filesystem
    E: LVM_SBIN_PATH=/sbin
    E: DEVLINKS=/dev/block/8:33 /dev/disk/by-id/scsi-1IET_00040001-part1 /dev/disk/by-path/ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk4-lun-1-part1 /dev/disk/by-label/ASMDISK1
