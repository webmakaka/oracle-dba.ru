---
layout: page
title: Инсталляция Oracle DataBase 12c в Oracle Linux 6.7 - Конфигурирование системных пользователей, настройка параметров системы
description: Инсталляция Oracle DataBase 12c в операционной системе Oracle Linux 6.7 - Конфигурирование системных пользователей, настройка параметров системы
keywords: Oracle DataBase 12c, Oracle Linux 6.7, Конфигурирование системных пользователей, настройка параметров системы
permalink: /database/installation/single-instance/simple/linux/6.7/oracle/12.1/prepare-kernel-parameters-and-user-environments/
---

# <a href="/database/installation/single-instance/simple/linux/6.7/oracle/12.1/">[Инсталляция Oracle DataBase Server 12.1 в Oracle Linux 6.7]</a>: Конфигурирование системных пользователей, настройка параметров системы

Перед тем как вносить изменения в конфигурационные файлы, рекомедуется сделать их резервные копии:

    # {
        cp /etc/sysctl.conf /etc/sysctl.conf.bkp.$(date +%Y-%m-%d)
        cp /etc/security/limits.conf /etc/security/limits.conf.bkp.$(date +%Y-%m-%d)
        cp /etc/pam.d/login /etc/pam.d/login.bkp.$(date +%Y-%m-%d)
        cp /etc/profile /etc/profile.bkp.$(date +%Y-%m-%d)
    }

### Создание пользователей и групп

Создаем группы:

    # groupadd -g 1000 oinstall
    # groupadd -g 1001 dba
    # groupadd -g 1002 oper

Создаем пользователя oracle12, сообщаем, что он будет находиться в группах dba и oinstall и домашним каталогом у него будет /home/oracle12

    # useradd \
    -g oinstall \
    -G dba,oper \
    -d /home/oracle12 \
    -m oracle12

Устанавливаем пароль для пользователя oracle12

    # passwd oracle12

Изменение параметров ядра и параметров учетной записи с правами администратора базы данных

1. Отредактируйте файл /etc/sysctl.conf

Рекомендуется закомментировать (поставить перед ними знак #) имеющиеся параметры kernel.shmmax и kernel.shmall. Далее они будут добавлены в качестве параметров вместе с остальными параметрами Oracle. Для этого выполните следующие команды:

    # sed -i.gres "s/kernel.shmmax/#kernel.shmmax/g" /etc/sysctl.conf
    # sed -i.gres "s/kernel.shmall/#kernel.shmall/g" /etc/sysctl.conf

<br/>

    # vi /etc/sysctl.conf

<br/>

    kernel.shmmax = RAM (in bytes) / 2

<br/>

Количество байт отперативной памяти, можно узнать командой

    # free -b
    4152623104 / 2 = 2076311552

Добавьте в конец файла /etc/sysctl.conf следующие параметры ядра.

    ############################################
    #### Kernel Parameters for Oracle 12

    kernel.sem = 250 32000 100 128
    kernel.shmall = 2097152
    kernel.shmmax = 2076311552
    kernel.shmmni = 4096
    fs.file-max = 6815744
    fs.aio-max-nr = 1048576
    net.ipv4.ip_local_port_range = 20000 65500
    net.core.rmem_default = 262144
    net.core.rmem_max = 4194304
    net.core.wmem_default = 262144
    net.core.wmem_max = 1048586
    vm.min_free_kbytes = 23168

    ############################################

2.  Отредактируйте файл /etc/security/limits.conf

        	# vi /etc/security/limits.conf

Добавьте следующие строки

    ############################################
    #### Settings required for Oracle 12

    oracle12 soft nproc 2047
    oracle12 hard nproc 16384
    oracle12 soft nofile 1024
    oracle12 hard nofile 65536
    oracle12 soft stack 10240
    oracle12 hard stack 32768

    ############################################

3.  Отредактируйте файл /etc/pam.d/login

        	# vi /etc/pam.d/login

Добавьте следующие строки

    ############################################
    #### Settings required for Oracle 12

    session required pam_limits.so
    ############################################

4.  Отредактируйте файл /etc/profile

        	# vi /etc/profile

Перед

    unset i
    unset pathmunge

Добавьте

    ###########################################
    #### Shell limits for Oracle 12 user accounts

    if [ $USER = "oracle12" ]; then
    ulimit -u 16384 -n 65536
    fi
    ############################################

Применить параметры ядра без перезагрузки можно следующей командой:

    # sysctl -p

5. Отредактируйте файл /home/oracle/.bash_profile

    # su - oracle12

<br/>

    $  vi ~/.bash_profile

После

    # User specific environment and startup programs

Добавьте

```
############################################
#### Oracle 12 Parameters

umask 022

export ORACLE_BASE=/u01/oracle
export ORACLE_HOME=$ORACLE_BASE/database/12.1
export ORACLE_SID=orcl12
export ORACLE_UNQNAME=orcl12
export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
export NLS_DATE_FORMAT="DD.MM.YYYY HH24:MI:SS"

export PATH=$PATH:$ORACLE_HOME/bin
export LD_LIBRARY_PATH=$ORACLE_HOME/lib

export NLS_DATE_FORMAT='dd/mm/yyyy hh24:mi:ss'

alias sqlplus='rlwrap sqlplus'
alias rman='rlwrap rman'

############################################
```

Применить переменные, определенные в файле .bash_profile к текущей сессии bash можно следующей командой:

    $ source ~/.bash_profile
