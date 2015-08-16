---
layout: page
title: Описание системы, которое будет настраиваться
permalink: /docs/oracle-database/installation/oracle-database-installation/distributed/dataguard/linux/6.7/oracle/12.1/info-about-env/
---

# [Инсталляция Oracle Active DataGuard 12.1 в операционной системе Centos 6.7]: Описание системы, которое будет настраиваться



<br/>


1) Устанавливаю 2 сервера как <a href="/docs/oracle-database/installation/oracle-database-installation/single/asm/linux/6.7/oracle/12.1/">здесь</a>


**На втором (StandBy) не создаю instance. Он будет скопирован с первого**


    Primary:  
    Hostname: moscow
    IP: 192.168.1.11  
    DB_Name: orcl12
    DB_UNIQUE_NAME: master


<br/>

    StandBy:  
    Hostname: piter  
    IP: 192.168.1.12  
    DB_Name: orcl12
    DB_UNIQUE_NAME: slave


<br/>

DB_UNIQUE_NAME - можно задать при создании instance. При выборе - выбрать Advanced.

<img src="http://img.oradba.net/oracle-database-installation/distributed/dataguard/linux/6.7/oracle/12.1/db-unique-name.png" border="0" alt="oracle database software installation"><br/><br/>


Либо манипуляциями с редактированием pfile.
