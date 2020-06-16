---
layout: page
title: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Инсталляция ASMLIB для работы ASM
description: Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID - Инсталляция ASMLIB для работы ASM
keywords: Oracle DataBase 12.1, Centos 6.7, ASM, GRID
permalink: /database/installation/single/asm/linux/6.7/oracle/12.1/asmlib-installation/
---

# <a href="/database/installation/single/asm/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Centos 6.7 с использованием ASM и GRID]</a>: Инсталляция ASMLIB для работы ASM

<br/>

<a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/install-mandatory-packages/">Обязательные для установки Oracle DataBase пакеты должны быть установлены</a>

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

Скачать: oracleasmlib-\*.x86_64.rpm

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
