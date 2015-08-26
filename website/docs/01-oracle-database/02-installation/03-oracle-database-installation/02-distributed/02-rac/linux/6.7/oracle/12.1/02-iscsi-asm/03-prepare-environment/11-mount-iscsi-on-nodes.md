---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Монтирование RAID на узлах кластера
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/mount-iscsi-on-nodes/
---


# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Монтирование SCSI на узлах кластера


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>


<br/>

	# yum install -y device-mapper-multipath.x86_64

<br/>


	# vi /etc/multipath.conf

<br/>

	defaults {
	    user_friendly_names no
	    getuid_callout      "/sbin/scsi_id --whitelisted --replace-whitespace --device=/dev/%n"
	}

	multipaths {
	    multipath {
	            wwid                    1IET_00010001
	            alias                   iscsi1
	    }

	    multipath {
	            wwid                    1IET_00020001
	            alias                   iscsi2
	    }

	    multipath {
	            wwid                    1IET_00030001
	            alias                   iscsi3
	    }

	    multipath {
	            wwid                    1IET_00040001
	            alias                   iscsi4
	    }

		multipath {
				wwid                    1IET_00050001
				alias                   iscsi5
		}

		multipath {
				wwid                    1IET_00060001
				alias                   iscsi6
		}

		multipath {
				wwid                    1IET_00070001
				alias                   iscsi7
		}
	}


<br/>


	# chkconfig --level 345 multipathd on
	# service multipathd restart

<br/>



	# yum install -y \
    iscsi-initiator-utils.x86_64

<br/>

	# chkconfig --level 345 iscsi on
	# chkconfig --level 345 iscsid on


<br/>

// Получить список экспортированных дисков с storage:

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

	# service iscsi restart
	# service iscsid restart


<br/>


	# ls /dev/mapper
	control  iscsi2  iscsi4  iscsi6  VolGroup-lv_root
	iscsi1   iscsi3  iscsi5  iscsi7  VolGroup-lv_swap

<br/>

	# multipath -ll
	iscsi7 (1IET_00070001) dm-4 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 9:0:0:1 sdh 8:112 active ready running
	iscsi6 (1IET_00060001) dm-6 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 6:0:0:1 sdf 8:80  active ready running
	iscsi5 (1IET_00050001) dm-8 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 7:0:0:1 sdg 8:96  active ready running
	iscsi4 (1IET_00040001) dm-3 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 3:0:0:1 sdc 8:32  active ready running
	iscsi3 (1IET_00030001) dm-7 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 8:0:0:1 sdi 8:128 active ready running
	iscsi2 (1IET_00020001) dm-5 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 5:0:0:1 sde 8:64  active ready running
	iscsi1 (1IET_00010001) dm-2 IET,VIRTUAL-DISK
	size=40G features='0' hwhandler='0' wp=rw
	`-+- policy='round-robin 0' prio=1 status=active
	  `- 4:0:0:1 sdd 8:48  active ready running


<br/>

	# scsi_id --whitelisted --replace-whitespace --device=/dev/sdc
	1IET_00040001

Подробнее:

http://www.linuxtopia.org/online_books/rhel6/rhel_6_virtualization/rhel_6_virtualization_sect-Virtualization-Virtualized_block_devices-Configuring_persistent_storage_in_Red_Hat_Enterprise_Linux_5.html
