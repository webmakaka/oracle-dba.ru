---
layout: page
title: Инсталляция Oracle DataBase 12.2 в Oracle Linux 7.4 - Конфигурирование системных пользователей, настройка параметров системы
description: Инсталляция Oracle DataBase 12.2 в операционной системе Oracle Linux 7.4 - Конфигурирование системных пользователей, настройка параметров системы
keywords: Oracle DataBase 12.2, Oracle Linux 7.4, создание пользователей
permalink: /database/installation/single-instance/simple/linux/7.4/oracle/12.2/prepare-kernel-parameters-and-user-environments/
---

<br/>

# <a href="/database/installation/single-instance/simple/linux/7.4/oracle/12.2/">[Инсталляция Oracle DataBase Server 12.2 в Oracle Linux 7.4]</a>:: Конфигурирование системных пользователей, настройка параметров системы

<br/>

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

<br/>

### Изменение параметров ядра и параметров учетной записи с правами администратора базы данных

    # echo 2076311552 > /proc/sys/kernel/shmmax

    # echo 6815744 > /proc/sys/fs/file-max
    # echo 1048576 > /proc/sys/fs/aio-max-nr


    # echo 262144 > /proc/sys/net/core/rmem_default
    # echo 4194304 > /proc/sys/net/core/rmem_max

    # echo 262144 > /proc/sys/net/core/wmem_default
    # echo 1048586 > /proc/sys/net/core/wmem_max

<br/>

    Применить параметры ядра без перезагрузки можно следующей командой:

    	# sysctl -p

Посмотреть результат:

    # sysctl -a | grep file-max

<br/>

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

<br/>

3.  Отредактируйте файл /etc/pam.d/login

        	# vi /etc/pam.d/login

Добавьте следующие строки

    ############################################
    #### Settings required for Oracle 12

    session required pam_limits.so
    ############################################

<br/>

4.  Отредактируйте файл /etc/profile

    # vi /etc/profile

В конце файла перед следующими командами.

    unset i
    unset pathmunge

Добавьте:

{% highlight shell %}

###########################################

#### Shell limits for Oracle 12 user accounts

if [ $USER = "oracle12" ]; then
ulimit -u 16384 -n 65536
fi
############################################

{% endhighlight %}

<br/>

5. Отредактируйте файл /home/oracle/.bash_profile

   # su - oracle12

<br/>

    $  vi ~/.bash_profile

После

    # User specific environment and startup programs

Добавьте

{% highlight shell %}

############################################

#### Oracle 12 Parameters

umask 022

export ORACLE_BASE=/u01/oracle
export ORACLE_HOME=\$ORACLE_BASE/database/12.2
export ORACLE_SID=orcl12
export ORACLE_UNQNAME=orcl12
export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
export NLS_DATE_FORMAT="DD.MM.YYYY HH24:MI:SS"

export PATH=$PATH:$ORACLE_HOME/bin
export LD_LIBRARY_PATH=\$ORACLE_HOME/lib

export NLS_DATE_FORMAT='dd/mm/yyyy hh24:mi:ss'

alias sqlplus='rlwrap sqlplus'
alias rman='rlwrap rman'

############################################

{% endhighlight %}

Применить переменные, определенные в файле .bash_profile к текущей сессии bash можно следующей командой:

    $ source ~/.bash_profile
