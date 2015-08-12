---
layout: page
title: Описание системы, которое будет настраиваться
permalink: /oracle-database-installation/dataguard/linux/6.7/oracle/12.1/info-about-env/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Описание системы, которое будет настраиваться



<br/>


1) Устанавливаю 2 сервера как здесь:  
http://oracle-dba.ru/oracle-database-installation/asm/linux/6.7/oracle/12.1/


На втором (StandBy) не создаю instance. Он будет скопирован с первого.


Primary:  
Hostname: moscow  
Instance: orcl12  
IP: 192.168.1.11  

StandBy:  
Hostname: piter  
IP: 192.168.1.12  
