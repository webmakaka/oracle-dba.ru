---
layout: page
title: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Настройка правил монтирования SCSI дисков на узлах кластера с помощью Device Mapper
description: Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM) - Настройка правил монтирования SCSI дисков на узлах кластера с помощью Device Mapper
keywords: Oracle DataBase 12.1, Oracle Linux 6.7, RAC, (ISCSI + ASM)
permalink: /database/installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-mounting-rules-by-device-mapper/
---

# [Инсталляция Oracle RAC 12.1 в Oracle Linux 6.7 (ISCSI + ASM)]: Настройка правил монтирования SCSI дисков на узлах кластера с помощью Device Mapper

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
    			alias                   iscsi-disk1
    	}

    	multipath {
    			wwid                    1IET_00020001
    			alias                   iscsi-disk2
    	}

    	multipath {
    			wwid                    1IET_00030001
    			alias                   iscsi-disk3
    	}

    	multipath {
    			wwid                    1IET_00040001
    			alias                   iscsi-disk4
    	}

    	multipath {
    			wwid                    1IET_00050001
    			alias                   iscsi-disk5
    	}

    	multipath {
    			wwid                    1IET_00060001
    			alias                   iscsi-disk6
    	}

    	multipath {
    			wwid                    1IET_00070001
    			alias                   iscsi-disk7
    	}

<br/>

    # chkconfig --level 345 multipathd on
    # service multipathd restart

<br/>

    # ls /dev/mapper

<br/>

    # multipath -ll

<!--

http://www.hhutzler.de/blog/rac-11-2-0-4-setup-using-openfiler-with-multipathed-iscsi-disks/

-->
