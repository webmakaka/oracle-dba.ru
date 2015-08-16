---
layout: page
title: Инсталляция Oracle Instant Client 11.2 в Oracle Linux
permalink: /oracle_client_installation/linux/6.3/oracle/11.2/
---

### [Инсталляция Oracle Instant Client 11.2 в Oracle Linux]

<br/>

Distrib:<br/>
http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html

Info:<br/>
http://docs.oracle.com/cd/E11882_01/server.112/e16604/apd.htm


Нужны:

<ul>
	<li>instantclient-basic-linux.x64-11.2.0.3.0.zip</li>
	<li>instantclient-sqlplus-linux.x64-11.2.0.3.0.zip</li>
</ul>


<br/>

Архивы следует разархивировать в 1 каталог.<br/>
Иначе возможно появится сообщение:<br/>
SP2-0667: Message file sp1<lang>.msb not found<br/>


<br/>

	# mkdir -p /u01/app/oracle/instantclient

<br/>

	# unzip instantclient-basic-linux.x64-11.2.0.3.0.zip
	# unzip instantclient-sqlplus-linux.x64-11.2.0.3.0.zip
	# mv instantclient_11_2/ 11.2
	# mv 11.2/ /u01/app/oracle/instantclient

<br/>

	# chown -R oracle11 /u01/app/oracle/instantclient/

<br/>


	# vi /etc/yum.repos.d/oracleLinuxRepoINTERNET.repo

<br/>

	[OEL_INTERNET]
	name=Oracle Enterprise Linux $releasever - $basearch
	baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/latest/$basearch/
	gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
	gpgcheck=1
	enabled=1


<br/>

	# yum install -y \
	gcc \
	make \
	readline-devel.x86_64

<br/>

	# yum install -y libaio-devel

<br/>


	# cd /tmp
	# wget http://utopia.knoware.nl/~hlub/uck/rlwrap/rlwrap-0.37.tar.gz

<br/>

	# tar zxvf rlwrap-0.37.tar.gz
	# cd rlwrap-0.37
	# ./configure

<br/>

	# make && make check && make install

<br/>


Если с sqlplus будет работать один конкретный пользователь. Данные записи следует добавить в его профиль.

	# su - oracle11

<br/>


	$ vi ~/.bash_profile


<br/>


	#################################
	## Oracle Instant Client

	export SQLPATH=/u01/app/oracle/instantclient/11.2
	export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
	export TNS_ADMIN=${SQLPATH}
	export LD_LIBRARY_PATH=${SQLPATH}
	export PATH=${SQLPATH}:${PATH}

	alias sqlplus='rlwrap sqlplus'
	alias rman='rlwrap rman'

	#################################


<br/>

	$ source ~/.bash_profile

<br/>


	# sqlplus /nolog

<br/>

	SQL> conn system/system@oracle112:1521/ora112.localdomain
	Connected.


<br/>

### Создание файла (tnsnames.ora) с параметрами подключения к базе данных


	# vi /u01/app/oracle/instantclient/11.2/tnsnames.ora

<br/>

	oracle11 =
	  (DESCRIPTION =
	    (ADDRESS = (PROTOCOL = TCP)(HOST = oracle112.localdomain)(PORT = 1521))
	    (CONNECT_DATA =
	      (SERVER = DEDICATED)
	      (SERVICE_NAME = ora112.localdomain)
	    )
	  )

<br/>

<code>oracle112.localdomain - запись в DNS или HOSTS</code>

<br/>

	# sqlplus /nolog

<br/>

	SQL> conn system/system@oracle11
	Connected.
