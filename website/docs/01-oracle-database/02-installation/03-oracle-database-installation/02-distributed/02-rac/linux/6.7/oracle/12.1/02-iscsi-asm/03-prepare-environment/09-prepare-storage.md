---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Подготовка сервера storage
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/prepare-storage/
---

# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Подготовка сервера storage (ISCSI)


<br/>


<ul>
	<li>iSCSI target — программа или контроллер, осуществляющие эмуляцию диска и выполняющие запросы iSCSI.</li>
	<li>iSCSI initiator — программа, осуществляющая клиентский доступ к SCSI.</li>
</ul>

<br/><br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Инсталляция iSCSI target</strong></span>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
	<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
	<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>storage</strong></span></td>
	</tr>
</table>


	# yum install -y \
	scsi-target-utils


<br/>

	# ls /dev/sd*

<br/>

	/dev/sda   /dev/sda2  /dev/sdc  /dev/sde  /dev/sdg
	/dev/sda1  /dev/sdb   /dev/sdd  /dev/sdf  /dev/sdh


Повторяем последовательно команды:

	# fdisk /dev/sdb
	# fdisk /dev/sdc
	# fdisk /dev/sdd
	# fdisk /dev/sde
	# fdisk /dev/sdf
	# fdisk /dev/sdg
	# fdisk /dev/sdh


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


<br/>

	# ls /dev/sd*

<br/>

	/dev/sda   /dev/sdb   /dev/sdc1  /dev/sde   /dev/sdf1  /dev/sdh
	/dev/sda1  /dev/sdb1  /dev/sdd   /dev/sde1  /dev/sdg   /dev/sdh1
	/dev/sda2  /dev/sdc   /dev/sdd1  /dev/sdf   /dev/sdg1

<br/>

	# vi /etc/tgt/targets.conf

Обязательно должна быть разкомментирована строка:

	default-driver iscsi

<br/>

	<target ru.oracle-dba:disk1>
	        backing-store /dev/sdb1
	        initiator-address 192.168.3.11
	        initiator-address 192.168.3.12
	</target>
	<target ru.oracle-dba:disk2>
	        backing-store /dev/sdc1
	        initiator-address 192.168.3.11
	        initiator-address 192.168.3.12
	</target>
	<target ru.oracle-dba:disk3>
	        backing-store /dev/sdd1
	        initiator-address 192.168.3.11
	        initiator-address 192.168.3.12
	</target>
	<target ru.oracle-dba:disk4>
	        backing-store /dev/sde1
	        initiator-address 192.168.3.11
	        initiator-address 192.168.3.12
	</target>
	<target ru.oracle-dba:disk5>
	        backing-store /dev/sdf1
	        initiator-address 192.168.3.11
	        initiator-address 192.168.3.12
	</target>
	<target ru.oracle-dba:disk6>
	        backing-store /dev/sdg1
	        initiator-address 192.168.3.11
	        initiator-address 192.168.3.12
	</target>
	<target ru.oracle-dba:disk7>
	        backing-store /dev/sdh1
	        initiator-address 192.168.3.11
	        initiator-address 192.168.3.12
	</target>


<br/>

	# chkconfig --level 345 tgtd on
	# service tgtd restart


Посмотреть результаты:

	# tgt-admin --show

