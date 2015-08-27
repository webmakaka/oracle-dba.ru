---
layout: page
title: Oracle RAC 11.2 ISCSI + ASM - Копирование дистрибутивов базы данных на сервер
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/copy-oracle-distrib-on-server/
---

# <a href="/docs/oracle-database/installation/oracle-database-installation/distributed/rac/linux/5.8/oracle/11.2/">[Инсталляция Oracle RAC 11.2 в операционной системе Oracle Linux 5.8 x86_64]</a>: Копирование дистрибутивов базы данных на сервер


<br/>


Необходимо скопировать следующие архивы на сервер (в каталог /tmp):

p10404530_112030_Linux-x86-64_1of7.zip  
p10404530_112030_Linux-x86-64_2of7.zip  
p10404530_112030_Linux-x86-64_3of7.zip  

<br/>

	# scp marley@192.168.1.5:/mnt/dsk2/_ISO/oracle/linux/11.2.0.3.0/p10404530_112030_Linux-x86-64_{1..3}of7.zip /tmp/

<br/>

	# chown -R oracle11:oinstall /tmp/p10404530_112030_Linux-x86-64_*
