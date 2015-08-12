---
layout: page
title: Предварительные шаги по настройке environment
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/prepare-env/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Предварительные шаги по настройке environment


### Следующие шаги выполняются на Primary и Standby


Все время забываю, где прописывается hostname сервера

	# vi /etc/sysconfig/network

**После переименования, лучше перезагрузить сервер или каким-то способом применить изменения, или иначе в конфигах будет прописано что-то не то и придется их потом еще и править**

<br/>

Устанавливаю пакет scp для копирования данных между серверами на обоих узлах

	# yum install -y openssh-clients


<br/>

	# vi /etc/hosts

<br/>

	## Localdomain and Localhost

	127.0.0.1 localhost.localdomain localhost


	## DataBases

	# moscow - primary; piter - standby

	192.168.1.11 moscow.localdomain moscow
	192.168.1.12 piter.localdomain piter


<br/>


	$ vi /home/oracle12/.bash_profile



<br/>

**PRIMARY**


<br/>

	#######################################################
	#### Oracle 12.1 Parameters ###########################

		umask 022

		export ORACLE_BASE=/u01/oracle
		export ORACLE_HOME=$ORACLE_BASE/database/12.1

		export GRID_HOME=$ORACLE_BASE/grid/12.1

		export ORACLE_SID=master
		export ORACLE_UNQNAME=master
		export NLS_LANG=AMERICAN_AMERICA.AL32UTF8

		export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin
		export LD_LIBRARY_PATH=$ORACLE_HOME/lib


		# rlwrap aliases

		alias sqlplus='rlwrap sqlplus'
		alias rman='rlwrap rman'
		alias asmcmd='rlwrap asmcmd'


		# my alases

		alias alert='tail -f $ORACLE_BASE/diag/rdbms/$ORACLE_SID/$ORACLE_SID/trace/alert_$ORACLE_SID.log'

	#### Oracle 12.1 Parameters ###########################
	#######################################################



**Standby**


<br/>

	#######################################################
	#### Oracle 12.1 Parameters ###########################

		umask 022

		export ORACLE_BASE=/u01/oracle
		export ORACLE_HOME=$ORACLE_BASE/database/12.1

		export GRID_HOME=$ORACLE_BASE/grid/12.1

		export ORACLE_SID=slave
		export ORACLE_UNQNAME=slave
		export NLS_LANG=AMERICAN_AMERICA.AL32UTF8

		export PATH=$PATH:$ORACLE_HOME/bin:$GRID_HOME/bin
		export LD_LIBRARY_PATH=$ORACLE_HOME/lib


		# rlwrap aliases

		alias sqlplus='rlwrap sqlplus'
		alias rman='rlwrap rman'
		alias asmcmd='rlwrap asmcmd'


		# my alases

		alias alert='tail -f $ORACLE_BASE/diag/rdbms/$ORACLE_SID/$ORACLE_SID/trace/alert_$ORACLE_SID.log'

	#### Oracle 12.1 Parameters ###########################
	#######################################################