<br/>

	Target 1: ru.oracle-dba:disk1
	    System information:
	        Driver: iscsi
	        State: ready
	    I_T nexus information:
	    LUN information:
	        LUN: 0
	            Type: controller
	            SCSI ID: IET     00010000
	            SCSI SN: beaf10
	            Size: 0 MB, Block size: 1
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: null
	            Backing store path: None
	            Backing store flags:
	        LUN: 1
	            Type: disk
	            SCSI ID: IET     00010001
	            SCSI SN: beaf11
	            Size: 42949 MB, Block size: 512
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: rdwr
	            Backing store path: /dev/sdb1
	            Backing store flags:
	    Account information:
	    ACL information:
	        192.168.3.11
	        192.168.3.12
	Target 2: ru.oracle-dba:disk2
	    System information:
	        Driver: iscsi
	        State: ready
	    I_T nexus information:
	    LUN information:
	        LUN: 0
	            Type: controller
	            SCSI ID: IET     00020000
	            SCSI SN: beaf20
	            Size: 0 MB, Block size: 1
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: null
	            Backing store path: None
	            Backing store flags:
	        LUN: 1
	            Type: disk
	            SCSI ID: IET     00020001
	            SCSI SN: beaf21
	            Size: 42949 MB, Block size: 512
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: rdwr
	            Backing store path: /dev/sdc1
	            Backing store flags:
	    Account information:
	    ACL information:
	        192.168.3.11
	        192.168.3.12
	Target 3: ru.oracle-dba:disk3
	    System information:
	        Driver: iscsi
	        State: ready
	    I_T nexus information:
	    LUN information:
	        LUN: 0
	            Type: controller
	            SCSI ID: IET     00030000
	            SCSI SN: beaf30
	            Size: 0 MB, Block size: 1
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: null
	            Backing store path: None
	            Backing store flags:
	        LUN: 1
	            Type: disk
	            SCSI ID: IET     00030001
	            SCSI SN: beaf31
	            Size: 42949 MB, Block size: 512
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: rdwr
	            Backing store path: /dev/sdd1
	            Backing store flags:
	    Account information:
	    ACL information:
	        192.168.3.11
	        192.168.3.12
	Target 4: ru.oracle-dba:disk4
	    System information:
	        Driver: iscsi
	        State: ready
	    I_T nexus information:
	    LUN information:
	        LUN: 0
	            Type: controller
	            SCSI ID: IET     00040000
	            SCSI SN: beaf40
	            Size: 0 MB, Block size: 1
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: null
	            Backing store path: None
	            Backing store flags:
	        LUN: 1
	            Type: disk
	            SCSI ID: IET     00040001
	            SCSI SN: beaf41
	            Size: 42949 MB, Block size: 512
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: rdwr
	            Backing store path: /dev/sde1
	            Backing store flags:
	    Account information:
	    ACL information:
	        192.168.3.11
	        192.168.3.12
	Target 5: ru.oracle-dba:disk5
	    System information:
	        Driver: iscsi
	        State: ready
	    I_T nexus information:
	    LUN information:
	        LUN: 0
	            Type: controller
	            SCSI ID: IET     00050000
	            SCSI SN: beaf50
	            Size: 0 MB, Block size: 1
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: null
	            Backing store path: None
	            Backing store flags:
	        LUN: 1
	            Type: disk
	            SCSI ID: IET     00050001
	            SCSI SN: beaf51
	            Size: 42949 MB, Block size: 512
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: rdwr
	            Backing store path: /dev/sdf1
	            Backing store flags:
	    Account information:
	    ACL information:
	        192.168.3.11
	        192.168.3.12
	Target 6: ru.oracle-dba:disk6
	    System information:
	        Driver: iscsi
	        State: ready
	    I_T nexus information:
	    LUN information:
	        LUN: 0
	            Type: controller
	            SCSI ID: IET     00060000
	            SCSI SN: beaf60
	            Size: 0 MB, Block size: 1
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: null
	            Backing store path: None
	            Backing store flags:
	        LUN: 1
	            Type: disk
	            SCSI ID: IET     00060001
	            SCSI SN: beaf61
	            Size: 42949 MB, Block size: 512
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: rdwr
	            Backing store path: /dev/sdg1
	            Backing store flags:
	    Account information:
	    ACL information:
	        192.168.3.11
	        192.168.3.12
	Target 7: ru.oracle-dba:disk7
	    System information:
	        Driver: iscsi
	        State: ready
	    I_T nexus information:
	    LUN information:
	        LUN: 0
	            Type: controller
	            SCSI ID: IET     00070000
	            SCSI SN: beaf70
	            Size: 0 MB, Block size: 1
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: null
	            Backing store path: None
	            Backing store flags:
	        LUN: 1
	            Type: disk
	            SCSI ID: IET     00070001
	            SCSI SN: beaf71
	            Size: 42949 MB, Block size: 512
	            Online: Yes
	            Removable media: No
	            Prevent removal: No
	            Readonly: No
	            Backing store type: rdwr
	            Backing store path: /dev/sdh1
	            Backing store flags:
	    Account information:
	    ACL information:
	        192.168.3.11
	        192.168.3.12
