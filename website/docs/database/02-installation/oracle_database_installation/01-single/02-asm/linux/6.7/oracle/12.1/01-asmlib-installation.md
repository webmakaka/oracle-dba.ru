---
layout: page
title: Инсталляция ASMLIB для работы ASM
permalink: /oracle-database-installation/single/asm/linux/6.7/oracle/12.1/asmlib-installation/
---

# <a href="/oracle-database-installation/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Инсталляция ASMLIB для работы ASM

<br/>

Обязательные для установки пакеты:  
http://oracle-dba.ru/oracle-database-installation/linux/6.4/oracle/12.1/install-mandatory-packages/


<br/><br/>

    # vi /etc/yum.repos.d/OracleLinuxRepo.repo

<br/>

    [OEL6]
    name=Oracle Enterprise Linux $releasever - $basearch
    baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/latest/$basearch/
    gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
    gpgcheck=1
    enabled=1

<br/>

    # yum repolist

<br/>

### Доп пакеты понадобились:

    # yum install -y nfs-utils.x86_64


<br/>

### Необходимо установить 3 пакета для ASM:

Необходимо с сайта Oracle:

http://www.oracle.com/technetwork/server-storage/linux/asmlib/rhel6-1940776.html

Скачать: oracleasmlib-*.x86_64.rpm


    # cd /tmp
    # wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.4-1.el6.x86_64.rpm

<br/>

    # yum install -y \
    oracleasm \
    oracleasm-support \
    oracleasmlib-2.0.4-1.el6.x86_64.rpm

<br/>

Проверяем инсталлированные пакеты:

    # rpm -qa | grep oracleasm
    oracleasm-support-2.1.8-1.el6.x86_64
    oracleasmlib-2.0.4-1.el6.x86_64
    kmod-oracleasm-2.0.8-5.el6_7.x86_64
