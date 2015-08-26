---
layout: page
title: Oracle RAC 12.1 SHARED FILE SYSTEM - Изменение параметров ядра и параметров учетной записи администратора базы данных
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/6.7/oracle/12.1/iscsi-asm/configure-kernel-parameters-and-user-environments/
---


# [Инсталляция Oracle RAC 12.1 SHARED FILE SYSTEM]: Изменение параметров ядра и параметров учетной записи администратора базы данных



<br/>


<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Редактирование конфиг файлов</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>rac1, rac2</strong></span></td>
	</tr>
</table>


Перед тем как вносить изменения в конфигурационные скрипты, следует предварительно создать их резервные копии:

	# {
	cp /etc/sysctl.conf /etc/sysctl.conf.bkp
	cp /etc/security/limits.conf /etc/security/limits.conf.bkp
	cp /etc/pam.d/login /etc/pam.d/login.bkp
	cp /etc/profile /etc/profile.bkp
	}


1) Отредактируйте файл  /etc/sysctl.conf

Рекомендуется закомментировать (поставить перед ними знак #) имеющиеся параметры kernel.shmmax и kernel.shmall. Далее они будут добавлены в качестве параметров вместе с остальными параметрами Oracle.

	# sed -i.gres "s/kernel.shmmax/#kernel.shmmax/g" /etc/sysctl.conf
	# sed -i.gres "s/kernel.shmall/#kernel.shmall/g" /etc/sysctl.conf

<br/>

	# vi /etc/sysctl.conf

<br/>

kernel.shmmax = 50% of RAM (in bytes) / 2

<br/>

Количество байт отперативной памяти, можно узнать введя команду

	# free -b


Добавьте в конец документа следующие параметры ядра.

	#################################################
	#### Oracle 12 Kernel Parameters

	kernel.sem = 250 32000 100 128

	kernel.shmall = 2097152
	kernel.shmmax = 2202540032
	kernel.shmmni = 4096
	fs.file-max = 6815744
	fs.aio-max-nr = 1048576
	net.ipv4.ip_local_port_range = 20000 65500
	net.core.rmem_default = 262144
	net.core.rmem_max = 4194304
	net.core.wmem_default = 262144
	net.core.wmem_max = 1048586
	vm.min_free_kbytes = 23168


	### New Parameters

	kernel.panic_on_oops = 1
	################################################

Применить параметры ядра, можно командой

	# sysctl -p



2) Отредактируйте файл /etc/security/limits.conf

	# vi /etc/security/limits.conf

<br/>

	################################################
	# Settings required for Oracle 12

	oracle12 soft nproc 2047
	oracle12 hard nproc 16384
	oracle12 soft nofile 1024
	oracle12 hard nofile 65536
	oracle12 soft stack 10240
	oracle12 hard stack 32768


	### Maximum locked memory
	oracle12  hard  memlock  3871653
	################################################


3) Отредактируйте файл /etc/pam.d/login

	# vi /etc/pam.d/login

<br/>

	################################################
	# Settings required for Oracle 12

		session required pam_limits.so
	################################################

4) Отредактируйте файл /etc/profile

	# vi /etc/profile

Перед  

unset i  
unset pathmunge

Добавляем:


	################################################
	# Shell limits for Oracle 12 user accounts

	if [ $USER = "oracle12" ]; then
	ulimit -u 16384 -n 65536
	fi
	################################################


<br/>

<span style="font-size: 20px; text-align: left; line-height: 130%; font-family: Arial,Helvetica,sans-serif; color: rgb(153, 0, 0);">
<strong>Настройка параметров окружения пользователя oracle11 на узлах кластера</strong></span>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node1</strong></span></td>
	</tr>
</table>


5) Отредактируйте файл /home/oracle12/.bash_profile

Значения ORACLE_SID и ORACLE_UNQNAME должны быть уникальны на каждой из нод кластера. В остальном конфиги одинаковы.


	# su - oracle12

	#  vi ~/.bash_profile

Сразу после:

	# User specific environment and startup programs


	############################################
	#### Oracle 12 Parameters rac1

	   umask 022

	   # Different Parameters

	    export ORACLE_SID=rac121
	    export ORACLE_UNQNAME=rac121
	    export ORACLE_HOSTNAME=rac1.localdomain

	   # Grid

	    export GRID_HOME=/u01/app/grid/12.1
	    export CRS_HOME=${GRID_HOME}/crs

	   # DataBase

	   export ORACLE_BASE=/u01/app/oracle
	   export ORACLE_HOME=${ORACLE_BASE}/product/rac/12.1

	   # NLS

	   export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
	   export NLS_DATE_FORMAT="DD.MM.YYYY HH24:MI:SS"

	   # Other
	   export ORACLE_OWNER=oracle12

	   # Alias

	    alias sqlplus='rlwrap sqlplus'
	    alias rman='rlwrap rman'

	   # Path

	   export LD_LIBRARY_PATH=$ORACLE_HOME/lib
	   export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin:$CRS_HOME/bin

	############################################


<br/><br/>

<table cellpadding="4" cellspacing="2" align="center" border="0" width="100%">
	<tr>
		<td style="color: rgb(255, 255, 255);" bgcolor="#386351" width="14%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>Server:</strong></span></td>
		<td height="20" bgcolor="#a2bcb1" width="60%"><span style="font-family: Arial,Helvetica,sans-serif; font-size: 14px;"><strong>node2</strong></span></td>
	</tr>
</table>

	# su - oracle12

	#  vi ~/.bash_profile

<br/>

	############################################
	#### Oracle 12 Parameters rac2

	   umask 022

	   # Different Parameters

		export ORACLE_SID=rac122
		export ORACLE_UNQNAME=rac122
		export ORACLE_HOSTNAME=rac2.localdomain

	   # Grid

		export GRID_HOME=/u01/app/grid/12.1
		export CRS_HOME=${GRID_HOME}/crs

	   # DataBase

	   export ORACLE_BASE=/u01/app/oracle
	   export ORACLE_HOME=${ORACLE_BASE}/product/rac/12.1

	   # NLS

	   export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
	   export NLS_DATE_FORMAT="DD.MM.YYYY HH24:MI:SS"

	   # Other
	   export ORACLE_OWNER=oracle12

	   # Alias

		alias sqlplus='rlwrap sqlplus'
		alias rman='rlwrap rman'

	   # Path

	   export LD_LIBRARY_PATH=$ORACLE_HOME/lib
	   export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin:$CRS_HOME/bin

	############################################

Применить параметры к текущей сессии консоли bash можно следующей командой:

	# source ~/.bash_profile
