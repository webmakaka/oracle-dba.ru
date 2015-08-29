---
layout: page
title: Oracle RAC 12.1 ISCSI + ASM - Настройка правил монтирования SCSI дисков на узлах кластера с помощью правил Udev
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-mounting-rules-by-uder-rules/
---

# [Инсталляция Oracle RAC 12.1 ISCSI + ASM]: Настройка правил монтирования SCSI дисков на узлах кластера с помощью правил Udev



### Вариант монтирования дисков с помощью udev правил


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
</tr>

</table>


	# yum install -y \
	parted

<br/>

	# fdisk /dev/sdc
	# fdisk /dev/sdd
	# fdisk /dev/sde
	# fdisk /dev/sdf
	# fdisk /dev/sdg
	# fdisk /dev/sdh
	# fdisk /dev/sdi

<br/>

	# partprobe /dev/sdc1 /dev/sdd1 /dev/sde1 /dev/sdf1 /dev/sdg1 /dev/sdh1 /dev/sdi1

<br/>

	# /sbin/udevadm test /block/sdc/sdc1
	# /sbin/udevadm test /block/sdd/sdd1
	# /sbin/udevadm test /block/sde/sde1
	# /sbin/udevadm test /block/sdf/sdf1
	# /sbin/udevadm test /block/sdg/sdg1
	# /sbin/udevadm test /block/sdh/sdh1
	# /sbin/udevadm test /block/sdi/sdi1


<br/>

### Создание файла с правилами Udev

	# echo "options=-g" > /etc/scsi_id.config


<br/>

	i=1
	cmd="/sbin/scsi_id -g -u -d"
	for disk in sdc sdd sde sdf sdg sdh sdi ; do
	         cat <<EOF >> /etc/udev/rules.d/99-oracle-asmdevices.rules
	KERNEL=="sd?1", BUS=="scsi", PROGRAM=="$cmd /dev/\$parent", \
	 RESULT=="`$cmd /dev/$disk`", NAME="iscsi-disk$i", OWNER="oracle12", GROUP="asmadmin", MODE="0660"
	EOF
	         i=$(($i+1))
	done


<br/>

	# scp /etc/udev/rules.d/99-oracle-asmdevices.rules root@rac2:/etc/udev/rules.d/99-oracle-asmdevices.rules


<br/>

	# /sbin/udevadm control --reload-rules
	# /sbin/start_udev


<br/>


	# ls /dev/iscsi*
	/dev/iscsi-disk1  /dev/iscsi-disk3  /dev/iscsi-disk5  /dev/iscsi-disk7
	/dev/iscsi-disk2  /dev/iscsi-disk4  /dev/iscsi-disk6



Проверить можно следующей командой на rac1 и rac2, что диски правильно подмонтировались.

	# ls -l /dev/disk/by-id/





<!--


Почитать здесь:

http://www.linuxtopia.org/online_books/rhel6/rhel_6_virtualization/rhel_6_virtualization_sect-Virtualization-Virtualized_block_devices-Configuring_persistent_storage_in_Red_Hat_Enterprise_Linux_5.html




Make SCSI Devices Trusted

	# vi /etc/scsi_id.config

Добавить:

	options=--whitelisted --replace-whitespace


Create UDEV Rules File

	# vi /etc/udev/rules.d/99-oracle-asmdevices.rules

<br/>


	KERNEL=="sd*", SUBSYSTEM=="block", PROGRAM="/sbin/scsi_id --whitelisted --replace-whitespace /dev/$name", RESULT=="1IET_00010001", NAME="asm-disk1"

	KERNEL=="sd*", SUBSYSTEM=="block", PROGRAM="/sbin/scsi_id --whitelisted --replace-whitespace /dev/$name", RESULT=="1IET_00020001", NAME="asm-disk2"

	KERNEL=="sd*", SUBSYSTEM=="block", PROGRAM="/sbin/scsi_id --whitelisted --replace-whitespace /dev/$name", RESULT=="1IET_00030001", NAME="asm-disk3"

	KERNEL=="sd*", SUBSYSTEM=="block", PROGRAM="/sbin/scsi_id --whitelisted --replace-whitespace /dev/$name", RESULT=="1IET_00040001", NAME="asm-disk4"

	KERNEL=="sd*", SUBSYSTEM=="block", PROGRAM="/sbin/scsi_id --whitelisted --replace-whitespace /dev/$name", RESULT=="1IET_00050001", NAME="asm-disk5"

	KERNEL=="sd*", SUBSYSTEM=="block", PROGRAM="/sbin/scsi_id --whitelisted --replace-whitespace /dev/$name", RESULT=="1IET_00060001", NAME="asm-disk6"

	KERNEL=="sd*", SUBSYSTEM=="block", PROGRAM="/sbin/scsi_id --whitelisted --replace-whitespace /dev/$name", RESULT=="1IET_00070001", NAME="asm-disk7"



Test Rules


	# udevadm test /block/sdc
	# udevadm test /block/sdd
	# udevadm test /block/sde
	# udevadm test /block/sdf
	# udevadm test /block/sdg
	# udevadm test /block/sdh
	# udevadm test /block/sdi



Restart UDEV Service


	# udevadm control --reload-rules
	# /sbin/start_udev

Результат:

	# ls /dev/asm*
	/dev/asm-disk1  /dev/asm-disk3  /dev/asm-disk5  /dev/asm-disk7
	/dev/asm-disk2  /dev/asm-disk4  /dev/asm-disk6


<br/>

-->
