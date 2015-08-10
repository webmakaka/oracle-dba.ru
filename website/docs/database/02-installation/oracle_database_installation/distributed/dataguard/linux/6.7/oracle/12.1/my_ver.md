---
layout: page
title: Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/1/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]:


1) Устанавливаю 2 сервера как здесь
http://oracle-dba.ru/oracle-database-installation/asm/linux/6.7/oracle/12.1/


На втором не создаю instance.


Primary:  
Hostname: moscow  
Instance: orcl  
IP: 192.168.1.11  

StandBy:  
Hostname: piter  
Instance: orcl  
IP: 192.168.1.12  


Все время забываю, где прописывается hostname сервера

	# vi /etc/sysconfig/network


Устанавливаю пакет scp для копирования данных между серверами на обоих узлах

	# yum install -y openssh-clients


<br/>

	# vi /etc/hosts


	## Localdomain and Localhost

	127.0.0.1 localhost.localdomain localhost


	## DataBases

	# moscow - primary; piter - standby

	192.168.1.10 moscow.localdomain moscow
	192.168.1.11 piter.localdomain piter


<br/>



### Primary
