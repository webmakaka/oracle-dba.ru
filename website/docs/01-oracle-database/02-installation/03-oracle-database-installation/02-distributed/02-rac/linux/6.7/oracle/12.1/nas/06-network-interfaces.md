---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/network-interfaces/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Настройка сетевых интерфейсов

<br/>



### Настройка на storage, node1, node2:

	# vi /etc/hosts

<br/>

	###############################################
	## Localdomain and Localhost (hosts file, DNS)

	127.0.0.1 localhost.localdomain localhost
	::1            localhost6.localdomain6 localhost6

	###############################################
	## Virtual VIP IPs Public Network (hosts file, DNS)

	192.168.1.21 rac1-vip.localdomain rac1-vip
	192.168.1.22 rac2-vip.localdomain rac2-vip

	###############################################
	## eth0 Public Network (hosts file, DNS)

	192.168.1.11 rac1.localdomain rac1
	192.168.1.12 rac2.localdomain rac2
	192.168.1.15 storage.localdomain storage

	################################################
	## eth1 Interconnect Private Network  (hosts file, DNS)

	192.168.2.11 rac1-priv-interconnect
	192.168.2.12 rac2-priv-interconnect

	#################################################
	## eth2 Network to nas Private Network (hosts file, DNS)

	192.168.3.11 rac1-priv-storage
	192.168.3.12 rac2-priv-storage

	#################################################
	## SCAN and GNS (DNS, DHCP)

	## Прописаны в DNS

	# 192.168.1.31	rac-scan.localdomain	rac-scan
	# 192.168.1.32	rac-scan.localdomain	rac-scan
	# 192.168.1.33	rac-scan.localdomain	rac-scan

	#################################################
	#################################################

<br/>

	# vi /etc/resolv.conf

<br/>

	search localdomain
	nameserver 192.168.1.1
	nameserver 192.168.1.10
	options attempts: 2
	options timeout: 1

<br/>

### Настройка сети узел 1 (rac1):


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

### Настройка сети узел 2 (rac2):


	# vi /etc/sysconfig/network

<br/>

	NETWORKING=yes
	NETWORKING_IPV6=no
	HOSTNAME=rac2.localdomain


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

### Настройка сети (storage):

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
