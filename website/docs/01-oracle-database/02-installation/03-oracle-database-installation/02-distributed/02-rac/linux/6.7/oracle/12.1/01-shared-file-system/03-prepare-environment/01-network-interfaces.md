---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Настройка сетевых интерфейсов
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/shared-file-system/network-interfaces/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Настройка сетевых интерфейсов


<br/>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2, storage, dnsserv</strong></span></td>
</tr>

</table>


<br/>

	# vi /etc/resolv.conf

<br/>

	search localdomain
	nameserver 192.168.1.10


<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1</strong></span></td>
</tr>

</table>


	# vi /etc/sysconfig/network

<br/>

	NETWORKING=yes
	NETWORKING_IPV6=no
	HOSTNAME=rac1.localdomain
	NOZEROCONF=yes

<br/>

(public)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth0

<br/>

	DEVICE="eth0"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.1.11
	NETMASK=255.255.255.0
	GATEWAY=192.168.1.1


<br/>

(private-interconnect)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth1

<br/>

	DEVICE="eth1"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.2.11
	NETMASK=255.255.255.0


<br/>

(private-storage)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth2

<br/>

	DEVICE="eth2"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.3.11
	NETMASK=255.255.255.0


<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac2</strong></span></td>
</tr>

</table>


	# vi /etc/sysconfig/network

<br/>

	NETWORKING=yes
	NETWORKING_IPV6=no
	HOSTNAME=rac2.localdomain
	NOZEROCONF=yes

<br/>

(public)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth0

<br/>

	DEVICE="eth0"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.1.12
	NETMASK=255.255.255.0
	GATEWAY=192.168.1.1

<br/>

(private-interconnect)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth1

<br/>

	DEVICE="eth1"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.2.12
	NETMASK=255.255.255.0

<br/>

(private-storage)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth2

<br/>

	DEVICE="eth2"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.3.12
	NETMASK=255.255.255.0


Перестартовать сетевые интерфейсы, можно с помощью следующей команды:

	# service network restart

<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>storage</strong></span></td>
</tr>

</table>

	# vi /etc/sysconfig/network

<br/>

	NETWORKING=yes
	NETWORKING_IPV6=no
	HOSTNAME=storage.localdomain

<br/>

(public)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth0

<br/>

	DEVICE="eth0"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.1.15
	NETMASK=255.255.255.0
	GATEWAY=192.168.1.1

<br/>

(private-storage)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth1

<br/>

	DEVICE="eth1"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.3.15
	NETMASK=255.255.255.0


Перестартовать сетевые интерфейсы, можно с помощью следующей команды:

	# service network restart

<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>dnsserv</strong></span></td>
</tr>

</table>



	# vi /etc/sysconfig/network

<br/>

	NETWORKING=yes
	NETWORKING_IPV6=no
	HOSTNAME=dnsserv.localdomain


<br/>

(public)

	# vi /etc/sysconfig/network-scripts/ifcfg-eth0

<br/>

	DEVICE="eth0"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.1.10
	NETMASK=255.255.255.0
	GATEWAY=192.168.1.1


Перестартовать сетевые интерфейсы, можно с помощью следующей команды:

	# service network restart


<br/>


<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2, storage, dnsserv</strong></span></td>
</tr>

</table>


	# vi /etc/hosts

<br/>

	##########################################################
	## Localdomain and Localhost (hosts file, DNS)

	127.0.0.1 localhost.localdomain localhost

	##########################################################
	## Virtual VIP IPs Public Network (hosts file, DNS)

	192.168.1.21 rac1-vip.localdomain rac1-vip
	192.168.1.22 rac2-vip.localdomain rac2-vip

	##########################################################
	## eth0 Public Network (hosts file, DNS)

	192.168.1.11 rac1.localdomain rac1
	192.168.1.12 rac2.localdomain rac2
	192.168.1.15 storage.localdomain storage

	##########################################################
	## eth1 Interconnect Private Network  (hosts file, DNS)

	192.168.2.11 rac1-priv-interconnect
	192.168.2.12 rac2-priv-interconnect

	##########################################################
	## eth2 Network to nas Private Network (hosts file, DNS)

	192.168.3.11 rac1-priv-storage
	192.168.3.12 rac2-priv-storage

	##########################################################
	## SCAN and GNS (DNS, DHCP)

	## Должны быть прописаны в DNS

	# 192.168.1.31	rac12-scan.localdomain	rac-scan
	# 192.168.1.32	rac12-scan.localdomain	rac-scan
	# 192.168.1.33	rac12-scan.localdomain	rac-scan

	##########################################################
	##########################################################
