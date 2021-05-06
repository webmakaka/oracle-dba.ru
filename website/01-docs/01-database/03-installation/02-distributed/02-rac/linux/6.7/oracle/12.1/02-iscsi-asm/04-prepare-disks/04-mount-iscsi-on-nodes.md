---
layout: page
title: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Монтирование SCSI дисков на узлах кластера
description: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Монтирование SCSI дисков на узлах кластера
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, (ISCSI + ASM)
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/mount-iscsi-on-nodes/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: Монтирование SCSI дисков на узлах кластера

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>

    # yum install -y \
    iscsi-initiator-utils.x86_64

<br/>

    # chkconfig --level 345 iscsi on
    # chkconfig --level 345 iscsid on

<br/>

Получить список экспортированных дисков с storage:

    # iscsiadm -m discovery -t sendtargets -p 192.168.3.15:3260

    Starting iscsid:                                           [  OK  ]
    192.168.3.15:3260,1 ru.oracle-dba:disk1
    192.168.3.15:3260,1 ru.oracle-dba:disk2
    192.168.3.15:3260,1 ru.oracle-dba:disk3
    192.168.3.15:3260,1 ru.oracle-dba:disk4
    192.168.3.15:3260,1 ru.oracle-dba:disk5
    192.168.3.15:3260,1 ru.oracle-dba:disk6
    192.168.3.15:3260,1 ru.oracle-dba:disk7

<br/>

    # service iscsid restart
    # service iscsi restart

<br/>

### Результаты:

    # ls -l /dev/disk/by-path/
    total 0
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk1-lun-1 -> ../../sdd
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk2-lun-1 -> ../../sde
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk3-lun-1 -> ../../sdi
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk4-lun-1 -> ../../sdc
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk5-lun-1 -> ../../sdg
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk6-lun-1 -> ../../sdf
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 ip-192.168.3.15:3260-iscsi-ru.oracle-dba:disk7-lun-1 -> ../../sdh
    lrwxrwxrwx 1 root root  9 Aug 30  2015 pci-0000:00:01.1-scsi-0:0:0:0 -> ../../sr0
    lrwxrwxrwx 1 root root  9 Aug 30  2015 pci-0000:00:16.0-sas-0x00060504030201a0-lun-0 -> ../../sda
    lrwxrwxrwx 1 root root 10 Aug 30  2015 pci-0000:00:16.0-sas-0x00060504030201a0-lun-0-part1 -> ../../sda1
    lrwxrwxrwx 1 root root 10 Aug 30  2015 pci-0000:00:16.0-sas-0x00060504030201a0-lun-0-part2 -> ../../sda2
    lrwxrwxrwx 1 root root  9 Aug 30  2015 pci-0000:00:16.0-sas-0x01060504030201a0-lun-0 -> ../../sdb
    lrwxrwxrwx 1 root root 10 Aug 30  2015 pci-0000:00:16.0-sas-0x01060504030201a0-lun-0-part1 -> ../../sdb1

<br/>

    # ls -l /dev/disk/by-id/

    total 0
    lrwxrwxrwx 1 root root  9 Aug 30  2015 ata-VBOX_CD-ROM_VB0-01f003f6 -> ../../sr0
    lrwxrwxrwx 1 root root 10 Aug 30  2015 dm-name-VolGroup-lv_root -> ../../dm-0
    lrwxrwxrwx 1 root root 10 Aug 30  2015 dm-name-VolGroup-lv_swap -> ../../dm-1
    lrwxrwxrwx 1 root root 10 Aug 30  2015 dm-uuid-LVM-xT7O36GGtKKaYDOOvFqcFZv9nknGEjgDbc4YIbNz0Eg8W0FMUTFfuFD2eUCKdR8r -> ../../dm-0
    lrwxrwxrwx 1 root root 10 Aug 30  2015 dm-uuid-LVM-xT7O36GGtKKaYDOOvFqcFZv9nknGEjgDvumafwdAzDL9wD2ldsyTHuwfu3r6v0o0 -> ../../dm-1
    lrwxrwxrwx 1 root root 10 Aug 30  2015 lvm-pv-uuid-iZA9q9-she5-tJvn-f75F-MZsB-spCV-HQ8Q0P -> ../../sda2
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 scsi-1IET_00010001 -> ../../sdd
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 scsi-1IET_00020001 -> ../../sde
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 scsi-1IET_00030001 -> ../../sdi
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 scsi-1IET_00040001 -> ../../sdc
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 scsi-1IET_00050001 -> ../../sdg
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 scsi-1IET_00060001 -> ../../sdf
    lrwxrwxrwx 1 root root  9 Aug 29 23:03 scsi-1IET_00070001 -> ../../sdh

<br/>

### Настрока правил монтирования iSCSI дисков нодам кластера.

В общем если не настроить, могут произвольно подключаться, как следствие не исключаю возможность потери данных.

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
</tr>

</table>

Получаем идентификаторы начиная с /dev/sdc:

    # ls /dev/sd*
    /dev/sda   /dev/sda2  /dev/sdb1  /dev/sdd  /dev/sdf  /dev/sdh
    /dev/sda1  /dev/sdb   /dev/sdc   /dev/sde  /dev/sdg  /dev/sdi

На виртуальной машине, виртуальные диски выдают следующие результаты:

    # scsi_id --whitelisted --replace-whitespace --device=/dev/sdc
    1IET_00040001

<br/>

    # for i in c d e f g h i
    do
    scsi_id --whitelisted --replace-whitespace --device=/dev/sd$i
    done

<br/>

    1IET_00040001
    1IET_00010001
    1IET_00020001
    1IET_00060001
    1IET_00050001
    1IET_00070001
    1IET_00030001
