---
layout: page
title: Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/nas/setup-dns-server/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Настройка DNS сервера

<br/>

DNS сервер настраивается только с целью, чтобы заработал RAC. Если нужен правильно работающий DNS сервер, необходимо обрадиться к специальным руководствам по настройке DNS сервера.


<br/>

## Настройка сети:

	# vi /etc/hosts

<br/>

	###############################################
	## Localdomain and Localhost (hosts file, DNS)

	127.0.0.1 localhost.localdomain localhost
	::1            localhost6.localdomain6 localhost6

	###############################################


<br/>

	# vi /etc/resolv.conf

<br/>

	search localdomain
	nameserver 192.168.1.1
	nameserver 192.168.1.10
	options attempts: 2
	options timeout: 1

<br/>

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

### Инсталляция DNS сервера:

Если в каталоге /etc/yum.repos.d нет нет файлов с описанием репозиториев Oracle Linux.


	# vi /etc/yum.repos.d/OracleLinuxRepo.repo

<br/>

	[OEL6]
	name=Oracle Enterprise Linux $releasever - $basearch
	baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/latest/$basearch/
	gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
	gpgcheck=1
	enabled=1


<br/>

	# yum install -y \
	bind \
	bind-utils


<br/>

### Настройка конфигурационных файлов DNS сервера:

	# vi /etc/named.conf


<br/>

	options
	{
	        directory "/var/named";

	};

	       // ## Localhost

	       zone "localhost" IN {
	              type master;
	              file "localhost.zone";
	              allow-update { none; };
	       };

	        zone "0.0.127.in-addr.arpa" IN {
	                type master;
	                file "127.0.0.in-addr.arpa";
	        allow-update {none;};
	        };


	 // ## Localdomain without domain prefix

	        zone "." IN  {
	                 type master;
	                 file "localdomain.zone";
	                 allow-update {none;};
	        };


	       // ## Localdomain with domain prefix



	        zone "localdomain" IN  {
	                 type master;
	                 file "localdomain.zone";
	                 allow-update {none;};
	        };



	// ## zone ARPA

	        zone "1.168.192.in-addr.arpa" IN  {
	                type master;
	                file "192.168.1.in-addr.arpa";
	        };


	        zone "2.168.192.in-addr.arpa" IN  {
	                type master;
	                file "192.168.2.in-addr.arpa";
	        };


	           zone "3.168.192.in-addr.arpa" IN  {
	                type master;
	                file "192.168.3.in-addr.arpa";
	        };


<br/>

	# vi /var/named/localhost.zone

<br/>

	$TTL 1D
	$ORIGIN localhost.
	@              IN  SOA   @  root (
	                         1   ; Serial
	                         8H  ; Refresh
	                         15M ; Retry
	                         1W  ; Expire
	                         1D) ; Minimum TTL
	               IN   NS   @
	               IN   A    127.0.0.1


<br/>

	# vi /var/named/127.0.0.in-addr.arpa

<br/>

	$TTL 1D
	$ORIGIN 0.0.127.in-addr.arpa.
	@    IN   SOA  localhost. root.localhost. (
	               1    ; serial
	               8H   ; refresh
	               15M  ; retry
	               1W   ; expire
	               1D ) ; minimum
	      IN   NS   localhost.
	1    IN   PTR  localhost.


<br/>

	# vi /var/named/localdomain.zone


<br/>

	$TTL 86400
	@                   	IN SOA              	ns1.localdomain. root.localhost (
	                                                            	2010063000 ; serial
	                                                            	28800 ; refresh
	                                                            	14400 ; retry
	                                                            	3600000 ; expiry
	                                                            	86400 ) ; minimum
	@                   	IN                  	NS          	ns1.localdomain.
	localhost           	IN                  	A           	127.0.0.1
	ns1                 	IN                  	A           	192.168.1.10

	rac-scan               	IN                  	A           	192.168.1.31
	rac-scan               	IN                  	A           	192.168.1.32
	rac-scan               	IN                  	A           	192.168.1.33


	rac1-vip            	IN                  	A           	192.168.1.21
	rac2-vip            	IN                  	A           	192.168.1.22


	rac1                	IN                  	A           	192.168.1.11
	rac2                	IN                  	A           	192.168.1.12
	storage             	IN                  	A           	192.168.1.15


	rac1-priv-interconnect  IN                  	A           	192.168.2.11
	rac2-priv-interconnect  IN                  	A           	192.168.2.12


	rac1-priv-storage     	IN                  	A           	192.168.3.11
	rac2-priv-storage      	IN                  	A           	192.168.3.12



<br/>

	# vi /var/named/192.168.1.in-addr.arpa


<br/>


	$TTL   	86400
	@      	IN   	SOA   	ns1.localdomain. postmaster.localhost. (
	                    	2010063000 ; serial
	                    	28800 ; refresh
	                    	14400 ; retry
	                    	3600000 ; expiry
	                    	86400 ) ; minimum
	@      	IN   	NS   	ns1.localdomain.
	
	31     	IN   	PTR  	rac-scan.localdomain.
	32     	IN   	PTR  	rac-scan.localdomain.
	33     	IN   	PTR  	rac-scan.localdomain.

	21     	IN   	PTR  	rac1-vip.localdomain.
	22     	IN   	PTR  	rac2-vip.localdomain.

	11     	IN   	PTR  	rac1.localdomain.
	12     	IN   	PTR  	rac2.localdomain.
	13     	IN   	PTR  	storage.localdomain.


<br/>

	# vi /var/named/192.168.2.in-addr.arpa

<br/>

	$TTL   	86400
	@      	IN   	SOA   	ns1.localdomain. postmaster.localhost. (
	                    	2010063000 ; serial
	                    	28800 ; refresh
	                    	14400 ; retry
	                    	3600000 ; expiry
	                    	86400 ) ; minimum
	@      	IN   	NS   	ns1.localdomain.

	11     	IN   	PTR  	rac1-priv-interconnect.localdomain.
	12     	IN   	PTR  	rac2-priv-interconnect.localdomain.

<br/>

	# vi /var/named/192.168.3.in-addr.arpa

<br/>


	$TTL   	86400
	@      	IN   	SOA   	ns1.localdomain. postmaster.localhost. (
	                    	2010063000 ; serial
	                    	28800 ; refresh
	                    	14400 ; retry
	                    	3600000 ; expiry
	                    	86400 ) ; minimum
	@      	IN   	NS   	ns1.localdomain.

	11     	IN   	PTR  	rac1-priv-storage.localdomain.
	12     	IN   	PTR  	rac2-priv-storage.localdomain.


Добавление в автозапуск:

	# chkconfig --level 345 named on

Restart

	# service named restart


Статус:

	rndc status


Проверка на клиентах:

	nslookup rac1
	nslookup rac2.localdomain
	nslookup 192.168.1.11
