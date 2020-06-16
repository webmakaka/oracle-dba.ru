---
layout: page
title: Инсталляция бесплатной, но ограниченной по ресурсам, базы данных Oracle 18c XE на сервер Centos 7
description: Инструкция по инсталляции бесплатной, но ограниченной по ресурсам, базы данных Oracle 18c XE на сервер Centos 7
keywords: бесплатная база oracle с ограничениями, oracle xe, centos 7, инсталляция
permalink: /database/installation/single-instance/centos/7/oracle/xe/18c/
---

<br/>

# Инсталляция бесплатной, но ограниченной по ресурсам, базы данных Oracle 18c XE на сервер Centos 7

<br/>

Делаю:  
05.03.2020

<br/>

Для centos 8 репозиториев с нужными пакетами пока нет. Поэтому пока буду использовать centos 7

<br/>

Дистрибутивы базы данных:  
https://www.oracle.com/database/technologies/xe-downloads.html

Поднять чистую виртуальную машину, предлагаю с помощью vagrant скрипта

<a href="https://sysadm.ru/linux/virtual/vagrant/install/ubuntu/">Инсталляция Vargant в Ubuntu 18.04</a>

<br/>

    // Также потребуется доп. плагин
    $ vagrant plugin install vagrant-hostmanager

<br/>

    $ mkdir ~/vagrant-oracle-xe-centos7 && cd ~/vagrant-oracle-xe-centos7
    $ git clone https://bitbucket.org/oracle-dba/vagrant-centos7.git .
    $ cd centos7/

<br/>

    $ vagrant up
    $ vagrant ssh

<br/>

### Работа в подготовленной для базе данных виртуальной машине

    $ sudo su -

    // Отключаем selinux
    # sed -i.bkp -e "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/selinux/config

<br/>

    // Отключаем firewall
    # systemctl disable firewalld
    # systemctl stop firewalld

<br/>

    // Подключаем репозиторий с нужными пакетами
    # vi /etc/yum.repos.d/oracleLinuxRepoINTERNET.repo

<br/>

```
[OEL_INTERNET]
name=Oracle Enterprise Linux $releasever - $basearch
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/latest/$basearch/
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol7
gpgcheck=1
enabled=1
```

<br/>

    # yum update -y

<br/>

    # yum install -y wget

<br/>

    # mkdir /distrib
    # cd /distrib/

    # wget https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-18c-1.0-1.x86_64.rpm


    // Проверка скачанного архива. Первый раз контрольная сумма не совпала
    # sha256sum oracle-database-xe-18c-1.0-1.x86_64.rpm

    # yum -y localinstall oracle-database-xe-18c-1.0-1.x86_64.rpm

    # /etc/init.d/oracle-xe-18c configure

<br/>

### Автоматический подъем базы после перезагрузки

<br/>

    $ vi /etc/oratab

<br/>

    XE:/opt/oracle/product/18c/dbhomeXE:N

заменить на

    # XE:/opt/oracle/product/18c/dbhomeXE:N
    XE:/opt/oracle/product/18c/dbhomeXE:Y

<br/>

### Инсталляция rlwrap

rlwrap - пакет, который позволяет хранить историю команд в SQL\*PLUS и RMAN в Linux (его необходимо прописывать отдельной строкой в bash профиле). Установив данный пакет, вы сможете использовать кнопки вверх, вниз для просмотра истории введенных команд, правильную работу команды backspace и др.

    # yum install -y \
    readline-devel.x86_64

<br/>

    # yum install -y git
    # cd /tmp
    # git clone --depth=1 https://github.com/hanslub42/rlwrap

    # cd rlwrap/

<br/>

    # yum install gcc
    # yum install -y automake
    # autoreconf --install
    # automake  --add-missing
    # ./configure
    # make && make check && make install

<br/>

### Работа с базой

    // Переключиться на своего пользователя
    # su - vagrant

<br/>

    // Установливаем переменные окружения
    $ vi ~/.bash_profile

(Добавить после строчки) # User specific environment and startup programs

<br/>

```
############################################
#### Oracle Parameters

    umask 022

    export ORACLE_BASE=/opt/oracle
    export ORACLE_HOME=$ORACLE_BASE/product/18c/dbhomeXE
    export ORACLE_SID=XE
    export ORACLE_UNQNAME=XE
    export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
    export NLS_DATE_FORMAT="DD.MM.YYYY HH24:MI:SS"

    export PATH=$PATH:$ORACLE_HOME/bin
    export LD_LIBRARY_PATH=$ORACLE_HOME/lib

	alias sqlplus='rlwrap sqlplus'
    alias rman='rlwrap rman'

############################################
```

    // Применить переменные окружения к текущим настройкам bash
    $ source ~/.bash_profile

<br/>

    // Подключаюсь учетной записью system и паролем manager
    $ sqlplus system/manager

    SQL> select status from v$instance;

    SQL> select name from v$pdbs;

    NAME
    --------------------------------------------------------------------------------
    PDB$SEED
    XEPDB1

    SQL> conn sys/manager@//localhost:1521/XEPDB1 as sysdba
    Connected.

<br/>

    // Подключение к базе утилитой RMAN
    $ rman target sys/manager

<br/>
<br/>

Возможно, будет полезно:  
https://www.youtube.com/watch?v=XB1ZakqiTa8
