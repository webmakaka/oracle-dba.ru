---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Настройка правил монтирования SCSI дисков на узлах кластера с помощью Device Mapper
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-mounting-rules-by-device-mapper/
---


# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Настройка правил монтирования SCSI дисков на узлах кластера с помощью Device Mapper


### Настрока правил монтирования iSCSI дисков нодам кластера.

Вообщем если не настроить, могут произвольно подключаться, как следствие не исключаю возможность потери данных.


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
	# scsi_id --whitelisted --replace-whitespace --device=/dev/sdd
	1IET_00010001
	# scsi_id --whitelisted --replace-whitespace --device=/dev/sde
	1IET_00020001
	# scsi_id --whitelisted --replace-whitespace --device=/dev/sdf
	1IET_00060001
	# scsi_id --whitelisted --replace-whitespace --device=/dev/sdg
	1IET_00050001
	# scsi_id --whitelisted --replace-whitespace --device=/dev/sdh
	1IET_00070001
	# scsi_id --whitelisted --replace-whitespace --device=/dev/sdi
	1IET_00030001

<br/>

	# for i in c d e f g h i
	do
	scsi_id –whitelisted –replace-whitespace –device=/dev/sd$i
	done


<br/>

### Device Mapper


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>


	# yum install -y \
	device-mapper-multipath.x86_64

<br/>

	# vi /etc/multipath.conf

<br/>

	defaults {
		udev_dir              /dev
		polling_interval      10
		path_selector         "round-robin 0"
		path_grouping_policy  multibus
		getuid_callout        "/lib/udev/scsi_id --whitelisted --replace-whitespace --device=/dev/%n"
	#    prio                  alua
		path_checker          readsector0
		rr_min_io             100
		max_fds               8192
		rr_weight             priorities
		failback              immediate
		no_path_retry         fail
		user_friendly_names   yes
	}

	blacklist {
		# Blacklist by WWID
		wwid "*"
	}
	blacklist_exceptions {
		wwid "1IET_00010001"
		wwid "1IET_00020001"
		wwid "1IET_00030001"
		wwid "1IET_00040001"
		wwid "1IET_00050001"
		wwid "1IET_00060001"
		wwid "1IET_00070001"

	}

	multipaths {
		multipath {
				wwid                    1IET_00010001
				alias                   asm-disk1
		}

		multipath {
				wwid                    1IET_00020001
				alias                   asm-disk2
		}

		multipath {
				wwid                    1IET_00030001
				alias                   asm-disk3
		}

		multipath {
				wwid                    1IET_00040001
				alias                   asm-disk4
		}

		multipath {
				wwid                    1IET_00050001
				alias                   asm-disk5
		}

		multipath {
				wwid                    1IET_00060001
				alias                   asm-disk6
		}

		multipath {
				wwid                    1IET_00070001
				alias                   asm-disk7
		}


<br/>


	# chkconfig --level 345 multipathd on
	# service multipathd restart

<br/>

	# ls /dev/mapper
	asm-disk1  asm-disk3  asm-disk5  asm-disk7  VolGroup-lv_root
	asm-disk2  asm-disk4  asm-disk6  control    VolGroup-lv_swap

<br/>

	# multipath -ll
	asm-disk7 (1IET_00070001) dm-7 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 9:0:0:1 sdh 8:112 active ready running
	asm-disk6 (1IET_00060001) dm-4 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 6:0:0:1 sde 8:64  active ready running
	asm-disk5 (1IET_00050001) dm-6 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 7:0:0:1 sdg 8:96  active ready running
	asm-disk4 (1IET_00040001) dm-2 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 3:0:0:1 sdc 8:32  active ready running
	asm-disk3 (1IET_00030001) dm-8 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 8:0:0:1 sdi 8:128 active ready running
	asm-disk2 (1IET_00020001) dm-5 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 5:0:0:1 sdf 8:80  active ready running
	asm-disk1 (1IET_00010001) dm-3 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 4:0:0:1 sdd 8:48  active ready running




<!--

http://www.hhutzler.de/blog/rac-11-2-0-4-setup-using-openfiler-with-multipathed-iscsi-disks/

-->
