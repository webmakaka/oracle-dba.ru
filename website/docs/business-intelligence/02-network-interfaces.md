---
layout: page
title: Настройка конфигурации сетевых интерфейсов
permalink: /docs/business-intelligence/installation/network-interfaces/
---



<h2>Настройка конфигурации сетевых интерфейсов</h2>



Необходимо выбрать подходящее имя для сервера, которое бы отражало его роль и назначение в сети.


Для этого, с помощью редактора (например, vi) отредактируйте файл /etc/sysconfig/network



Задайте параметры, согласно характеристикам Вашей сети.



Не рекомендуется в hostname использовать знак нижнего подчеркивания (_).
(Enterprise Manager и другие web приложения не смогут подключиться к базе по http/https)


	# vi /etc/sysconfig/network

<br/>


	NETWORKING=yes
	NETWORKING_IPV6=no
	HOSTNAME=oraclebi.localdomain


<br/>

	# vi /etc/sysconfig/network-scripts/ifcfg-eth0


<br/>


	DEVICE="eth0"
	ONBOOT="yes"
	BOOTPROTO="static"
	IPADDR=192.168.1.9
	NETMASK=255.255.255.0
	GATEWAY=192.168.1.1


<br/>

	# vi /etc/resolv.conf

<br/>


	nameserver 192.168.1.1
	nameserver 127.0.0.1
	search localdomain

	options attempts: 2
	options timeout: 1


<br/>

	# vi /etc/hosts

<br/>

	## Localdomain and Localhost (hosts file, DNS)
	127.0.0.1 localhost.localdomain localhost
	::1            localhost6.localdomain6 localhost6

	## IPs Public Network (hosts file, DNS)
	192.168.1.9 oraclebi.localdomain oraclebi
	192.168.1.10 oracle112.localdomain oracle112

Перестартовать сетевые интерфейсы, можно с помощью следующей команды:

	# service network restart
