---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Настройка DNS сервера
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/setup-dns-server/
---

# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Настройка DNS сервера


<br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">

<tr>
<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>dnsserv</strong></span></td>
</tr>

</table>

<br/>

DNS сервер настраивается только с целью, чтобы заработал RAC. Если нужен правильно работающий DNS сервер, необходимо обрадиться к специальным руководствам по настройке DNS сервера.


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

	rac12-scan             	IN                  	A           	192.168.1.31
	rac12-scan             	IN                  	A           	192.168.1.32
	rac12-scan             	IN                  	A           	192.168.1.33


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

	31     	IN   	PTR  	rac12-scan.localdomain.
	32     	IN   	PTR  	rac12-scan.localdomain.
	33     	IN   	PTR  	rac12-scan.localdomain.

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
